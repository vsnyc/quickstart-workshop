+++
title = "Testing locally"
chapter = false
weight = 1
+++

At this point, you have all your code built and ready to be tested. We will use TaskCat, an open source tool developed by AWS Quick Start team to simplify and automate the testing of AWS CloudFormation templates. It test the CloudFormation templates by deploying it in multiple AWS Regions simultaneously and generates a report with a pass/fail result for each region. You can customize the tests through a test config file. 

### Install Python 3

TaskCat requires python3. By default, Cloud9 workspace comes with python 2. Therefore, we will install python 3 in a virtual environment before installing TaskCat.

Run following commands, to create a virtual environment and install python 3

```
unalias python
cd ~/environment/
virtualenv -p /usr/bin/python36 vpy36
source vpy36/bin/activate
```

Run `python --version`, and you should see the output as below:

<pre>
(vpy36) Admin:~/environment $ python --version
Python 3.6.7
</pre>

### Install TaskCat

TaskCat can be installed with Docker or by using pip. We will use pip for this workshop.

From your terminal, run the following command.

`pip install taskcat`

You should see the following output.

![taskcat-install](/images/taskcat-install.gif)

Run `taskcat --version` to check TaskCat version and confirm that TaskCat is installed correctly.

### Prepare tests

TaskCat requires two files at **ci/** folder in the project directory, to run the tests. Following are the files:

1. An input parameter file in JSON format
2. A test configuration file named **taskcat.yml**

#### Input parameter file
***Input parameter file*** is a JSON file. It contains the test values for the parameters of your CloudFormation template. You can have multiple parameter files to test different deployment scenarios. This file is a list of object, each object contains two keys named - **ParameterKey** and **ParameterValue**. **ParameterKey** specifies the exact name of the parameter in the CloudFormation template and **ParameterValue** specifies the parameter value needs to be passed to the parameter. You can also auto-generate values for some parameter types such as UUIDs, Availability Zones, strings and numbers, at run time by using pre-defined tokens. For the complete list of pre-defined tokens, see the [TaskCat documentation](https://github.com/aws-quickstart/taskcat#more-information-on-taskcat-runtime-injection).

For this workshop, we have already created the input parameter file. Open **ci/workshop_input.json**, and replace the *YOUR-KEYPAIR-HERE* with your KeyPairName.

Your input parameter file looks like below. 

```
[
    {
        "ParameterKey": "AvailabilityZones",
        "ParameterValue": "$[taskcat_getaz_2]"
    },
    {
        "ParameterKey": "EmailAddress",
        "ParameterValue": "email@yourdomain.com"
    },
    {
        "ParameterKey": "KeyPairName",
        "ParameterValue": "YOUR-KEYPAIR-HERE"
    },
    {
        "ParameterKey": "RemoteAccessCIDR",
        "ParameterValue": "0.0.0.0/0"
    },
    {
        "ParameterKey": "WebserverCIDR",
        "ParameterValue": "0.0.0.0/0"
    },
    {
        "ParameterKey": "QSS3BucketName",
        "ParameterValue": "$[taskcat_autobucket]"
    }
]
```

{{%expand "BONUS Section (May be skipped)" %}}

As you can see above, there are few parameters like *KeyPairName* and *EmailAddress* which you may not want to hardcode a value and check it into the github repository. For such situations, TaskCat provide capability to override the parameter values via override files. Following are the two override files supported by TaskCat:

- **Global override file** - Place this in the **.aws** directory within your home directory 
*~/.aws/taskcat_global_override.json*
- **Project override file** - Place this in the **ci/** directory within your project directory 
*<project_name>/ci/taskcat_project_override.json*

TaskCat read parameters in the following order:

1. It will read values from the standard parameter files.
2. It will replace those with values from the global overrides file, if that file exists.
3. It will replace those with values from the project overrides file, if that file exists.

For this workshop, create a global override file and add the parameter value for the password. You file should look like below:

```
[
    {
        "ParameterKey": "EmailAddress",
        "ParameterValue": "email@yourdomain.com"
    },
    {
        "ParameterKey": "KeyPairName",
        "ParameterValue": "your-key-pair-name"
    }
]
```
{{% /expand%}}

#### TaskCat configuration file

The second file required by TaskCat is the configuration file named **taskcat.yml** in the **ci/** folder. 

<pre>
 global:
  owner: quickstart@amazon.com
  qsname: quickstart-name
  regions:
    - ap-northeast-1
    - ap-northeast-2
    - ap-south-1
    - ap-southeast-1
    - ap-southeast-2
    - ca-central-1
    - eu-central-1
    - eu-west-1
    - eu-west-2
    - sa-east-1
    - us-east-1
    - us-east-2
    - us-west-1
    - us-west-2
  reporting: true
tests:
  test-scenario1:
    parameter_input: input.json
    template_file: master.template
    regions:
    - us-east-1
  test-scenario2:
    parameter_input: input2.json
    template_file: master.template
</pre>

The **taskcat.yml** contains 2 high level mappings - *global* and *tests*. 

**global** mapping defines the global configurations of the project. It contains:

* owner - Project owner's email address
* qsname - Name of the project. Must be same as the project folder name.
* regions - All the regions where tests needs to be executed
* reporting - To generate test report with logs from each test execution

**tests** mapping defines test scenarios which will be executed by TaskCat. You can define multiple test scenarios in *test* mapping, and each test scenario must specify parameter input file name and CloudFormation template file name. Optionally, you can also define regions in which the test needs to be executed. This region list will override the global region list.

For the workshop, we have pre-created the **ci/taskcat.yml**. Open the file to evaluate its contents.It should look like following:

```
global:
  owner: owner@amazon.com
  qsname: qs-workshop
  regions:
    - ap-southeast-1
    - ap-southeast-2
    - eu-central-1
    - eu-west-1
    - us-east-1
    - us-west-1
    - us-west-2
  reporting: true
tests:
  lab-master-vpc:
    parameter_input: input.json 
    template_file: master.template.yaml
    regions:
      - us-west-2
```

### Running tests

Now that we have input parameter files and taskcat configuration file created, let's run TaskCat to execute our tests.

Run the following command in your terminal window:

`taskcat -c qs-workshop/ci/taskcat.yml`

You should see the TaskCat logs scrolling through your terminal window. TaskCat performs series of actions as part of executing a test, such as template validation, parameter validation, staging content into S3 bucket, and launching CloudFormation stack. It launches the stack creation in all the defined regions, for each test, simultaneously. And regularly polls the CloudFormation stack status to check if the stack creation is finished. How much time TaskCat takes to finish the testing, depends on how many tests you have defined in your TaskCat configuration file and how long each stack creation and deletion takes. 

After the TaskCat run is complete, you will see a report genereated in HTML format in the current directory from where you are running TaskCat command. You can see the report by opening **taskcat_outputs/index.html** file in a web browser. Your report should look like below:

![taskcat-report](/images/taskcat-report.png)

If you do not see all green, you can click on the **View Logs** link for the failed test and see the CloudFormation event logs for further troubleshooting.
