+++
title = "Creating a keypair"
chapter = false
weight = 10
+++

**Create an Amazon EC2 key pair**

- Signin to your AWS account [Sign In to the Console](https://console.aws.amazon.com/)
- We will be working in the **eu-central-1** EU (Frankfurt) Region for this workshop, choose **EU (Frankfurt)** from the upper right of the console. If you encounter any permission-related errors as you go through the lab, verify that you are in the **EU (Frankfurt)** Region.
- Go to the **EC2** console by searching or choosing it from the list of AWS services.
- In the EC2 console, choose **Key Pairs** from the left pane.
- Choose **Create Key Pair**. 
- Name you keypair **qsworkshop** (You can delete this keypair once you finsh your labs)
- Save the private key `.pem` file locally to a place you can refer to later, as needed. (for example ~/qsworkshop.pem)
- Change your current working dir to where you stored your .pem file (for example cd ~)

**Reduce the permission on your .pem file so only the root user can read it**

`chmod 400 qsworkshop.pem`

For more information on Amazon EC2 Key Pairs, see the [Amazon EC2 documentation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html).

