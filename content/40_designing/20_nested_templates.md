+++
title = "Flexible Entrypoints"
chapter = false
weight = 20
+++

#### Creating multiple entry point using nested templates

**Modularity Concept**

To cover your deployment scenarios in a modular fashion, create a master template that deploys one or many nested stacks, depending on the Quick Start. One or more of those nested stacks will deploy the actual workload of the Quick Start, while the others will be referenced as submodules (inside the your-quickstart/submodules/quickstart-imported folder in GitHub for each referenced Quick Start) at a particular commit level. This ensures that the reference is repeatable and does not change unexpectedly. The following diagram shows an example of how stacks could be linked together.


**Design your Quick Start to cover at least two entrypoint**

Building a new virtual private cloud (VPC) that contains the AWS infrastructure for the workload. This scenario enables users to set up a test, demo, or POC environment that doesn’t interfere with their production environment.
Enabling users to deploy the workload into their existing VPC. This scenario enables quick adoption by users who want to deploy the workload into their existing production environment.
You might also consider additional entry point that are specific to your architecture on AWS. For an example, see the EKS Start. Would have three entry points:

- **New VPC+EKS+Workload** - Creates a VPC then load the EKS QuickStart then the workload (master template)
- **EKS+Workload** - Loads the EKS QuickStart into an exisiting VPC then the workload 
- **Workload** - just load the workload into a exisitng EKS Cluster
