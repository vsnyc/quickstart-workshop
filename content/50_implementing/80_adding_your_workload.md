+++
title = "Adding you workload"
chapter = false
weight = 80
+++

**What is a workload template?**

The workload template contain the product specfic code. For the purpose of this lab we will create a AutoScaled web server template as the workload.

*Download the workload template*

`curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/implementing/templates/workload.template.yaml -o templates/workload.template.yaml`

**Commit changes to repo**

git add templates/workload.template.yaml

`git commit -a -m 'Added Workload'`
