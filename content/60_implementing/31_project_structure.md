+++
title = "Verify Project Structure"
chapter = false
weight = 31
+++

**Your _develop_ branch should now contain the following:**

<pre>
    ├── ci
    │   ├── taskcat.yml
    │   └── workshop_input.json
    ├── submodules
    │   ├── quickstart-aws-vpc
    │   │   ├── LICENSE.txt
    │   │   ├── NOTICE.txt
    │   │   ├── README.md
    │   │   ├── ci
    │   │   │   ├── (test input files ...)
    │   │   │   └── taskcat.yml
    │   │   └── templates
    │   │       └── aws-vpc.template
    │   └── quickstart-linux-bastion
    │       ├── LICENSE.txt
    │       ├── NOTICE.txt
    │       ├── README.md
    │       ├── ci
    │       │   ├── (test input files ...)
    │       │   └── taskcat.yml
    │       ├── scripts
    │       │   ├── banner_message.txt
    │       │   └── bastion_bootstrap.sh
    │       ├── submodules
    │       │   └── quickstart-aws-vpc
    │       └── templates
    │           ├── linux-bastion-master.template
    │           └── linux-bastion.template
    └── templates
        └── workshop.template.yaml
</pre>

**Push your submodules to the develop branch**

`git push`

<pre>
    Enumerating objects: 13, done.
    Counting objects: 100% (13/13), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (8/8), done.
    Writing objects: 100% (8/8), 1.86 KiB | 635.00 KiB/s, done.
    Total 8 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    To github.com:avattathil/qs-workshop.git
       3fe60df..acdba90  develop -> develop
</pre>
