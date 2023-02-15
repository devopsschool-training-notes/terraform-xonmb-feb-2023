
## Here's an example Terraform code block that uses the lookup function to create an EC2 instance in a specific AWS region:
```
# Define your AWS provider
provider "aws" {
  region = "us-west-2"
}

# Define the AMI to use for the EC2 instance
data "aws_ami" "ubuntu" {
  most_recent = true
  owners = ["099720109477"] # Canonical
  filter {
    name = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}

# Define the instance type to use
variable "instance_type" {
  default = "t2.micro"
}

# Define a map of instance tags
variable "tags" {
  default = {
    Name = "Example EC2 Instance"
    Environment = "Development"
  }
}

# Create the EC2 instance
resource "aws_instance" "example" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type
  tags          = var.tags
  key_name      = "example_key"

  # Use the lookup function to get the subnet ID for the region
  subnet_id = lookup(var.subnet_ids, var.region)

  # Use the lookup function to get the security group ID for the region
  vpc_security_group_ids = [lookup(var.security_group_ids, var.region)]
}
```
