+++
title = "Adding Resources"
chapter = false
weight = 10
+++

### Add resources to your Workload template

First you will create a CloudFormation template which will create all the necessary AWS resources to deploy the workload, as shown in Image 1.

Some of the key resources such as Webserver auto-scaling group (WebServerGroup), launch configuration (WebServerLaunchConfig) and Application
load balancer (ApplicationLoadBalancer), are listed below.

_Resources_ is the required section in a CloudFormation template. Each CloudFormation resource has a **Type** and few **Properties**. The resource type identifies the type of resource that you are declaring. For example, `AWS::AutoScaling::AutoScalingGroup` declares an Auto Scaling group. Resource properties are additional options that you can specify for a resource. Some properties are required and some are optional. For example, _MinSize_ and _MaxSize_ are required properties, whereas, _Tags_ is optional.

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
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/workload.template.yaml -o templates/workload.template.yaml
```

Open **templates/workload.template.yaml** file in a text editor to inspect the resources being created in the template.

Commit changes to repo by running the following commands.

`git add templates/workload.template.yaml`

`git commit -a -m 'Added Workload'`