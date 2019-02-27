+++
title = "Nesting VPC Submodule"
chapter = false
weight = 50
+++

**Add QuickStart VPC as a nested stack**

Open _templates/workshop.template.yaml_ in an editor to inspect the contents of the file

In the **Resources:** section add a resource of Type **Type: 'AWS::CloudFormation::Stack'** this create a nested cloudformation 

<pre>
    Resources:
      VPCStack:
        Type: 'AWS::CloudFormation::Stack'
        Properties:
          TemplateURL: !Sub >-
            https://${QSS3BucketName}.s3.amazonaws.com/${QSS3KeyPrefix}submodules/quickstart-aws-vpc/templates/aws-vpc.template
          Parameters:
            AvailabilityZones: !Join
              - ','
              - !Ref AvailabilityZones
            KeyPairName: !Ref KeyPairName
            NumberOfAZs: '2'
            PrivateSubnet1ACIDR: !Ref PrivateSubnet1CIDR
            PrivateSubnet2ACIDR: !Ref PrivateSubnet2CIDR
            PublicSubnet1CIDR: !Ref PublicSubnet1CIDR
            PublicSubnet2CIDR: !Ref PublicSubnet2CIDR
            VPCCIDR: !Ref VPCCIDR
</pre>

{{% notice tip %}}
Close your editor and use the below command to append the above code to your template
{{% /notice %}}

**Append VPCStack to templates/workshop.template.yaml**

`curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/implementing/templates/vpcstack.master.template.yaml >>templates/workshop.template.yaml`

**Commit changes to master template**

` git commit -a -m 'Add QuickStart VPC as a nested stack'`

