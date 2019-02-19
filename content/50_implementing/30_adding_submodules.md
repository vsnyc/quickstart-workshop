+++
title = "Working with submodules"
chapter = false
weight = 30
+++

**Change to the root of your repo**

`cd qs-workshop`

**Add QuicStart VPC as submodule to your repo**

`git submodule add -b master git@github.com:aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc`

**Commit your changes and push to the develop branch**

`git commit -a -m "Add QuicStart VPC Submodule"`

`git push`

**Your branch should now contain the following**

    ├── ci
    │   ├── taskcat.yml
    │   └── workshop_input.json
    ├── submodules
    │   └── quickstart-aws-vpc
    │       ├── LICENSE.txt
    │       ├── NOTICE.txt
    │       ├── README.md
    │       ├── ci
    │       │   ├── aws-vpc-3az-complete.json
    │       │   ├── aws-vpc-3az-public.json
    │       │   ├── aws-vpc-3az.json
    │       │   ├── aws-vpc-4az-complete.json
    │       │   ├── aws-vpc-4az-public.json
    │       │   ├── aws-vpc-4az.json
    │       │   ├── aws-vpc-complete.json
    │       │   ├── aws-vpc-dedicated.json
    │       │   ├── aws-vpc-defaults.json
    │       │   ├── aws-vpc-public.json
    │       │   ├── aws-vpc-sa-east-1.json
    │       │   └── taskcat.yml
    │       └── templates
    │           └── aws-vpc.template
    └── templates
        └── workshop.template.yaml

{{% notice tip %}}
If you need to update your submodules later you can use the following command  `git sddubmodule update --recursive`
{{% /notice %}}


