+++
title = "Adding your workload"
chapter = false
weight = 50
+++

In the Quick Start context, the term **workload** is referred as the partner product and all the necessary resources deployed using the CloudFormation template.

In this workshop, **an autoscaled nginx web server deployed across 2 AZs, along with Elastic load balancer (ELB)** is referred as workload, as shown in the image below.

{{< figure src="/images/workload.png" title="Image 1: Workload" >}}

### Create Workload template

To keep the code modular, maintainable and easy to test, its important to create workload as a nested stack, similar to how you did for VPC and Bastion stack.

First you will create a CloudFormation template which will create all the necessary AWS resources to deploy the workload, as shown in Image 1.

For this workshop, we have pre-created the workload template which you can download to the **templates/** directory of your project.

Run the following command to download the workload template.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/workload.template.yaml -o templates/workload.template.yaml
```

Open **templates/workload.template.yaml** file in a text editor to inspect the resources being created in the template.

Commit changes to repo by running the following commands.

`git add templates/workload.template.yaml`

`git commit -a -m 'Added Workload'`