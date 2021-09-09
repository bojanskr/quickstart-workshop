+++
title = "Nested stacks"
chapter = false
weight = 70
+++

So far in the workshop, the CloudFormation template you have created deploys all the resources necessary to create an auto-scaled webserver with a load balancer. Users who wants to deploy your CloudFormation template needs to have a VPC in their AWS Account, as your template requires VPC details such as VPC Id, Subnet IDs, etc.

You may choose to create a VPC and other related resources in the same Workload CloudFormation template. However, as you write other CloudFormation templates in the real world, you will often find that VPC is a common resource which you need to create for variety of different workloads. So, instead of copy and pasting VPC related resources in every workload template, its best to have a separate CloudFormation template for creating netowrking resources such as VPC, Subnets, Network ACLs and any other related resources, and reference that template. Visually, your template structure will look like below.

{{< figure src="/images/main-template.png" title="Nested stacks" >}}

You have a `main.template.yaml` file which creates your main stack. This file references two other templates. First is `aws-vpc.template.yaml` file which creates a VPC stack and second is `workload.template.yaml` file which creates the workload stack. VPC stack and Workload stack are called *Nested stacks*.

### Using existing template

The [Quick Start catalog](https://aws.amazon.com/quickstart) has 190+ reference architectures that has been deployed thousands of times by customers. This catalog includes a [VPC Quick Start](https://aws.amazon.com/quickstart/architecture/vpc/) which builds a virtual private network (VPC) environment with public and private subnets, following AWS best practices. It is also highly customizable. Therefore, instead of building your own VPC template, its best to use an existing VPC template that has been battle tested.

#### Git Submodules

To use the VPC Quick Start in your workshop, you will use Git Submodules feature.

Git Submodules allow you to have a Git repository as a subdirectory of another Git repository. This lets you clone another repository into your project, and keep it in sync with the original repository whenever there are new updates to it.

Change directory to the root of your project folder.

```
cd /home/ec2-user/environment
```

Initialize current directory as a Git repo.

```
git init
```

Add VPC Quick Start as a submodule.

```
git submodule add -b main https://github.com/aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc
```

By running the above command, you have added the **quickstart-aws-vpc** git repo as a submodule in the **submodules/quickstart-aws-vpc** directory of qs-workshop repo, and the submodule is tracking the main branch of the *quickstart-aws-vpc*.

Your project directory **qs-workshop** should look like below.

<pre>
    ├── submodules
    │   ├── quickstart-aws-vpc
    │       ├── LICENSE.txt
    │       ├── NOTICE.txt
    │       ├── README.md
    │       ├── templates
    │       │   └── aws-vpc.template
    │       └── .taskcat.yml
    │
    ├── templates
    │   └── workshop.template.yaml
    └── .gitmodules
</pre>

### Creating main template

Let’s create the main templete now, as shown in the image above.

Create the main template by creating a file called `main.template.yaml` in **templates/** directory, copy the below contents into the file, and save.

```yaml
---
AWSTemplateFormatVersion: 2010-09-09

Description:
  This template creates the nested stacks - VPC and Workload stacks.

Resources:
  set of resources

Outputs:
  set of outputs
```

### Add nested stacks

To use VPC and workload templates for creating nested stacks, you will add 2 resources of Type **AWS::CloudFormation::Stack**.

For example, in your _main.template.yaml_ you will create a VPC stack and workload stacks as shown below:

```yaml
Resources:
  VPCStack:
      Type: 'AWS::CloudFormation::Stack'
      Properties:
        TemplateURL:
          !Sub https://${S3BucketName}.s3.${S3BucketRegion}.${AWS::URLSuffix}/${S3KeyPrefix}submodules/quickstart-aws-vpc/templates/aws-vpc.template
        Parameters:
          AvailabilityZones: !Join 
            - ','
            - !Ref AvailabilityZones
          KeyPairName: !Ref KeyPairName
          NumberOfAZs: '2'
          PrivateSubnet1ACIDR: !Ref PrivateSubnet1CIDR
          PrivateSubnet2ACIDR: !Ref PrivateSubnet2CIDR
          PublicSubnet1CIDR: !Ref PublicSubnet1CIDR
          PublicSubnet2CIDR: !Ref PublicSubnet2CIDR
          VPCCIDR: !Ref VPCCIDR
  WorkloadStack:
      Type: 'AWS::CloudFormation::Stack'
      Properties:
        TemplateURL:
          !Sub https://${S3BucketName}.s3.${S3BucketRegion}.${AWS::URLSuffix}/${S3KeyPrefix}templates/public.workload.template.yaml
        Parameters:
          InstanceType: !Ref InstanceType
          SSHLocation: !Ref SSHLocation
          KeyName: !Ref KeyPairName
          OperatorEMail: !Ref OperatorEMail
          PublicSubnet1ID: !GetAtt VPCStack.Outputs.PublicSubnet1ID
          PublicSubnet2ID: !GetAtt VPCStack.Outputs.PublicSubnet2ID
          VPCID: !GetAtt VPCStack.Outputs.VPCID
```

To make it simple for this workshop, we have pre-created a stub that you can copy to your main template.

Run the following command to copy the pre-created **main.template.yaml** file.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/main.template.yaml -o templates/main.template.yaml
```

Open _templates/main.template.yaml_ in an editor to verify the content.

In addition to the VPC and workload Stack in the Resources section, you will also find the parameters section being added. Parameters section contains the parameters that are required by both the VPC template and the workload template.

### Result

**Congratulations!** You have successfully created CloudFormation templates that creates a VPC and deploys your workload inside that VPC.