+++
title = "Adding outputs"
chapter = false
weight = 70
+++

The **final step** in finishing your main template is to add outputs. **Outputs** section of the CloudFormation template allows us to return any values to the user after the Stack creation is completed successfully. Some examples are IP address of the EC2 instance, VPC Id, etc.

### Add Outputs

For this workshop, you will add the following outputs to your main template.

<pre>
	Outputs:
	  WebUrl:
	    Description: The web server URL
	    Value:
	      Fn::GetAtt:
	      - WorkloadStack
	      - Outputs.URL
</pre>

Run the following command to add outputs to **main.template.yaml** file.

```
curl -s https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/main/implementing/templates/outputs.main.template.yaml >>templates/main.template.yaml
```

Commit your changes.

` git commit -a -m 'Add outputs to main template'`

### Inspect Outputs

Open _templates/main.template.yaml_ in an editor and your **Outputs** section should have all the outputs, as mentioned above.

**Congratulations! You have successfully finished developing CloudFormation templates for your Quick Start. It's time to test it now.**