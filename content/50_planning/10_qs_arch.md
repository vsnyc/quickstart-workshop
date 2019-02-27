+++
title = "Quick Start architecture"
chapter = false
weight = 10
+++

Quick Starts are built for **production** deployments. Therefore, when designing the architecture of your Quick Start, you should consider answering the following questions, before starting to write the CloudFormation templates.

- **How many Availability Zones the workload will be deployed into?**

	You should use at least two for high availability.

- **Where should your workload be placed?**

	Consider security and external access when deciding whether to install your software in a public or private subnet.

- **How many public and private subnets?**

	If your workload needs an additional level of isolation, you might consider setting up a second private subnet with network ACL protection in each Availability Zone.

- **Is your workload distributed across multiple instances?**

	If yes, use Elastic Load Balancing to help ensure availability and fault tolerance.

- **Is your workload stateless or stateful? Do you save session state in the workload instances?**

	If you don’t, your workload instance would be a good candidate for Auto Scaling.

{{% notice tip %}}
These are just some of the considerations when designing the architcture of your Quick Start. Use [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) to build secure, high-performing, resilient, and efficient infrastructure.
{{% /notice %}}