+++
title = "Adding Rules"
chapter = false
weight = 60
+++

When passing parameters to the CloudFormation for creating or updating a stack, its important to validate the parameter values. Incorrect values can lead to failure in stack creation or update.

**Rules** section allows you to validate a parameter or a combination of parameters passed to a template, before creating or updating resources.

### Understanding Rules

A Rule consists of two properties:
- Rule condition (optional) - determines when a rule takes effect.
- Assertion (required) - describes what values users can specify for a particular parameter.

You can define only one rule condition, but more than one assertions for a given rule.

Let's take a look at an example. Following rule **prodInstanceType** ensures that the value of the parameter _InstanceType_ contains the keyword _a1.large_, as defined in _Assertions_. This rule will take effect only when the value of the parameter _Environment_ is equals to _prod_, as determined by the _RuleCondition_.

```yaml
Rules:
  prodInstanceType:
    RuleCondition: !Equals 
      - !Ref Environment
      - prod
    Assertions:
      - Assert:
          'Fn::Contains':
            - - a1.large
            - !Ref InstanceType
        AssertDescription: 'For a production environment, the instance type must be a1.large'
```

### Adding Rules to the template

You will add above rule to the workload template to ensure that only a1.large instance types are used for production environments.

Run the following command to add rule in the **workload.template.yaml** file.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/rule.workload.template.yaml >>templates/workload.template.yaml
```

Open _templates/workload.template.yaml_ in an editor to verify the Rules section.