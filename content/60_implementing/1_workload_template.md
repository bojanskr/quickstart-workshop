+++
title = "Building Workload template"
chapter = false
weight = 1
+++

{{% notice info %}}
The following instruction must be performed from within your workshop repo **workshop**
{{% /notice %}}

### Workload stack

The term **workload** here is used to represent the CloudFormation stack which consists of all the resources that is core to the solution you want to deploy.

In this workshop, **a multi-az auto-scaled Apache web server deployed across 2 AZs, along with Elastic load balancer (ELB)** is referred as workload, as shown in the image below.

{{< figure src="/images/workload.png" title="Image 1: Workload" >}}

#### Template anatomy

A template is a JSON- or YAML-formatted text file that describes your AWS infrastructure. Through out this workshop you will create template in YAML, as its more readable than JSON and allows adding code comments.

Let's start with creating the workload template.

Create a file called `workload.template.yaml` in **templates/** directory, copy the below contents into the file, and save.

```yaml
---
#The AWS CloudFormation template version that the template conforms to. The template format version isn't the same as the API or WSDL version. The template format version can change independently of the API and WSDL versions.
AWSTemplateFormatVersion: 2010-09-09

Description:
  #A text string that describes the template. This section must always follow the template format version section.
  This template creates the workload stack.

Metadata:
  #Objects that provide additional information about the template.
  template metadata

Parameters:
  #Values to pass to your template at runtime (when you create or update a stack). You can refer to parameters from the Resources and Outputs sections of the template.
  set of parameters

Rules:
  #Validates a parameter or a combination of parameters passed to a template during a stack creation or stack update.
  set of rules

Mappings:
  #A mapping of keys and associated values that you can use to specify conditional parameter values, similar to a lookup table. You can match a key to a corresponding value by using the Fn::FindInMap intrinsic function in the Resources and Outputs sections.
  set of mappings

Conditions:
  #Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment.
  set of conditions

Resources:
  #Specifies the stack resources and their properties, such as an Amazon Elastic Compute Cloud instance or an Amazon Simple Storage Service bucket. You can refer to resources in the Resources and Outputs sections of the template.
  set of resources

Outputs:
  #Describes the values that are returned whenever you view your stack's properties.
  set of outputs
```

The above examples show an AWS CloudFormation template structure and its sections.

Right now the **workload.template.yaml** is incomplete. It doesn't do much at this point. You will be filling in different sections of the templates as you follow along the rest of the workshop.