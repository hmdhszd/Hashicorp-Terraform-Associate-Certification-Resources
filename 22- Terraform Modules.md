

### A Terraform module is a set of Terraform configuration files in a single directory.

Even a simple configuration consisting of a single directory with one or more .tf files is a module. When you run Terraform commands directly from such a directory, it is considered the root module.





__________________________________________________________________________________________



#### Root Module

Every Terraform configuration has at least one module, known as its root module, which consists of the resources defined in the .tf files in the main working directory.

A module can call other modules, which lets you include the child module's resources in the configuration in a concise way.


__________________________________________________________________________________________





#### Child Modules

A module that has been called by another module is often referred to as a child module.

Child modules can be called multiple times within the same configuration, and multiple configurations can use the same child module.



__________________________________________________________________________________________



in the Terraform Registry, you can find 2 types of modules:

- `Official` Modules own and maintain by HashiCorp

- `Verified` Modules (have verified checkmark beside its name)

- `Community` Modules


__________________________________________________________________________________________




#### Terraform get

we use this command to download the modules from the registry


__________________________________________________________________________________________



## 1- Public Module - Terraform Registry


in the terraform module, we can use our variables by adding them inside the module block


main.tf

```bash
module "iam_iam-user" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"
  version = "3.4.0"
  # insert the required variables here
  name = "max"
}
```



__________________________________________________________________________________________



## 2- Local Module

directory structure:

```bash
my_terraform_project/
├── main.tf
├── variables.tf
├── terraform.tfvars
├── modules/
│   └── s3_bucket/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── .terraform/ (directory created after running 'terraform init')
```


__________________________________________________________________________________________



we use module block to refer to the module:


my_terraform_project/main.tf


```bash
# This is the main configuration file

provider "aws" {
  region = "us-west-1"
}

module "my_s3_bucket" {
  source     = "./modules/s3_bucket"
  bucket_name = "my-unique-bucket-name"
}

output "bucket_id" {
  description = "ID of the created S3 bucket from the local module"
  value       = module.my_s3_bucket.bucket_id
}
```


__________________________________________________________________________________________

my_terraform_project/variables.tf


```bash
# This is the variables.tf file in the root directory

variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}

# You can add more variables here if needed
```


__________________________________________________________________________________________


my_terraform_project/terraform.tfvars


```bash
# This is the terraform.tfvars file in the root directory

bucket_name = "my-unique-bucket-name"
```


__________________________________________________________________________________________

my_terraform_project/modules/s3_bucket/main.tf

```bash
# This is the main.tf file for the local module named "s3_bucket"

resource "aws_s3_bucket" "my_bucket" {
  bucket = var.bucket_name
  acl    = "private"
}

resource "aws_iam_policy" "s3_policy" {
  name        = "s3-policy"
  description = "Policy for accessing the S3 bucket"

  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect   = "Allow",
        Action   = ["s3:GetObject"],
        Resource = "${aws_s3_bucket.my_bucket.arn}/*",
      },
    ],
  })
}

```



__________________________________________________________________________________________





my_terraform_project/modules/s3_bucket/variables.tf

```bash
# This is the variables.tf file for the local module named "s3_bucket"

variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}
```



__________________________________________________________________________________________




my_terraform_project/modules/s3_bucket/outputs.tf


```bash
# This is the outputs.tf file for the local module named "s3_bucket"

output "bucket_id" {
  description = "ID of the created S3 bucket"
  value       = aws_s3_bucket.my_bucket.id
}
```




__________________________________________________________________________________________



### Module Composition



We call this flat style of module usage module composition, because it takes multiple composable building-block modules and assembles them together to produce a larger system.






__________________________________________________________________________________________



Modules can be used to create lightweight abstractions, so that you can describe your infrastructure in terms of its architecture, rather than directly in terms of physical objects.


__________________________________________________________________________________________



#### Choose the ways available to download the module in your current terraform configuration directory.

- terraform init

- terraform get


__________________________________________________________________________________________
