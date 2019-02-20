+++
title = "Nesting Bastion Submodule"
chapter = false
weight = 60
+++

**Add QuickStart Linux Bastion as a nested stack**

Open _templates/workshop.template.yaml_ in an editor to inspect the contents of the file

In the **Resources:** section add a resource of Type **Type: 'AWS::CloudFormation::Stack'** this create a nested cloudformation 

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

{{% notice tip %}}
Close your editor and use the below command to append the above code to your template
{{% /notice %}}

**Append VPCStack to templates/workshop.template.yaml**

`curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/implementing/templates/bastionstack.master.template.yaml >>templates/workshop.template.yaml`

