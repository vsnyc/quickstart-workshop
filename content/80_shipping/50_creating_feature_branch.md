+++
title = "Create a feature branch"
chapter = false
weight = 50
+++

It's recommended that any changes you do, you do it on a feature branch. This feature branch should track the **upstream/develop** to make it easier to ensure that your PR is mergeable.

Create a feature branch and tracking *upstream/develop*

`git checkout -b feature/something -t upstream/develop`

Your output should look like below.

<pre>
Branch 'feature/something' set up to track remote branch 'develop' from 'upstream'.
Switched to a new branch 'feature/something'
</pre>

{{% notice tip %}}
Try to Name your branch based of the work you are doing for example:
**fix/broken-script-path**  or **update/update-amis**
{{% /notice %}}

