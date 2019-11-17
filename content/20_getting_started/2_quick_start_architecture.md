+++
title = "AWS Quick Start Architecture"
chapter = false
weight = 20
+++

### AWS Quick Start Architecture
Here's the architecture of what we will build:

![arch](/images/autodesk-forge-on-aws-arch.png)

This architecture contains following components:

- A virtual private cloud (VPC) that spans two Availability Zones, configured with two public and two private subnets.
- In a public subnet, a bastion host to provide Secure Shell (SSH) access to the web servers. The bastion host is maintained by an Auto Scaling group that spans multiple Availability Zones, and is configured to ensure there is always one bastion host available.
- AWS-managed network address translation (NAT) gateways deployed into the public subnets and configured with an Elastic IP address for outbound internet connectivity. The NAT gateways are used for internet access for all EC2 instances launched within the private network.
- In the private subnets, Autodesk Forge application server instances across both Availability Zones, to ensure high availability.
- Auto Scaling enabled for the Autodesk Forge cluster, to automatically add or remove servers based on their use. Auto Scaling provides additional servers during peak hours and lowers costs by removing servers during off hours. This functionality is tightly integrated with the Application Load Balancer, and automatically adds and removes instances from the load balancer. The default installation sets up low and high CPU-based thresholds for scaling the instance capacity up or down. You can modify these thresholds during launch and after deployment.  
- The Elastic Load Balancing service, which provides HTTP and HTTPS load balancing across the Autodesk Forge instances. This Quick Start uses an Application Load Balancer, which is configured to use either HTTP or HTTPS. 
- An AWS Identity and Access Management (IAM) role with fine-grained permissions for access to AWS services necessary for the deployment process.  
- Appropriate security groups for each instance or function to restrict access to only necessary protocols and ports. For example, access to HTTP(S) server ports on Amazon EC2 web servers is limited to the Application Load Balancer. 
- Optionally, Amazon Route 53 as your public Domain Name System (DNS) for resolving your Forge site’s domain name. When you choose to deploy the application with a custom domain and Security Sockets Layer (SSL) certificate, a new RecordSet in your pre-existing Route 53 Hosted Zone will be created.
- AWS Systems Manager (SSM) parameters in the AWS Systems Manager Parameter Store to securely store the Forge client ID and secret.


To learn more about this, visit the [Autodesk Forge on AWS Quick Start](https://aws.amazon.com/quickstart/architecture/autodesk-forge/) and view the deployment guide.