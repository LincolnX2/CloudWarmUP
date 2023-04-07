# CloudWarmUP
Multicloud intensive Training by Jean Rodrigues 
WarmUp Day2 05/04/2023

What Is Terraform? 

Terraform is an IAC tool, used primarily by DevOps teams to automate various infrastructure tasks. The provisioning of cloud resources, for instance, is one of the main use cases of Terraform. It’s a cloud-agnostic, open-source provisioning tool written in the Go language and created by HashiCorp.

The importance of Terraform?

- an infrastructure as code (IaC) tool that lets you build,change and version both cloud and on-premises resources.
- automation tool
- Cloud Agnostic
- Declarative Language (HCL)
- "Agentless and Masterless"

Terraform : Use Cases

1. Resource provisioning on cloud providers
	- 'plugins' connected to 'providers'
	- Multicloud deployment
2. Resource Provisioning on 'vmware' environments
	- Terraform + vmware
3. combine with multiple tools together
	-Terraform + Ansible + kubernetes

Usefulness of Terraform in Devops Career

1. Terraform is one of the main tools in devops universe
2. Terraform is part of the scope of the professional who works with cloud
3. Terraform is widely used by large companies.
4. Terraform is the evolution of the manual tasks ie tasks are automated.

Benefits of Infrastructure-as-Code (IaC)

IaC replaces standard operating procedures and manual effort required for IT resource management with lines of code. Instead of manually configuring cloud nodes or physical hardware, IaC automates the process infrastructure management through source code.

Here are several of the major key benefits of using an IaC solution like Terraform:

1. Speed and Simplicity. IaC eliminates manual processes, thereby accelerating the delivery and management lifecycles. IaC makes it possible to spin up an entire infrastructure architecture by simply running a script.

2. Team Collaboration. Various team members can collaborate on IaC software in the same way they would with regular application code through tools like Github. Code can be easily linked to issue tracking systems for future use and reference.

3. Error Reduction. IaC minimizes the probability of errors or deviations when provisioning your infrastructure. The code completely standardizes your setup, allowing applications to run smoothly and error-free without the constant need for admin oversight.

4. Disaster Recovery. With IaC you can actually recover from disasters more rapidly. Because manually constructed infrastructure needs to be manually rebuilt. But with IaC, you can usually just re-run scripts and have the exact same software provisioned again.

5. Enhanced Security. IaC relies on automation that removes many security risks associated with human error. When an IaC-based solution is installed correctly, the overall security of your computing architecture and associated data improves massively.

How does terraform works?

Terraform lets you define and manage your entire infrastructure via configuration files and version control. It accomplishes this by using the two main components of Terraform architecture: Core and Providers.
Terraform.exe(binary) will read tf files in the configuration files containing main.tf,resources.tfl and variable.tfl and so check the state file and provision what is requested.

Hands on Terraform & AWS
We want to use terraform as an IaC to provision amazon S3
Terraform + vs code - create configuration files - terraform - To provision Amazon Simple Storage(Amazon S3)

Get configuration template for aws from :
https://registry.terraform.io/

Installed version:
  terraform.x86_64 0:1.4.4-1                                                                                                                                                                                                                      
#STEPS


After Terraform is installed via CLI do the following:
upload the main.tf file through amazon console https://s3.console.aws.amazon.com/s3/buckets?region=us-east-1&region=us-east-1 
run 'terraform init'
run 'terraform plan'
run 'terraform apply'

# Hands-on with AWS and Terraform

# Terraform Configuration File (main.tf)

```jsx
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-1"
}

resource "aws_s3_bucket" "s3_bucket" {
  bucket = "tcb-app-qa-jr"
}

resource "aws_s3_bucket_public_access_block" "s3_block" {
  bucket = aws_s3_bucket.s3_bucket.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}
```

# Steps
- Install terraform by taken the following steps on CLI:
- sudo yum install -y yum-utils shadow-utils
- sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
- sudo yum -y install terraform

On the desktop or vscode:
- Create folder cloud-warmup
- Create folder live2-terraform-aws
- Open the cloud-warmup folder on VS Code
- Create the file [main.tf](http://main.tf/)
- Create the configuration to deploy an S3 bucket

```jsx
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-1"
}

resource "aws_s3_bucket" "s3_bucket" {
  bucket = "tcb-app-qa-jr"
}
```

- Login to AWS, open the Cloud Shell
- Install Terraform
[https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started)
- Upload the [main.tf](http://main.tf/) file to the Cloud Shell
- Init, plan and apply to create the S3

```jsx
terraform init
terraform plan
terraform apply
```

- Add the configuration to prevent public access on S3

```jsx
resource "aws_s3_bucket_public_access_block" "s3_block" {
bucket = aws_s3_bucket.s3_bucket.id

block_public_acls       = true
block_public_policy     = true
ignore_public_acls      = true
restrict_public_buckets = true
}
```

# Troubleshooting:

If the Cloud Shell AWS CLI token session expires, run any AWS CLI to refresh it. Example:
aws s3 ls s3://tcb-app-qa-jr
