+++
title = "What We'll Build"
chapter = false
weight = 10
+++

### Our Goal
In this workshop, we will learn:

- Setting-up source control for Quick Start artifacts
- Setting-up a development environment to build Quick Start
- Setting-up CICD pipeline to continuously build and test code changes to the Quick Start
- Designing Quick Start architecture following AWS best practices
- Writing templates for maintainability, flexibility and re-usability
- Testing templates in multiple regions with different input parameters using single command
- Packaging and submitting the Quick Start for review and publishing

### Architecture
Here's the architecture of what we will build:

![arch](/images/architecture.png)

This architecture contains following components:

- A virtual private cloud (VPC) that spans two Availability Zones, configured with two public and two private subnets.
- AWS-managed network address translation (NAT) gateways deployed into the public subnets and configured with an Elastic IP address for outbound internet connectivity. The NAT gateways are used for internet access for all EC2 instances launched within the private network.
- Amazon EC2 web server instances launched in the private subnets, with auto-scaling group enabled to automatically increase capacity if there is a demand spike, and to reduce capacity during low traffic times.
- Elastic Load Balancing deployed to automatically distribute traffic across the multiple web server instances.
- An AWS Identity and Access Management (IAM) instance role with fine-grained permissions for accessing AWS services necessary for the deployment process.
- Appropriate security groups for each instance to restrict access to only necessary protocols and ports. For example, access to HTTP server ports on Amazon EC2 web servers is limited to Elastic Load Balancing.

If above architecture looks too complex, don't worry. We will walk you through step-by-step, build it iteratively - one component at a time, and use existing resources to avoid re-creating what's already built.