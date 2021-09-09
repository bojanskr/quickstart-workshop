+++
title = "Adding Conditions"
chapter = false
weight = 50
+++

To make your CloudFormation template flexible and re-use the same template for multiple environments like Dev, Pre-Prod and Prod, sometimes you want to have certain AWS resources created or configured only for a specific environment. For example, you may want to create an EBS volume and mount it to your EC2 instance for Production deployment. But, for development environment, you may want to just use the local instance store.

You can implement it using **Conditions** in the CloudFormation template. You can create a condition and then associate it with a resource or output so that AWS CloudFormation only creates the resource or output if the condition is true. Similarly, you can associate the condition with a property so that AWS CloudFormation only sets the property to a specific value if the condition is true. If the condition is false, AWS CloudFormation sets the property to a different value that you specify.

### Understanding Conditions

First, you need to define a _Condition_ which will evaluate to _True_ or _False_, depending upon the intrinsic functions and values being compared. An example of a condition is shown below.

Here, condition called **CreateProdResources** will evaluate to _True_, if the value of _EnvType_ parameter is equals to _prod_, otherwise _False_.

```yaml
Conditions:
  CreateProdResources: !Equals 
    - !Ref EnvType
    - prod
```

**!Equals** is an intrinsic function that is used to evaluate the condition. For list of all the allowed functions, see [Condition functions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-conditions.html).

### Adding Conditions to the template

In the workload template, you currently have single Webserver Security group. You will create a Condition, as shown above. 

You will add another security group resource to your template which is more restrictive for production environment and attach above condition so that, the new Security group is created only when user is deploying the stack to create production environment.

Run the following command to add condition and new Security group in the **workload.template.yaml** file.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/condition.workload.template.yaml >>templates/workload.template.yaml
```

Open _templates/workload.template.yaml_ in an editor to verify the Conditions section.