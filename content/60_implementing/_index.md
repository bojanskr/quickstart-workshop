+++
title = "Writing CloudFormation"
chapter = true
weight = 60
+++

# Writing CloudFormation templates

Most of the time, when you are writing CloudFormation templates to automate the deployment of a solution, you will create several AWS resources. You can create all the resources in a signle CloudFormation template. However, depending upon the no. of resources you are creating, it can make your CloudFormation template extremely large with thousands of lines of code. This will make your template complex, difficult to read, test, debug and update.

It's usually a best practice to have multiple CloudFormation templates, each creating the AWS resources that are logically grouped together into a stack. For example, we have grouped the resources that you will create in this workshop into 2 templates. `aws-vpc.template.yaml` creates a VPC stack that contains all the resources related to a VPC, such as an AWS VPC, Subnets, Network ACLs, etc. `workload.template.yaml` creates a workload stack that contains all the resource related to the webserver, such as web server auto-scaling group, web server security group, Application load balancer, etc.

![main-template](/images/main-template.png?width=60%&height=60%)

Dividing AWS resources into different templates makes your code modular and easy to test. In our example above, you can test VPC stack and workload stack independently. It reduces the no. of lines of code in each template, making it more readable. And, you can re-use templates such as `aws-vpc.template.yaml`, to create VPC stack across different solutions, avoiding code duplication.

{{% children showhidden="false" %}}


