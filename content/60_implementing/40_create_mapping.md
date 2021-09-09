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

In the workload template, you have a hardcoded AMI value for the WebServer as shown below:

```yaml
Properties:
      KeyName: !Ref KeyPairName
      ImageId: 'ami-ad45dr33ddfe3ddf'
```

To pass the AMI Id dynamically based on a region where the CloudFormation stack is created, add a AWSAMIRegionMap in the Mappings section and replace the hardcoded AMI Id value with the intrinsic function **Fn::FindInMap**, as shown below:

```yaml
Mappings:
  AWSAMIRegionMap:
    AMI:
      US1604HVM: ubuntu/images/hvm-ssd/ubuntu-xenial-16.04-amd64-server-20180405
    ap-northeast-1:
      US1604HVM: ami-60a4b21c
    ap-northeast-2:
      US1604HVM: ami-633d920d
    ap-south-1:
      US1604HVM: ami-dba580b4
    ap-southeast-1:
      US1604HVM: ami-82c9ecfe
    ap-southeast-2:
      US1604HVM: ami-2b12dc49
    ca-central-1:
      US1604HVM: ami-9d7afcf9
    eu-central-1:
      US1604HVM: ami-cd491726
    eu-west-1:
      US1604HVM: ami-74e6b80d
    eu-west-2:
      US1604HVM: ami-506e8f37
    sa-east-1:
      US1604HVM: ami-5782d43b
    us-east-1:
      US1604HVM: ami-6dfe5010
    us-east-2:
      US1604HVM: ami-e82a1a8d
    us-west-1:
      US1604HVM: ami-493f2f29
    us-west-2:
      US1604HVM: ami-ca89eeb2
```

```yaml
Properties:
  KeyName: !Ref KeyPairName
  ImageId: !FindInMap 
    - AWSAMIRegionMap
    - !Ref 'AWS::Region'
    - US1604HVM
```

### Adding Mappings section

Run the following command to add Mappings section and update ImageId property to use the mapping, in the **workload.template.yaml** file.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/mappings.workload.template.yaml >>templates/workload.template.yaml
```

Open _templates/workload.template.yaml_ in an editor to verify the Mappings section.