+++
title = "Deploy Quick Start"
chapter = false
weight = 10
+++

1. Deploy the Quick Start with the default Forge application by running the command below. This will create a new CloudFormation stack in your account with the name: *Forge-Prod-Stack*.
  
    ```bash
    bash run_cfn.sh
    ```    
   The *run_cfn.sh* bash script contains a single AWS CLI command to create a CloudFormation stack.
   
       <pre>
        aws cloudformation --region us-west-2 create-stack --stack-name Forge-Prod-Stack \
          --template-url https://aws-cfn-samples.s3.amazonaws.com/quickstart-autodesk-forge/templates/autodesk-forge-master.json \
          --parameters file://forge-prod-cfn.json \
          --capabilities "CAPABILITY_IAM" --disable-rollback
        </pre>
   
    
2. This step will take approximately 15 minutes, we'll come back and verify that our base application has deployed correctly. To test your application, go to the CloudFormation console and choose the `Forge-Prod-Stack`. In the Outputs section, go to the link provided as the value of `ForgeAppURL`.
![arch](/images/prod-stack-complete.png?height=60%&width=60%)
3. Going to the *ForgeAppURL*, you can verify the default application. The view will differ based on what is stored in your buckets.
![arch](/images/default-app-view.png?height=60%&width=60%)