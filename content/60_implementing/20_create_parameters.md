+++
title = "Adding parameters"
chapter = false
weight = 20
+++

Parameters makes your CloudFormation template dynamic and flexible. It allows you to pass the values to your CloudFormation resources and makes it configurable based on the deployment requirements.

Using parameters, you can make the same template create a Production environment with workload deployed across multiple AZs, with large instance sizes and higher auto-scaling min/max/desired values, as well as, a development environment with workload in sigle AZ, smaller instance and without auto-scaling.

### Parameters

Follow the below best practices when creating parameters for your CloudFormation templates:

- Try to parameterize your templates appropriately, making sure to cover settings that you expect users to customize. Some examples are CIDR blocks, FQDN names, host names, instance types, and storage volume sizes.
- When adding parameters in your template, you can set default values to it. Make sure that the default value is available in all (or the majority of) AWS Regions. To check availability, see [Amazon EC2 Pricing webpages](https://aws.amazon.com/ec2/pricing/on-demand/).
- Use AWS-specific parameter types whenever possible. It helps with auto-validation of the parameter values. Check [parameters reference page](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html#aws-specific-parameter-types) for the list of all the available parameter types.


#### Identify parameters

Looking at your `templates/workload.template.yaml` let's identify the parameters that should be added to make the workload configurable.


##### Workload template parameters

For this workshop, we have identified the following parameters that should be added to your workload template.

| Parameter Key | Description | Default Value|
| ------------- | ----------- | ------------ |
|InstanceType| EC2 instance type | t2.medium|
|KeyPairName| The name of an existing public/private key pair| Requires Input |
|PrivateSubnet1ID| Private Subnet Id 1 |Requires Input |
|PrivateSubnet2ID| Private Subnet Id 2 |Requires Input |
|PublicSubnet1ID| Public Subnet Id 1 |Requires Input |
|PublicSubnet2ID| Public Subnet Id 2 |Requires Input |
|SSHLocation| Allowed CIDR block for  webserver SSH access|10.0.0.0/16|
|OperatorEmail| Email address to send an email for auto-scaling event |Requires Input |
|VPCID| ID of the VPC |Requires Input |

#### Add parameters to the workload template

Let's add parameters to the **workload.template.yaml** CloudFormation template.

For this workshop, we have pre-created a stub template which has all the parameters listed above.

Run the following command to download the stub template and overwrite **workload.template.yaml** file.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/parameters.workload.template.yaml -o templates/workload.template.yaml
```

Open *workload.template.yaml* file in a text editor to see the parameters being added.


### Parameter groups and labels

When you use the AWS CloudFormation console to create or update a stack, the console alphabetically lists parameters of your templates by their logical ID. You may want to improve the experience of the users deploying your template by displaying the parameters in a logical group and in a specific order. You may also want to customize the parameter labels. This can be done using `AWS::CloudFormation::Interface` metadata key.

In the metadata key, you can specify the groups to create, the parameters to include in each group, and the order in which the console shows each parameter within its group. You can also define friendly parameter names so that the console shows descriptive names instead of logical IDs.

#### Workload template parameter groups and labels

Following are the 2 parameter groups we have created for the workload template.

```yaml
Metadata:
  AWS::CloudFormation::Interface:
    ParameterGroups:
    - Label:
        default: Network configuration
      Parameters:
      - VPCID
      - PrivateSubnet1ID
      - PrivateSubnet2ID
      - PublicSubnet1ID
      - PublicSubnet2ID
    - Label:
        default: Amazon EC2 configuration
      Parameters:
      - KeyPairName
      - InstanceType
    ParameterLabels:
      KeyPairName:
        default: SSH key name
      PrivateSubnet1ID:
        default: Private subnet 1 ID
      PrivateSubnet2ID:
        default: Private subnet 2 ID
      PublicSubnet1ID:
        default: Public subnet 1 ID
      PublicSubnet2ID:
        default: Public subnet 2 ID
```

#### Add parameter groups and labels to the workload template

Let's add parameter groups and labels to the **workload.template.yaml** CloudFormation template.

For this workshop, we have pre-created a stub template which has parameter groups and labels listed above.

Run the following command to download the stub template and overwrite **workload.template.yaml** file.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/parametergroups.workload.template.yaml -o templates/workload.template.yaml
```

Open *workload.template.yaml* file in a text editor to see the parameter groups and labels being added.