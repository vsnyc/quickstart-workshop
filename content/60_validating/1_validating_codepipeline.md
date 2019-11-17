+++
title = "Validating CI/CD pipeline"
chapter = false
weight = 1
+++

### Deployment options

1. Once the Forge-App-CICD stack reaches *CREATE_COMPLETE* status, go to the *CodePipelineURL* in the Outputs section.
![arch](/images/cicd-stack-complete.png?height=60%&width=60%)
2. The CodePipeline will sequentially execute each of the stages: *Source*, *Test build*, *Git merge*, *Sync to S3*, *Prod* we had talked about earlier.  
![arch](/images/build-stage-progress.png?height=60%&width=60%)
3. While the *Test build* stage is in progress, you can go to CloudFormation console in US West (N. California) Region to verify a test stack is being created. 
![arch](/images/test-stack-progress.png?height=60%&width=60%)
4. It takes about 25 minutes for the pipeline to reach the PROD stage. When it reaches there it will wait for a manual approval to proceed. 
![arch](/images/prod-approval-wait.png)
5. Choose **Review** and then type in a description for the changes and choose **Approve**
![arch](/images/prod-stack-approve.png)