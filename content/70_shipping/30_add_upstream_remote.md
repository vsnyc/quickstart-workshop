+++
title = "Adding upstream remote branch"
chapter = false
weight = 30
+++


**Adding upstream branch**

Before sending Pull Requests to the the quickstart org (upstream branch) make sure that you branch is in sync.

**List remotes**

`git remote -v`

    origin  https://github.com/avattathil/quickstart-linux-bastion (fetch)
    origin  https://github.com/avattathil/quickstart-linux-bastion (push)

**Add upstream and fetch**

`git fetch upstream`

    From https://github.com/aws-quickstart/quickstart-linux-bastion
     * [new branch]      develop                                 -> upstream/develop
     * [new branch]      master                                  -> upstream/master

