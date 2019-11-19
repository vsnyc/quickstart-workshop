+++
title = "Setup Git CLI"
chapter = false
weight = 40
+++

Through out this workshop, you will run GitHub commands from your Cloud9 workspace terminal window, to perform different operations on your GitHub repo.

By default, Cloud9 workspace comes installed with Git CLI. However, you need to configure it to use with your GitHub account.

### Configure Git Profile

In the terminal, run these two commands, one at a time, substituting your Git name and email address for USER_NAME and EMAIL_ADDRESS, respectively.

`cd ~/environment`

`git config --global user.name "USER_NAME"`

`git config --global user.email "EMAIL_ADDRESS"`

### Configure Git Credentials

There are 2 ways you can connect to your GitHub repository from the terminal - SSH and HTTPS. Using an HTTPS remote URL has some advantages: it's easier to set up than SSH, and usually works through strict firewalls and proxies. However, it also prompts you to enter your GitHub credentials every time you pull or push a repository.

You can setup an SSH connection to GitHub, by following the [GitHub documentation](https://help.github.com/en/articles/connecting-to-github-with-ssh). However, for this workshop we will use HTTPS connection. 

To avoid prompts to enter your GitHub credentials every time you pull or push a repository, you will configure password caching.

Turn on the credential helper so that Git will save your password in memory for some time. By default, Git will cache your password for 15 minutes.

In terminal, , enter the following:

`git config --global credential.helper cache`

To change the default password cache timeout from 15 mins to 1 hr, enter the following:

`git config --global credential.helper 'cache --timeout=3600'`