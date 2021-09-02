+++
title = "Creating VPC Stack"
chapter = false
weight = 30
+++

At this point you have everything you need to build an **AWS VPC** as a nested stack, spanned across multiple Availability zones as shown in the image below.

![vpc-only](/images/aws-vpc.png)

### Add QuickStart VPC as a nested stack

Open _templates/main.template.yaml_ in an editor to inspect the contents of the file. Right now the **Resources** section is empty.

You will add a resource of Type **'AWS::CloudFormation::Stack'** to create a nested cloudformation stack.

Close _templates/main.template.yaml_ file and run the following command to add **VPC Stack** resource.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/vpcstack.main.template.yaml >>templates/main.template.yaml
```

Add and commit your changes.

`git add .`

` git commit -a -m 'Add QuickStart VPC as a nested stack'`

### Inspect VPC Stack Resource

Open _templates/main.template.yaml_ in an editor and your **Resources** sections should look as shown below.

<pre>
    Resources:
      VPCStack:
        Type: 'AWS::CloudFormation::Stack'
        Properties:
          TemplateURL: !Sub >-
            https://${QSS3BucketName}.s3.amazonaws.com/${QSS3KeyPrefix}submodules/quickstart-aws-vpc/templates/aws-vpc.template
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
</pre>

**Congratulations!** You have successfully added an AWS VPC to your Quick Start.



