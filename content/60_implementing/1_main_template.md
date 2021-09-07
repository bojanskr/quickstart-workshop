+++
title = "Building main template"
chapter = false
weight = 1
+++

{{% notice info %}}
The following instruction must be performed from within your workshop repo **qs-workshop**
{{% /notice %}}

### Deployment options
Each Quick Start should allow users to deploy the workload into an existing VPC and in a new VPC which is created as part of the Quick Start. Which means, you need to provide two deployment options to cover both the scenarios:

1. Building a new virtual private cloud (VPC) that contains the AWS infrastructure for the workload. This scenario enables users to set up a test, demo, or POC environment that doesn’t interfere with their production environment.
2. Deploying the workload into an existing VPC. This scenario enables quick adoption by users who want to deploy the workload into their existing production environment.

### Modularity

To cover both the above scenarios, we will structure our templates in a modular fashion, as shown below.
![main-template](/images/main-template.png?width=60%&height=60%)

**main.template** is the entry point to deploy the Quick Start into a new VPC. It creates a VPC, and the workload, as nested stacks.

**workload.template** is the entry point to deploy the workload into an existing VPC.

To deploy the Quick Start into a new VPC, user will launch **main.template**. And to deploy Quick Start into an already existing VPC, user will launch **workload.template**. Workload template will require VPC information to be passed in as parameters.

### Build main template
Let's create the main templete now.

Main template will create one or many nested stacks, depending upon the Quick Start architecture. 

For this workshop's Quick Start architecture, main template will create two nested stacks - VPC stack, and a workload stack, as shown in the image above.

Create the main template by creating a file called `main.template.yaml` in **templates/** directory, copy the below contents into the file, and save.

```
---
AWSTemplateFormatVersion: 2010-09-09

Description:
  This template creates the VPC and workload as nested stacks.

Parameters:
  set of parameters

Mappings:
  set of mappings

Conditions:
  set of conditions

Resources:
  set of resources

Outputs:
  set of outputs
```

Right now the **main.template.yaml** is incomplete. It doesn't do much at this point. You will be filling in different sections of the templates as you follow along rest of the workshop.