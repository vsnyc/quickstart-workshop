+++
title = "Planning Quick Start deployment"
chapter = false
weight = 1
+++

1. Clone git repo in Cloud9 IDE using the following command in your terminal, replacing GITHUB_USERNAME with your GitHub user name:
    `git clone --recursive https://github.com/YOUR_GITHUB_USERNAME/quickstart-autodesk-forge.git`
    
    When asked for a user name and password, use your `GITHUB_USERNAME` and `GITHUB_TOKEN` that you created earlier.
    Now you have the Quick Start code downloaded to your IDE so you can make any changes.
    ![arch](/images/clone-quick-start.png)
2. To deploy the Quick Start and the CodePipeline, we need to prepare the following.
   1. Two Amazon S3 buckets: one located in your deployment AWS Region (US West (Oregon)) that will host your configuration parameters; and one located in US East (N. Virginia) that will host your Quick Start production code.
   2. CloudFormation input configuration parameters for your Forge production stack, the formats differ slightly when the deployment is done directly using AWS CloudFormation vs. when triggered using AWS CodePipeline, so we'll prepare two versions of the file.
   3. CloudFormation input configuration parameters for your test stack. The Quick Start comes with sensible defaults, so we only need to add a select few properties such as Forge secrets as a override.
   4. Two key pairs, one in US West (Oregon) for production stack and one in US West (N. California) for test stack. We had to split the production and test stacks in two regions to accommodate the fact that new AWS accounts only have 5 Elastic IPs by default.
   5. The Client ID and Secret of your Forge app.
3. To help build the above required setup, we have prepared a workshop assets bundle you can use to avoid manual steps. Feel free to look into the scripts to understand how we have automated the simple tasks.
4. Download workshop assets. This will be located at the Root level of the project together with the quickstart-autodesk-forge folder.
    ```bash
    cd ~/environment
    curl -O https://aws-cfn-samples.s3.amazonaws.com/forge-workshop/forge-workshop-assets.zip
    ```
5. Unzip workshop assets.
    ```bash
    unzip forge-workshop-assets.zip
    ```
6. Let's take a look at the extracted files, but do not edit them yet.

       Name     | Description
       ---------|------
       forge-prod-cfn.json | Input parameter file to create your production stack using AWS CloudFormation. It contains a few tokens; e.g., `YOUR_EMAIL`, `YOUR_FORGE_CLIENT_ID`, etc. that need to be replaced.
       forge-prod-codepipeline.json | Input parameter file to create/update your production stack using AWS CodePipeline. It contains a few tokens; e.g., `YOUR_EMAIL`, `YOUR_FORGE_CLIENT_ID`, etc. that need to be replaced.
       taskcat_project_override.json | Input parameter file containing overrides for testing. It contains a few tokens; e.g., `YOUR_EMAIL`, `YOUR_FORGE_CLIENT_ID`, etc. that need to be replaced.    
       make_buckets_key_pairs.sh | A script that creates two S3 buckets and two key pairs as explained in Step 2.
       update_artifacts.sh | A script that replaces the tokens in the 3 json input files with values that you provide and then prepares a zip file to be used by CodePipeline as a source.
       run_cfn.sh | A helper script to create your production stack. It contains a single `aws cloudformation create-stack` command and is provided as a simple wrapper for an otherwise long command.

7. Let's run the following command to make the buckets and key pairs.       
   ```bash
   bash make_buckets_key_pairs.sh
   ```
   Sample output:
   ```text
    make_bucket: au-demo-config-5ac3c715-5857
    Created config bucket: au-demo-config-5ac3c715-5857
    make_bucket: au-demo-code-5ac3c715-5857
    Created code hosting bucket: au-demo-code-5ac3c715-5857
    Created forge-demo key pair in us-west-1 and us-west-2
    ```
8. The names of the created buckets are saved to file system as `config-bucket.txt` and `code-bucket.txt` for future reference. We'll need them again in Section 3, Step 3. Export the config bucket to an environment variable for convenience.  
       `export CONFIG_BUCKET=$(cat config-bucket.txt)`   
9. Echo the environment variable to verify it got saved correctly.
        `echo $CONFIG_BUCKET`      
10. Open update_artifacts.sh and fill lines 1-4 as follows. Be sure to not add any spaces after the properties: `EMAIL`, `FORGE_CLIENT_ID`, etc.
      
       Property | Value
       ---------|------
       EMAIL    | Any valid email address that you own. This will be used to send EC2 Auto Scaling and CodePipeline action notifications
       FORGE_CLIENT_ID  | The Forge client ID of your pre-existing Forge application
       FORGE_CLIENT_SECRET | The Forge client secret of your pre-existing Forge application
       IP_ADDRESS | You can either update it with your IP address (check at http://checkip.amazonaws.com/, e.g. "1.2.3.4\\/32") or with "0.0.0.0\\/0" to allow access from anywhere. Note the backslash for IP address value, it is required to escape it during substitution.
11. Now let's execute the following command to use the updated input values and generate a zip file containing configuration needed for our CodePipeline that we'll be creating in a few minutes.

    `bash update_artifacts.sh`       
12. Let's verify the substituted tokens in `forge-prod-cfn.json`, `forge-prod-codepipeline.json`, and `taskcat_project_override.json`.    