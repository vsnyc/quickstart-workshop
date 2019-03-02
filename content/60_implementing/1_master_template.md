+++
title = "Building master template"
chapter = false
weight = 1
+++

{{% notice info %}}
The following instruction must be performed from within your workshop repo **qs-workshop**
{{% /notice %}}

### Deployment options
Each Quick Start should allow users to deploy the workload into an existing VPC or in a new VPC which is created as part of the Quick Start.
Which means, we need to provide two deployment options to cover both the scenarios:

1. Building a new virtual private cloud (VPC) that contains the AWS infrastructure for the workload. This scenario enables users to set up a test, demo, or POC environment that doesn’t interfere with their production environment.
2. Deploying the workload into an existing VPC. This scenario enables quick adoption by users who want to deploy the workload into their existing production environment.

### Build master template
We are now ready to create a master templete. Master template will be the entrypoint to deploy the Quick Start into a new VPC, covering scenario 1 mentioned above.
Master template will create one or many nested stacks, depending upon the Quick Start architecture. 

For this workshop Quick Start, master template will create two nested stacks - a VPC stack and a workload stack, as shown in the image below.
![master-template](/images/master-template.png?width=60%&height=60%)

Let's create the master template by creating a file called `master.template.yaml`, copy the below contents into the file, and save.

```
---
AWSTemplateFormatVersion: 2010-09-09

Description:
  This template creates the VPC and workload as nested stacks.

Parameters:
  set of parameters

Mappings:
  set of mappings

Conditions:
  set of conditions

Resources:
  set of resources

Outputs:
  set of outputs
```

Right now the **master.template.yaml** is incomplete. It doesn't do much at this point. You will be filling in different sections of the templates as you follow rest of the workshop.