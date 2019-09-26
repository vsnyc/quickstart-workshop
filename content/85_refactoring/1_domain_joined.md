+++
title = "Deploy a domain joined AMI"
chapter = false
weight = 1
+++

Let's take the example of the current standalone Tableau server on Windows quick start and see what it would take to join it to an Active Directory domain. 

### Fork the Tableau server quick start
In a browser, go to https://github.com/vsnyc/quickstart-tableau-server and use the Fork action at top right to fork the repository to your GitHub account.

### Clone the forked Tableau server quick start

```
cd ~/environment
export GITHUB_USERNAME=<change-me>
git clone --recursive https://github.com/${GITHUB_USERNAME}/quickstart-tableau-server.git --branch develop
cd quickstart-tableau-server
```

### Add Active Directory Quick Start as a submodule
We already have an Active Directory quick start that gives a couple of options to configure AD. We'll go with the option of creating a AWS Managed AD resource. Let's start with adding the quick start as a submodule.

```
git submodule add -b master https://github.com/aws-quickstart/quickstart-microsoft-activedirectory.git submodules/quickstart-microsoft-activedirectory
```

### Add Microsoft Quick Start utilities as a submodule

```
git submodule add -b master https://github.com/aws-quickstart/quickstart-microsoft-utilities.git submodules/quickstart-microsoft-utilities
```

You should see new submodules added.

```
ls submodules/
```
Commit your changes and push to the develop branch.

`git commit -a -m "Added Active Directory and Microsoft utilities submodules"`

Run `git push origin develop`


### Update parameters

Add the following parameters to `tableau-single-server-master.template`,  `tableau-single-server.template`, and `tableau-single-server-windows.template`. Notice the last dangling commma, this assumes the block was pasted in the middle matching alphabetical order.

```
    "DomainAdminPassword": {
      "AllowedPattern": "(?=^.{6,255}$)((?=.*\\d)(?=.*[A-Z])(?=.*[a-z])|(?=.*\\d)(?=.*[^A-Za-z0-9])(?=.*[a-z])|(?=.*[^A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z])|(?=.*\\d)(?=.*[A-Z])(?=.*[^A-Za-z0-9]))^.*",
      "Description": "Password for the domain admin user. Must be at least 8 characters containing letters, numbers and symbols",
      "MaxLength": "32",
      "MinLength": "8",
      "NoEcho": "true",
      "Type": "String"
    },
    "DomainDNSName": {
      "AllowedPattern": "[a-zA-Z0-9]+\\..+",
      "Default": "example.com",
      "Description": "Fully qualified domain name (FQDN) of the forest root domain e.g. example.com",
      "MaxLength": "255",
      "MinLength": "2",
      "Type": "String"
    },
    "DomainNetBIOSName": {
      "AllowedPattern": "[a-zA-Z0-9]+",
      "Default": "example",
      "Description": "NetBIOS name of the domain (up to 15 characters) for users of earlier versions of Windows e.g. EXAMPLE",
      "MaxLength": "15",
      "MinLength": "1",
      "Type": "String"
    },
```

### Add Active Directory Cloudformation resource

```
    "ADStack": {
      "DependsOn": "VPCStack",
      "Type": "AWS::CloudFormation::Stack",
      "Properties": {
        "TemplateURL": {
          "Fn::Sub": "https://${QSS3BucketName}.s3.amazonaws.com/${QSS3KeyPrefix}submodules/quickstart-microsoft-activedirectory/templates/ad-3.template"
        },
        "Parameters": {
          "DomainAdminPassword": {
            "Ref": "DomainAdminPassword"
          },
          "DomainDNSName": {
            "Ref": "DomainDNSName"
          },
          "DomainNetBIOSName": {
            "Ref": "DomainNetBIOSName"
          },
          "PrivateSubnet1CIDR": {
            "Ref": "PublicSubnet1CIDR"
          },
          "PrivateSubnet1ID": {
            "Fn::GetAtt": [
              "VPCStack",
              "Outputs.PublicSubnet1ID"
            ]
          },
          "PrivateSubnet2CIDR": {
            "Ref": "PublicSubnet2CIDR"
          },
          "PrivateSubnet2ID": {
            "Fn::GetAtt": [
              "VPCStack",
              "Outputs.PublicSubnet2ID"
            ]
          },
          "PublicSubnet1CIDR": {
            "Ref": "PublicSubnet1CIDR"
          },
          "PublicSubnet2CIDR": {
            "Ref": "PublicSubnet2CIDR"
          },
          "QSS3BucketName": {
            "Ref": "QSS3BucketName"
          },
          "QSS3KeyPrefix": {
            "Fn::Sub": "${QSS3KeyPrefix}submodules/quickstart-microsoft-activedirectory/"
          },
          "VPCID": {
            "Fn::GetAtt": [
              "VPCStack",
              "Outputs.VPCID"
            ]
          },
          "VPCCIDR": {
            "Ref": "VPCCIDR"
          }
        }
      }
    },
```

### Make the WorkloadStack dependent on AD Stack

In WorkloadStack, change `"DependsOn": ["VPCStack"],` to `"DependsOn": ["ADStack"]`.

### Pass the AD parameters to the nested Workload stack resource.

In `tableau-single-server.template` and `tableau-single-server-windows.template` the following parameters in the nested WorkloadStack resource. 

**NOTE: This change will break the Linux versions since the corresponding parameters are not added there yet.**

```
          "DomainAdminPassword": {
            "Ref": "DomainAdminPassword"
          },
          "DomainDNSName": {
            "Ref": "DomainDNSName"
          },
          "DomainNetBIOSName": {
            "Ref": "DomainNetBIOSName"
          },
```          

### Update Windows Tableau server template to join to AD

Open tableau-single-server-windows.template. In the TableauWindowsServer resource, `Metadata/CloudFormation::Init/config/files` section, add a snippet to download Join-Domain powershell script.

```
"c:\\cfn\\scripts\\Join-Domain.ps1": {
    "source": {
        "Fn::Sub": "https://aws-quickstart.s3.amazonaws.com/quickstart-microsoft-rdgateway/submodules/quickstart-microsoft-utilities/scripts/Join-Domain.ps1"
    }
}
```

In `Metadata/CloudFormation::Init/config/commands` section, add a command to join AD domain. Replace commands `2-create-user` and `3-add-admin` with the below.

```
"2-set-execution-policy": {
    "command": "powershell.exe -Command \"Set-ExecutionPolicy RemoteSigned -Force\"",
    "waitAfterCompletion": "0"
},
"3-join-domain": {
    "command": {
        "Fn::Join": [
            "",
            [
                "powershell.exe -Command \"C:\\cfn\\scripts\\Join-Domain.ps1 -DomainName '",
                {
                    "Ref": "DomainDNSName"
                },
                "' -UserName '",
                {
                    "Ref": "DomainNetBIOSName"
                },
                "\\Admin",
                "' -Password '",
                {
                    "Ref": "DomainAdminPassword"
                },
                "'\""
            ]
        ]
    },
    "waitAfterCompletion": "forever"
},
```

### Update Windows Tableau server template authentication from Local to AD (need help)

Replace the definition of `c:\\tabsetup\\config.json` with the following:

```
"c:\\tabsetup\\config.json": {
    "content": {
        "configEntities": {
            "identityStore": {
                "_type": "identityStoreType",
                "type": "activedirectory",
                "domain": {
                    "Ref": "DomainDNSName"
                },
                "nickname": {
                    "Ref": "DomainNetBIOSName"
                },
                "username": "Admin",
                "password": {
                    "Ref": "DomainAdminPassword"
                }
            }
        },
        "topologyVersion": {}
    }
},
```

### Test the changes. 
We'll make a copy of taskcat.yml and single-windows.json test specification files to test our changes.

```
cp ci/taskcat.yml ci/taskcat-local.yml
cp ci/single-windows.json ci/single-windows-local.json
```

Open taskcat-local.yml and delete or comment out all tests except `single-windows`.

Change the `parameter_input` value for `single-windows` test to: `single-windows-local.json`. Reduce the regions to just one, e.g. `us-west-2`.

Open `single-windows-local.json` and update test parameters. Update the following keys:

* KeyPairName
* Password
* SourceCIDR
* TableauServerAdminPassword

Add a new parameter DomainAdminPassword and provide a value, e.g.

```
    {
        "ParameterKey": "DomainAdminPassword",
        "ParameterValue": "Test_ActiveD1re-123"
    }
```

### Run Taskcat

```
taskcat -c ci/taskcat-local.yml -n
```