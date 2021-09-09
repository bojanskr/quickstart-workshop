+++
title = "Adding Resources"
chapter = false
weight = 10
+++

### Add resources to your Workload template

_Resources_ is the required section in a CloudFormation template. 

Each CloudFormation resource has a **Type** and few **Properties**. 

The resource type identifies the type of resource that you are declaring. For example, `AWS::AutoScaling::AutoScalingGroup` declares an Auto Scaling group. 

Resource properties are additional options that you can specify for a resource. Some properties are required and some are optional. For example, _MinSize_ and _MaxSize_ are required properties, whereas, _Tags_ is optional.

Following code shows 3 sample Resources - an Auto Scaling Group, a Launch Configuration and an Elastic Load Balancer. As you can see, each resource has a type and few properties.

```yaml
Resources:
  WebServerGroup:
    Type: 'AWS::AutoScaling::AutoScalingGroup'
    Properties:
      VPCZoneIdentifier:
        - !Ref PublicSubnet1ID
        - !Ref PublicSubnet2ID
      LaunchConfigurationName: !Ref WebServerLaunchConfig
      MinSize: '2'
      MaxSize: '8'
      Tags:
        - Key: name
          Value:  WebServer ASG
    ....

  WebServerLaunchConfig:
    Type: 'AWS::AutoScaling::LaunchConfiguration'
    Properties:
      KeyName: myKeyPair
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref WebServerSecurityGroup
    ....

  ApplicationLoadBalancer:
    Type: 'AWS::ElasticLoadBalancingV2::LoadBalancer'
    Properties:
      Subnets:
        - !Ref PublicSubnet1ID
        - !Ref PublicSubnet2ID
    ....
```

For this workshop, we have pre-created the workload template which you can download to the **templates/** directory of your project.

Run the following command to download the workload template.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/resources.workload.template.yaml -o templates/workload.template.yaml
```

Open **templates/workload.template.yaml** file in a text editor to inspect the resources being added to the template.

All of the resources together builds a multi-AZ, auto-scaled web server in private subnets, with ELB in the public subnet.