+++
title = "Cleanup"
chapter = false
weight = 1
+++

{{% notice tip %}}
**If you are doing this as part of a workshop using the Event Engine, you can skip this page.**
{{% /notice %}}

### Clean up steps

{{% notice warning %}}
The order below is important to remove resources cleanly.
{{% /notice %}}

1. Go to AWS CloudFormation console in US West (N. California) Region and delete the root (non-nested) stack that starts with the name *tcat-tag-forge-*. We had setup the CI/CD pipeline to not auto-delete the test stack to save testing time.
2. Go to AWS CloudFormation console in US West (Oregon) Region and first delete the *Forge-Prod-Stack*
3. Once *Forge-Prod-Stack* is deleted, delete the *Forge-App-CICD* stack.
4. Go to Amazon S3 console and delete the code and config buckets, you can search for `au-demo` to list the buckets. You can also get the full bucket names from the files: *code-bucket.txt* and *config-bucket.txt*.
5. Go to AWS Cloud9 console and delete the Cloud9 workspace you created.