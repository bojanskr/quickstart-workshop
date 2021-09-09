+++
title = "What We'll Build"
chapter = false
weight = 10
+++

### Our Goal
In this workshop, we will learn:

- Anatomy of the CloudFormation template
- Basics of CloudFormation template:
    - Creating AWS Resources such as EC2 instances, Elastic Load Balancer, etc.
    - Making CloudFormation template customizable using Parameters
    - Providing AWS resource information to users using Outputs
- Advance concepts of CloudFormation:
    - Making CloudFormation template dynamic using Mappings
    - Creating AWS resources when certain condition is True, using Conditions
    - Avoiding stack failure by validating parameter values, using Rules
    - Re-using existing templates, via Nested Stacks
- Testing templates in multiple regions with different input parameters using Taskcat
- Performing static analysis of the templates

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