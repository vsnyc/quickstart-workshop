+++
title = "Adding submodules"
chapter = false
weight = 30
+++

We will add two submodules to the qs-workshop repo (QuickStart VPC and QuickStart Linux Bastion)

**Change to the root of your repo**

`cd qs-workshop`

#### Add a VPC to your project
**Add QuickStart VPC as a submodule**

`git submodule add -b master git@github.com:aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc`

**Commit your changes and push to the develop branch**

`git commit -a -m "Add QuickStart VPC Submodule"`

#### Add Linux Bastion to your project
**Add QuickStart Linux Bastion as a submodule**

`git submodule add -b master git@github.com:aws-quickstart/quickstart-linux-bastion.git submodules/quickstart-linux-bastion`

**Commit your changes and push to the develop branch**

`git commit -a -m "Add QuickStart Linux Bastion Submodule"`

{{% notice tip %}}
If you need to update your submodules later you can use the following command  `git sddubmodule update --recursive`
{{% /notice %}}


