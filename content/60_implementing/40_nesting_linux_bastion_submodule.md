+++
title = "Creating Bastion Stack"
chapter = false
weight = 40
+++

Now you will add **Linux bastion** as a nested stack to your Quick Start. After you have completed the steps listed here, your Quick Start architecture will look like below.

![vpc-bastion](/images/vpc-bastion.png)

### Add QuickStart Linux Bastion as a nested stack

Open _templates/master.template.yaml_ in an editor to inspect the contents of the file. You should have only 1 resource - VPCStack.

You will add a resource of Type **‘AWS::CloudFormation::Stack’** to create second nested cloudformation stack.

Close _templates/master.template.yaml_ file and run the following command to add **Bastion Stack** resource.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/implementing/templates/bastionstack.master.template.yaml >>templates/master.template.yaml
```

Commit your changes.

` git commit -a -m 'Add QuickStart Linux Bastion as a nested stack'`

### Inspect Bastion Stack Resource

Open _templates/master.template.yaml_ in an editor and your **Resources** sections should have BastionStack resource, as shown below.

<pre>
	Resources:
	  BastionStack:
	    DependsOn: VPCStack
	    Type: AWS::CloudFormation::Stack
	    Properties:
	      TemplateURL:
	        Fn::Sub: https://${QSS3BucketName}.s3.amazonaws.com/${QSS3KeyPrefix}submodules/quickstart-linux-bastion/templates/linux-bastion.template
	      Parameters:
	        BastionAMIOS:
	          Ref: BastionAMIOS
	        BastionInstanceType:
	          Ref: BastionInstanceType
	        KeyPairName:
	          Ref: KeyPairName
	        PublicSubnet1ID:
	          Fn::GetAtt:
	          - VPCStack
	          - Outputs.PublicSubnet1ID
	        PublicSubnet2ID:
	          Fn::GetAtt:
	          - VPCStack
	          - Outputs.PublicSubnet2ID
	        QSS3BucketName:
	          Ref: QSS3BucketName
	        QSS3KeyPrefix:
	          Fn::Sub: ${QSS3KeyPrefix}submodules/quickstart-linux-bastion/
	        RemoteAccessCIDR:
	          Ref: RemoteAccessCIDR
	        VPCID:
	          Fn::GetAtt:
	          - VPCStack
	          - Outputs.VPCID
</pre>

**Great job!** You have successfully added a Linux Bastion to your Quick Start.
