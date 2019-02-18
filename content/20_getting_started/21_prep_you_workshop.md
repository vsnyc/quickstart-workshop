+++
title = "Load workshop base"
chapter = false
weight = 21
+++

**Clone you workshop repo**

`git clone git@github.com:avattathil/qs-workshop.git`

    # git clone git@github.com:avattathil/qs-workshop.git
    Cloning into 'qs-workshop'...
    warning: You appear to have cloned an empty repository.

** Change directory to the qs-workshop repo**
`cd qs-workshop`

**Download and push base content to you repo**
`curl https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/develop/workshop-base/base.tar | tar -x`

`git commit -a -m 'Load base content'`

	[master (root-commit) ab0660b] Load base content
 	 3 files changed, 33 insertions(+)
	 create mode 100644 ci/taskcat.yml
	 create mode 100644 ci/workshop_input.json
	 create mode 100644 templates/workshop.template.yaml


**Download and push base content to the master branch**

`git push`

	Enumerating objects: 7, done.
	Counting objects: 100% (7/7), done.
	Delta compression using up to 8 threads
	Compressing objects: 100% (6/6), done.
	Writing objects: 100% (7/7), 753 bytes | 753.00 KiB/s, done.
	Total 7 (delta 0), reused 0 (delta 0)
	To github.com:avattathil/qs-workshop.git
	 * [new branch]      master -> master

**Create a develop branch and set the upstream branch**

`git checkout -b develop`

**Push develop branch**
`git push --set-upstream origin develop`

	Warning: Permanently added the RSA host key for IP address '192.30.253.113' to the list of known hosts.
	Total 0 (delta 0), reused 0 (delta 0)
	remote:
	remote: Create a pull request for 'develop' on GitHub by visiting:
	remote:      https://github.com/avattathil/qs-workshop/pull/new/develop
	remote:
	To github.com:avattathil/qs-workshop.git
	 * [new branch]      develop -> develop
	Branch 'develop' set up to track remote branch 'develop' from 'origin'.

