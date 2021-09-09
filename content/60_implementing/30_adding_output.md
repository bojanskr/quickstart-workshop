+++
title = "Adding outputs"
chapter = false
weight = 30
+++

**Outputs** section of the CloudFormation template allows us to return any values to the user after the Stack creation is completed successfully. Some examples are IP address of the EC2 instance, VPC Id, S3 bucket name, etc.

### Outputs section

The Outputs section consists of the key name _Outputs_, followed by a space and a single colon. You can declare a maximum of 200 outputs in a template.

The following example demonstrates the structure of the Outputs section.

```yaml
Outputs:
  Logical ID:
    Description: Information about the value
    Value: Value to return
    Export:
      Name: Value to export
```

### Add Outputs to the workload template

For this workshop, you will add the following output to your workload template to give users easy access to the webserver URL.

```yaml
Outputs:
  URL:
    Description: The URL of the website
    Value: !Join 
      - ''
      - - 'http://'
        - !GetAtt 
          - ElasticLoadBalancer
          - DNSName
```

Run the following command to add outputs to the **workload.template.yaml** file.

```
cd /home/ec2-user/environment
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/cfn-workshop/templates/stubs/outputs.workload.template.yaml -o templates/workload.template.yaml
```

Open *workload.template.yaml* file in a text editor to see the outputs being added.