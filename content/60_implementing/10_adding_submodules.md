+++
title = "Adding submodules"
chapter = false
weight = 10
+++

The Quick Start catalog has **160+** Quick Starts. It includes a [VPC Quick Start](https://aws.amazon.com/quickstart/architecture/vpc/) which builds a virtual private network (VPC) environment with public and private subnets, following AWS best practices. 

You will use the VPC Quick Start to create a VPC in your workshop Quick Start. By using an existing Quick Start, you get the following benefits:

- Re-use the architeture built by AWS SAs, which follows the AWS best practices.
- Automatically get the AMI and security updates for VPC and Linux bastion stacks.
- Less code to maintain.
- Focus on building the workload.
- Avoid duplicating same code across multiple Quick Starts

### Git Submodules
To use the VPC Quick Start in your workshop Quick Start, you will use Git Submodules.

Git Submodules allow you to keep a Git repository as a subdirectory of another Git repository. This lets you clone another repository into your project and keep your commits separate.

We will add a submodule to the **qs-workshop** repo - QuickStart VPC.

### Add a VPC to your project
Change directory to the root of your repo.

Make sure you are in *qs-workshop* folder.

Add QuickStart VPC as a submodule.

```
git submodule add -b master https://github.com/aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc
```

By running the above command, you have added the **quickstart-aws-vpc** git repo as a submodule in the **submodules/quickstart-aws-vpc** directory of qs-workshop repo, and the submodule is tracking the master branch of the *quickstart-aws-vpc*.

Now, Commit your changes and push to the develop branch.

`git commit -a -m "Add QuickStart VPC Submodule"`

{{% notice tip %}}
If you need to update your submodules later you can use the following command  `git submodule update --recursive`
Similarly, if you are cloning an existing repo that already contains a submodule you will need to run `git submodule init` first, then `git submodule update -r` after to copy the contents.
{{% /notice %}}

### Verify project structure

Your project directory **qs-workshop** should look like below.

<pre>
    ├── ci
    │   ├── taskcat.yml
    │   └── workshop_input.json
    ├── submodules
    │   ├── quickstart-aws-vpc
    │       ├── LICENSE.txt
    │       ├── NOTICE.txt
    │       ├── README.md
    │       ├── ci
    │       │   ├── (test input files ...)
    │       │   └── taskcat.yml
    │       └── templates
    │           └── aws-vpc.template
    │  
    ├── templates
    │   └── master.template.yaml
    │   └── workshop.template.yaml
    ├── .gitmodules
    └── .taskcat.yml
</pre>

Once you have verified that your project structure is correct, its time to push the changes to the develop branch.

Run `git push origin develop`

<pre>
    Enumerating objects: 13, done.
    Counting objects: 100% (13/13), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (8/8), done.
    Writing objects: 100% (8/8), 1.86 KiB | 635.00 KiB/s, done.
    Total 8 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    To github.com:avattathil/qs-workshop.git
       3fe60df..acdba90  develop -> develop
</pre>
