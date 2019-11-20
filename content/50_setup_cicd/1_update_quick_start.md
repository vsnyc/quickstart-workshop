+++
title = "Updating the Quick Start"
chapter = false
weight = 10
+++

### Updating the Quick Start

We will now update our app and setup a CodePipeline to deploy our changes automatically. We'll replace the default app with an app that displays a dashboard for the models. In the Cloud9 IDE:

1. In terminal, go to the repo directory: `cd quickstart-autodesk-forge`
2. Checkout develop branch: `git checkout develop`
3. open `templates/autodesk-forge-nodejs.json`. Change the value of *FORGE_APP_NAME* in line 147 from `forge-viewmodels-nodejs-aws` to `forge-viewmodels-nodejs-aws-dashboard`. Save the file.
4. open `templates/autodesk-forge.json`. Change `Toggle` value in line 801 from "false" to "true". Save the file.
5. In terminal, from the quickstart-autodesk-forge directory, add the files, commit and push. When asked for a password, use your GitHub personal access token created earlier (see [Create GitHub token] ( {{< relref "10_prerequisites/30_github_token" >}})).
           
    ```bash
    git add -A
    git commit -m "Updated app to include a dashboard"
    git push
    ```