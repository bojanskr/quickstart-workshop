+++
title = "Adding parameters"
chapter = false
weight = 20
+++

Parameters makes your CloudFormation template dynamic and flexible. It allows you to pass the values to your CloudFormation resources and makes it configurable based on the deployment requirements.

Using parameters, you can make the same template create a Production environment with workload deployed across multiple AZs, with large instance sizes and higher auto-scaling min/max/desired values, as well as, a development environment with workload in sigle AZ, smaller instance and without auto-scaling.

### Parameters best practices

Follow the below Quick Start parameter guidelines when creating parameters for your CloudFormation templates:

- Try to parameterize as much as possible, making sure to cover settings that you expect users to customize. Some examples are CIDR blocks, FQDN names, host names, instance types, and storage volume sizes.
- When setting defaults for instance types, make sure that the default is available in all (or the majority of) AWS Regions. To check availability, see [Amazon EC2 Pricing webpages](https://aws.amazon.com/ec2/pricing/on-demand/).
- Must include the standard parameters for the Quick Start S3 bucket name (*QSS3BucketName*) and key prefix (*QSS3KeyPrefix*). Set the default value for the key prefix to *quickstart-repo-name/*, e.g., quickstart-aws-vpc/. See [example](https://aws-quickstart.github.io/design-parms.html#qsconfig).
- Use AWS-specific parameter types as much as possible.
- For parameter names, labels, and groups, follow the guidelines in the [Parameter naming standards section](https://aws-quickstart.github.io/naming-parms.html).

### Identify parameters

Let's identify the parameters which needs to be passed to the **VPC Quick Start** from the main template. 


#### VPC Quick Start parameters

Open *submodules/quickstart-aws-vpc/aws-vpc.template* file to evaluate the *VPC Quick Start* parameters.

*VPC Quick Start* provide variety of parameters to customize the VPC architecture depending upon your needs. 

For this workshop, following parameters values needs to be passed to the **VPC Quick Start** template.

| Parameter Key | Description | Default Value|
| ------------- | ----------- | ------------ |
|AvailabilityZones| List of Availability Zones | Requires Input|
|KeyPairName| The name of an existing public/private key pair| Requires Input |
|PrivateSubnet1CIDR| CIDR block for private subnet 1 located in Availability Zone 1 |10.0.0.0/19|
|PrivateSubnet2CIDR| CIDR block for private subnet 2 located in Availability Zone 2 |10.0.32.0/19|
|PublicSubnet1CIDR| CIDR block for the public (DMZ) subnet 1 located in Availability Zone 1 |10.0.128.0/20|
|PublicSubnet2CIDR| CIDR block for the public (DMZ) subnet 2 located in Availability Zone 2|10.0.144.0/20|
|VPCCIDR| CIDR block for the VPC|10.0.0.0/16|

### Add parameters to the main template

Let's add parameters to **main.template.yaml** CloudFormation template.

For this workshop, we have pre-created a stub template which has all the parameters listed above.

Run the following command to download the stub template and overwrite **main.template.yaml** file.

```
curl https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/incomplete.main.template.yaml -o templates/main.template.yaml
```

Open *main.template.yaml* file in a text editor to see the parameters being added.