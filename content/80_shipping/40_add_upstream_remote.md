+++
title = "Add upstream remote branch"
chapter = false
weight = 40
+++


Before sending Pull Requests to the the quickstart org (upstream branch) make sure that your branch is in sync. To do so, you will add the upstream branch to your fork.

### Add Upstream

List remotes.

`git remote -v`

You should see following output.
<pre>
    origin  git@github.com:avattathil/quickstart-linux-bastion.git (fetch)
    origin  git@github.com:avattathil/quickstart-linux-bastion.git (push)
</pre>

Add upstream and fetch the commits from the remote.

`git remote add upstream git@github.com:aws-quickstart/quickstart-linux-bastion.git`

`git fetch upstream`

<pre>
From github.com:aws-quickstart/quickstart-linux-bastion
 * [new branch]......develop..........................-> upstream/develop
 * [new branch]......master...........................-> upstream/master
</pre>
