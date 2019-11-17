+++
title = "CI/CD Pipeline Architecture"
chapter = false
weight = 30
+++

### CI/CD Pipeline Architecture
Here's the architecture of the CodePipeline we will build:

![arch](/images/forge-cicd-taskcat-pipeline.png)

This architecture contains following components:

- **Source stage**: The Source stage consists of your Forge Quick Start code located in a GitHub repository and the configuration files you'll need to run your test and production stacks stored securely in Amazon S3.  
- **Test build stage**: In the event of a source change (code is committed to GitHub  or a configuration update is pushed to Amazon S3), a trigger will start the AWS CodePipeline build process, pulling the code from these locations and running a build using AWS CodeBuild. The test CodeBuild project invokes TaskCat to test your source modifications. If the tests are successful, we move on to the next stage.
- **Git merge stage**: After the tests pass, we use a custom action using AWS Lambda to merge the development branch to the master branch
- **Sync to S3 stage**: To run the updated code in production, we create a CodeBuild job that takes the updated master branch and recursively copies the GitHub repository contents to your bucket in Amazon S3 that holds the production templates.
- **Prod stage**: After the new code has synced to Amazon S3, the pipeline invokes the CloudFormation deployment stage. In this stage, we first create a change set that an administrator could review to understand what changes are included in the deployment. And then after an administrator manually approves the change, the deployment will proceed. 

At the end, when the pipeline execution is successful, you will see your change in GitHub deployed to production automatically with just one manual step that requires you to choose Approve action before the final deployment.

To learn more about this, visit the [Forge community blog](https://forge.autodesk.com/blog/guest-blog-continuous-delivery-how-easily-take-your-forge-application-development-production).