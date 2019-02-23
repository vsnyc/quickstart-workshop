+++
title = "Set-up CICD for CloudFormation"
chapter = false
weight = 10
+++

Now, we will setup a CICD pipeline for our Github repo. This will ensure that any changes to the code is always tested before merge, and the master branch of the repo always contains the working code which is ready to be submitted to the original Quick Start repository. We will use the **[CI/CD pipeline for AWS CloudFormation templates](https://aws.amazon.com/quickstart/architecture/cicd-taskcat/) Quick Start** to setup the pipeline. This is an example where we are using an existing Quick Start to accomplish a task.

### Deploying pipeline

Go to [CI/CD pipeline for AWS CloudFormation templates](https://aws.amazon.com/quickstart/architecture/cicd-taskcat/) Quick Start landing page.
![lpage](/images/qs-cicd-page.png)

Select **How to deploy** tab and click **Launch the Quick Start** link.
![howto](/images/how-to-deploy.png)

It will open the AWS CloudFormation console in a new tab in your browser. Click **Next** on the **Select Template** page.
![select-template](/images/select-template.png)

On the **Specify Details** page, enter following values for the parameters:

- **Repository owner** - Your github id
- **Repository name** - `qs-workshop`
- **Source branch** - `develop`
- **Release branch** - `master`
- **OAuth2 token** - Github access token created in [Create Github token](20_github_token.html) page.

Click **Next** and **Next**.

On the **Review** page, review and confirm the template settings. Under Capabilities, select the check boxes to acknowledge that the template will create IAM resources and require additional capabilities. Then click **Create** to deploy the stack.
![cstack](/images/create-stack.gif)

It will take approximately 3-5 minutes to deploy the CICD pipeline. You can check the status of the CloudFormation stack from [CloudFormation console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2).

**Congratulations!** You have successfully setup a CICD pipeline for your Quick Start Github repo.


