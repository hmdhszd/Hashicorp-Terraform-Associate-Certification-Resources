

### We can have our variables in a separate file (variables.tf) and refer to them with a "var." prefix

ex: var.aws_region

__________________________________________________________________________________________


main.tf

```bash
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "ec2_instance" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_pair_name
}

output "public_ip" {
  value = aws_instance.ec2_instance.public_ip
}
```



__________________________________________________________________________________________

variables.tf

```bashvariable "aws_region" {
  description = "The AWS region where the EC2 instance will be created."
  default     = "us-west-2"
}

variable "ami_id" {
  description = "The ID of the Amazon Machine Image (AMI) for the EC2 instance."
  default     = "ami-0c55b159cbfafe1f0"  # Replace this with your desired AMI ID
}

variable "instance_type" {
  description = "The instance type for the EC2 instance."
  default     = "t2.micro"
}

variable "key_pair_name" {
  description = "The name of the key pair to associate with the EC2 instance."
  default     = "my-key-pair"  # Replace this with the name of your key pair
}
```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________
