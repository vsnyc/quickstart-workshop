+++
title = "Clone your fork localy"
chapter = false
weight = 20
+++

**Get your fork URL**

Navigate to you GitHub Home page **https://github.com/<your-gitusername>**
From the repositories tab 

![Get you Clone URL](/images/copy-web-url.png)

**Clone your fork**

Change you current working directory to the location where you want clone you fork 

{{% notice warning %}}
When cloing your fork make sure to include the **--recurse-submodules** flag
{{% /notice %}}


1. clone repo into your home directory under a folder called quickstarts

    `mkdir ~/quickstarts`
    `git clone --recurse-submodules `

![Clone your fork](/images/clone-your-fork.gif)

