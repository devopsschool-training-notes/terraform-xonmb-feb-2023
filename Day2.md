## Output Vaules
- https://www.devopsschool.com/blog/terraform-output-variable-example/

## Conditioning
- https://www.devopsschool.com/blog/terraform-conditioning-example-program/

## Looping
- https://www.devopsschool.com/blog/how-to-do-looping-iterations-in-terraform/

## terraform Provisioner
- https://www.devopsschool.com/blog/understanding-local-exec-provisioner-in-terraform/

## aws.tf
```

resource "aws_security_group" "allow_tls" {
  name        = "devopsscool-sec-group"
  description = "Allow TLS inbound traffic"
  tags = {
    Name = "devopsschool terraform example"
  }
  ingress {
    # TLS (change to whatever ports you need)
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    # Please restrict your ingress to only necessary IPs and ports.
    # Opening to 0.0.0.0/0 can lead to security vulnerabilities.
    cidr_blocks = ["0.0.0.0/0"]

  }

    ingress {
    # TLS (change to whatever ports you need)
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    # Please restrict your ingress to only necessary IPs and ports.
    # Opening to 0.0.0.0/0 can lead to security vulnerabilities.
    cidr_blocks = ["0.0.0.0/0"]
  }

    ingress {
    # TLS (change to whatever ports you need)
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    # Please restrict your ingress to only necessary IPs and ports.
    # Opening to 0.0.0.0/0 can lead to security vulnerabilities.
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port       = 0
    to_port         = 0
    protocol        = "-1"
    cidr_blocks     = ["0.0.0.0/0"]
  }
}


resource "aws_instance" "web" {
  ami           = "ami-0557a15b87f6559cf"
  instance_type = "t3.micro"
  key_name = "rajesh"
  vpc_security_group_ids = [aws_security_group.allow_tls.id]

  tags = {
    Name = "HelloWorld-Rajesh"
  }
  
  connection {
      type     = "ssh"
      user     = "ubuntu"
      private_key = file("rajesh.pem")
      #host = aws_instance.web.public_ip
      host = self.public_ip
  }
  
  provisioner "local-exec" {
    command = "mkdir terradata"
  }
  
  provisioner "remote-exec" {
    inline = [
      "touch /tmp/devopsschool-remote"
    ]
  }
  
  provisioner "file" {
    source      = "hello.ps1"
    destination = "/tmp/hello.ps1"
  } 
  
  depends_on = [aws_s3_bucket.bucket,aws_security_group.allow_tls]
}


resource "aws_s3_bucket" "bucket" {
  acl    = "private"
}
```
## github.tf

```
variable "github-condition" {
  type    = string
  default = "java1"
}


resource "github_repository" "example" {
  name        = "example-feb-2023"
  description = "My awesome codebase"

  visibility = "public"


}

resource "github_repository" "example1" {
  name        = var.github-condition
  description = "My awesome codebase"

  private = false
  count            = var.github-condition == "java" ? 1 : 0

}
```

## Output.tf

```
output "ec2ip" {
	value = aws_instance.web.private_ip
	description ="This is for demo for showing ec2ip"
}

output "pvtip" {
	value = aws_instance.web.public_ip
	description ="This is for demo for showing ec2ip"
}
```

## Terraform Module 
 - https://www.devopsschool.com/blog/terraform-modules-tutorials-and-complete-guide/

## Example for root module main.ft

```
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"

  name = "my-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway = false
  enable_vpn_gateway = false

  tags = {
    Terraform = "true"
    Environment = "dev"
  }
}

module "Xops" {
  source      = "./Xapp"
}

module "Yops" {
  source      = "./YApp"
}
```

## Assignment - Module - 1
Write a terraform module which has following resources
- 1 ec2 instance
- 1 Security group 
- 1 keypair
- install Apache2 (use ubuntu ami)

## Assignment - Module - 1
Write a terraform module which would create a s3 bucket and 
upload some files to s3 bucket from the host server.

## Assignment - Module - 3
Use any module of your choise from https://registry.terraform.io/browse/modules and install it.
