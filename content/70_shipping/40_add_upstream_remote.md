+++
title = "Adding upstream remote branch"
chapter = false
weight = 40
+++


**Adding upstream branch**

Before sending Pull Requests to the the quickstart org (upstream branch) make sure that you branch is in sync.

**List remotes**

`git remote -v`

    origin  git@github.com:avattathil/quickstart-linux-bastion.git (fetch)
    origin  git@github.com:avattathil/quickstart-linux-bastion.git (push)

**Add upstream and fetch**

`git remote add upstream https://github.com/aws-quickstart/quickstart-linux-bastion`
`git fetch upstream`

    From github.com:aws-quickstart/quickstart-linux-bastion
     * [new branch]      develop                                 -> upstream/develop
     * [new branch]      master                                  -> upstream/master

