+++
title = "Creating a feature branch"
chapter = false
weight = 50
+++


**Feature branch**

Setup your wip or feature branch to track the **upstream/develop**
This will make it easier the ensure your PR is mergeable

**Create a branch for your updates and feature adds" 

`git checkout -b feature/something -t upstream/develop`

	Branch 'feature/something' set up to track remote branch 'develop' from 'upstream'.
	Switched to a new branch 'feature/something'

{{% notice tip %}}
Try to Name your branch based of the work you are doing for example:
**fix/broken-script-path**  or **update/update-amis**
{{% /notice %}}

