+++
title = "Creating VPC entrypoint"
chapter = false
weight = 40
+++

Lets start by pulling down a stub template. This template will serve as a starting point. We can then add the required code to build out a VPCStack as a nested template

**Download the stub template and overwrite workshop.template.yaml file**

`curl https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/implementing/templates/incomplete.master.template.yaml -o templates/workshop.template.yaml`

The stub template provides a pre populated Parameters section containing the following:

{{% notice tip %}}
Any parameter below that does not have a **Default** value **(Requires Input)** during launch
We will pass these values via the taskcat input file which will be covered in the testing section of this workshop
{{% /notice %}}

**Parameters required by the QuickStart VPC**

| Parameter Key | Description | Default Value|
| ------------- | ----------- | ------------ |
|AvailabilityZones| List of Availability Zones | Requires Input|
|KeyPairName| The name of an existing public/private key pair| Requires Input |
|PrivateSubnet1CIDR| CIDR block for private subnet 1 located in Availability Zone 1 |10.0.0.0/19|
|PrivateSubnet2CIDR| CIDR block for private subnet 2 located in Availability Zone 2 |10.0.32.0/19|
|PublicSubnet1CIDR| CIDR block for the public (DMZ) subnet 1 located in Availability Zone 1 |10.0.128.0/20|
|PublicSubnet2CIDR| CIDR block for the public (DMZ) subnet 2 located in Availability Zone 2|10.0.144.0/20|
|VPCCIDR| CIDR block for the VPC|10.0.0.0/16|

**QuickStart Portability Parameters**

{{% notice tip %}}
These parameters allow you to host assets in you own s3 bucket.
In the testing section we will cover how we use these parameters in conjunction with __taskcat overrides__ to test these templates in auto generated buckets
{{% /notice %}}

| Parameter Key | Description | Default Value|
| ------------- | ----------- | ------------ |
|QSS3BucketName|S3 bucket name for the Quick Start assets|aws-quickstart|
|QSS3KeyPrefix| S3 key prefix for the Quick Start assets. Should end with(/)| implementing/

