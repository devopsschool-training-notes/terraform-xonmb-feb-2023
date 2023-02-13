
# What is Terraform?
		- IAAC tool
		- Infra as a Code
		- Coding for Infra
		- From Hashicorp
				Vagrant - terraform - vault - nomad - consul - 
		- Written in GO
		- Release
				terraform - cmd - FREE
				TFE			- GUI - Paid
					Hosted
					Cloud
		- Version - 1.3.8


# Whats there in Infra?
------------------------------
AWS			- CloudFormation
Azure		- ARM
GC
Docker
Kubernetes
Github
https://registry.terraform.io/browse/providers

# Why Terraform?

### 20 Tools - 20 Coding Standard & Spec == Hard to work - learn - test - debug - extend - share

### 2874 Tools == 1 Coding Standard & Spec = == Easy to work - learn - test - debug - extend - share

###  DevOps
- Code for Product
- Code for testing a product
- Code for Code Analysis
- Code for Build
- Code for Security
- Code for CI
- Code for CD
- Code for Infra


# How it works? Architecture??

<img width="914" alt="image" src="https://user-images.githubusercontent.com/44023974/218354871-006be02c-29de-46ae-bb34-f1a43bb3ee1c.png">

# Terraform Workflow

**Step 1 - Install Terraform				DONE**
- https://developer.hashicorp.com/terraform/downloads

**Step 2 - Download Providers				DONE**
- aws
- github

**Create a file called "providers.tf" and copy following code in it.** 
```
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "4.54.0"
    }
	github = {
      source = "integrations/github"
      version = "5.17.0"
    }
  }
}

provider "aws" {
  # Configuration options
}


provider "github" {
  # Configuration options
}
```
**Run a following command to download providers.**
```
$ terraform init
```

Step 3 - Write Terraform Code

Step 4 - $ terraform plan

Step 5 - $ terraform apply

Step 6 - $ terraform destroy


$ C:\tools\terraform\terraform.exe

$ terraform.exe

- How to store Terraform Code?
anyfilename.tf

- wt if i have multiple tf file in ONE dir?

dir1/
		file1.tf		|
		file2.tf		|		ONE TF CODE
		file3.tf		|




