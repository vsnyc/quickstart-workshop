+++
title = "Testing through CICD pipeline"
chapter = false
weight = 10
+++

Another option for testing your CloudFormation templates is through the CICD pipeline we have [setup earlier](../20_getting_started/30_setup_cicd.html) in the workshop. 

With CICD pipeline, you can push your code to the develop branch of your repository, which will automatically trigger the test execution. You can stop your workspace and come back later to see the test results. You don't have to actively monitor the tests and keep your terminal session open for TaskCat to run your tests.

### Push code

First, commit your changes locally by running the following commands:

```
git add .
git commit -m "some meaningful message"
```

Now, push your changes to the develop branch of your github repository, by running the following command:

`git push origin develop`

It will trigger the code pipeline to start building and testing your code changes.

### View test run

You can see the progress and result of the test through AWS CodePipeline console.

Go to AWS [CloudFormation console](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2), and select the region where you created the CICD pipeline from the top right corner. You should see the CloudFormation stack for your CICD pipeline, as shown below.

![cfn-stack](/images/cicd-cfnstack.png)

Select the main stack checkbox, and in the window below it, under **Outputs** tab, click the link of **CodePipelieURL**.

![pipeline-url](/images/cicd-pipeline-url.png)

You should see the CICD pipeline, as shown below. You will also notice that, the pipeline has been triggered by your code push and the **Build** process is either completed or in-progress.

![cicd-pipeline](/images/cicd-pipeline.png)

After the test is completed successfully, the *develop* branch or your git repository will be merged into the *master* branch, and the pipeline will look like below.

![cicd-success](/images/cicd-success.png)

### View test logs

To see the test logs, click **Details** under **Code Build**, and scroll down to **Build logs** section, as shown below.

![cicd-logs](/images/cicd-logs.gif)
