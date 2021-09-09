+++
title = "Create Mappings"
chapter = false
weight = 40
+++

**Mapping** section in the CloudFormation template is like a dictionary variable type in programming language, which allows you to store key value pairs of similar type. It is an optional section in the template.

For example, if you want to set values based on a region, you can create a mapping that uses the region name as a key and contains the values you want to specify for each specific region. You use the `Fn::FindInMap` intrinsic function to retrieve values in a map.

{{% notice warning %}}
You can't include parameters, pseudo parameters, or intrinsic functions in the Mappings section.
{{% /notice %}}

### Understanding Mappings section

In the workload template, you have an option to hardcode AMI value for the WebServer as shown below:

```yaml
Properties:
      KeyName: !Ref KeyPairName
      ImageId: 'ami-ad45dr33ddfe3ddf'
```

However, hardcoding an AMI Id is not a good practice. Instead, you should pass an AMI Id dynamically based on a region where the CloudFormation stack is created.

To do that, add a _AWSRegionArch2AMI_ map in the Mappings section and use the intrinsic function **Fn::FindInMap**, as shown below:

```yaml
Mappings:
  AWSRegionArch2AMI:
      us-east-1:
        HVM64: ami-0ff8a91507f77f867
      us-west-2:
        HVM64: ami-a0cfeed8
      us-west-1:
        HVM64: ami-0bdb828fd58c52235
      eu-west-1:
        HVM64: ami-047bb4163c506cd98
      eu-west-2:
        HVM64: ami-f976839e
      eu-west-3:
        HVM64: ami-0ebc281c20e89ba4b
      eu-central-1:
        HVM64: ami-0233214e13e500f77
      ap-northeast-1:
        HVM64: ami-06cd52961ce9f0d85
      ap-northeast-2:
        HVM64: ami-0a10b2721688ce9d2
      ap-northeast-3:
        HVM64: ami-0d98120a9fb693f07
      ap-southeast-1:
        HVM64: ami-08569b978cc4dfa10
      ap-southeast-2:
        HVM64: ami-09b42976632b27e9b
      ap-south-1:
        HVM64: ami-0912f71e06545ad88
      us-east-2:
        HVM64: ami-0b59bfac6be064b78
      ca-central-1:
        HVM64: ami-0b18956f
      sa-east-1:
        HVM64: ami-07b14488da8ea02a0
      cn-north-1:
        HVM64: ami-0a4eaf6c4454eda75
      cn-northwest-1:
        HVM64: ami-6b6a7d09
```

```yaml
Properties:
  KeyName: !Ref KeyPairName
  ImageId: !FindInMap 
    - AWSRegionArch2AMI
    - !Ref 'AWS::Region'
    - HVM64
```

### Adding Mappings section

Run the following command to add Mappings section and update ImageId property to use the mapping, in the **workload.template.yaml** file.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/mappings.workload.template.yaml -o templates/workload.template.yaml
```

Open *workload.template.yaml* file in a text editor to see the mappings being added.