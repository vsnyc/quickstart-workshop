+++
title = "4. Create Github Token"
chapter = false
weight = 30
+++

{{% notice warning %}}
You must have a GitHub account for this workshop. If you do not have an account create one by following these instructions [Signing up for a new GitHub Account](https://help.github.com/articles/signing-up-for-a-new-github-account/){{% /notice %}}

You need Github personal access token which will be used to create CICD pipeline for your CloudFormation templates.

Follow the steps below to create a token:

1. Verify your email address, if it hasn't been verified yet.
2. In the upper-right corner of any page, click your profile photo, then click **Settings**.
![Settings](/images/github-settings.png)
3. In the left sidebar, click **Developer settings**.
![Developer Settings](/images/github-devsettings.png)
4. In the left sidebar, click **Personal access tokens**.
![Personal access](/images/github-personal-access.png)
5. Click **Generate new token**.
![Generate](/images/github-generate-token.png)
6. Give your token a descriptive name.
7. Select the scopes, or permissions, you'd like to grant this token. For this workshop, select **repo** and **admin:repo_hook**.
![Scope](/images/github-token-scope.gif)
8. Click **Generate token**.
![Generate token](/images/github-generate.png)
9. Copy the token to your clipboard and save it securely. For security reasons, after you navigate off the page, you will not be able to see the token again.
![Copy](/images/github-copy-token.png)

{{% notice warning %}}
Treat your tokens like passwords and keep them secret.
{{% /notice %}}
