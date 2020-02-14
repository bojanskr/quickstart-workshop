+++
title = "Create a keypair"
chapter = false
weight = 10
+++

An EC2 KeyPair is required if you want to SSH into an EC2 instance. We will be creating multiple EC2 instances in this workshop and use a KeyPair with those instances.

{{% notice tip %}}
If you already have an existing EC2 KeyPair, and corresponding private key, you can skip this page.
{{% /notice %}}

### Create an Amazon EC2 key pair

Sign-in to your [AWS account](https://console.aws.amazon.com/)

We will be working in the **us-east-1 (N. Virginia)** Region for this workshop, therefore, choose **US East (N. Virginia)** from the upper right of the console.
![select region](/images/select-region.png)

Go to the **EC2** console by searching or choosing it from the list of AWS services.

Choose **Key Pairs** from the left pane.
![select keypair](/images/select-keypair.png)

Choose **Create Key Pair**. 
![create keypair](/images/create-keypair.png)

Enter the keypair name as **qsworkshop**, and click **create**. This will automatically download a file named **qsworkshop.pem** on your local machine. This is your private key. 

Move **qsworkshop.pem** file to your home directory. The new location should be *~/qsworkshop.pem*.

Run `cd ~` to go to your home directory.

Reduce the permission on your .pem file so only the root user can read it by running `chmod 400 qsworkshop.pem`.

{{% notice tip %}}
For more information on Amazon EC2 Key Pairs, see the [Amazon EC2 documentation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html).
{{% /notice %}}