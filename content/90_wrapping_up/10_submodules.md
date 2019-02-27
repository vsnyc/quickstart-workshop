+++
title = "Designing with submodules"
chapter = false
weight = 10
+++

**What is a Git submodule?**

Submodules allow you to keep a Git repository as a subdirectory of another Git repository.  More info [here](https://git-scm.com/book/en/v2/Git-Tools-Submodules)


**Why do we use submodules?**

Depending on your use case you may have multiple submodule in your reference like __QuickStart VPC__ or __QuickStart Linux Bastion__. By leveraging submodules you can include a stable snapshot of any QuickStart without having to copy the code into you repo. 

As a added benifit the QuickStart CI process will automatically keep your submodule updated. After all integration test passed our CI will push a commit to update the submodule then run through the integration test again to make sure the updates were compatible. 

In the lab to follow we will walk through how to use _submodule_ in conjunction with _cloudformation nesting_
