+++
title = "Clone your fork"
chapter = false
weight = 30
+++

### Get your fork URL

1. Navigate to you GitHub Home page **https://github.com/YOUR_GIT_USERNAME_HERE/**

2. Copy you forks url path

![Get you Clone URL](/images/copy-web-url.png)


### Clone your fork

{{% notice warning %}}
When cloing your fork make sure to include the **--recurse-submodules** flag
{{% /notice %}}

Change you current working directory to the location where you want to clone you fork. For this workshop, create a **quickstarts** directory in your home directory.

`mkdir ~/quickstarts`

Clone the repo

`git clone --recurse-submodules YOUR-FORK-URL`

![Clone your fork](/images/clone-your-fork.gif)

