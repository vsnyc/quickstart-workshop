+++
title = "Setting up CICD pipeline"
chapter = false
weight = 20
+++

### Setting up the CICD pipeline

1. Let's upload the `quickstart-autodesk-forge.zip` and the test config file  `taskcat_project_override.json` to config bucket  

    `cd ~/environment`
    
    `aws s3 cp quickstart-autodesk-forge.zip s3://$CONFIG_BUCKET/`
    
    `aws s3 cp taskcat_project_override.json s3://$CONFIG_BUCKET/`

2. In a new browser tab, open the following [launch stack link](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?stackName=Forge-App-CICD&templateURL=https://aws-cfn-samples.s3.amazonaws.com/quickstart-taskcat-ci/templates/taskcat-cicd-pipeline.template.yaml&param_ProdStackName=Forge-Prod-Stack&param_ProdStackConfig=forge-prod-codepipeline.json&param_TemplateFileName=autodesk-forge-master.json&param_TestStackConfig=taskcat_project_override.json&param_SourceRepoBranch=develop&param_ReleaseBranch=master&param_QSS3KeyPrefix=quickstart-taskcat-ci/&param_QSS3BucketName=aws-cfn-samples&param_GitHubRepoName=quickstart-autodesk-forge&param_KeepTestStack=True) that will setup your CodePipeline. Most fields are populated with defaults, fill in only the blank fields.
    * Repository owner: your GitHub user name
    * OAuth2 token: your GitHub oauth token created in Step 4
    * Email: your email address
    * ConfigBucket: your config bucket created in Step 9, this value is saved in *config-bucket.txt*
    * CodeHostingBucket: your code hosting bucket created in Step 9, this value is saved in *code-bucket.txt*
{{% notice tip %}}
The launch link above launches a slightly modified version of the [AWS CI/CD pipeline Quick Start](https://aws.amazon.com/quickstart/architecture/cicd-taskcat/). We have taken the base Quick Start and added a couple of new stages as described earlier in [CI/CD architecture] ( {{< relref "20_getting_started/3_cicd_architecture" >}}) section. You can view the [updated code](https://github.com/vsnyc/quickstart-taskcat-ci/) on GitHub.
{{% /notice %}}

3. Select both the check boxes in the Capabilities section and choose **Create Stack**. After the `Forge-App-CICD` stack is created, it will automatically execute the CodePipeline. 
![arch](/images/create-cicd-stack.png?height=60%&width=60%)