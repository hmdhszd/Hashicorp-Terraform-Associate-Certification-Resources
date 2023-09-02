








__________________________________________________________________________________________





 `Comma` `,` 

version = ">= 1.2.0, < 2.0.0"


A version constraint is a string literal containing one or more conditions, which are separated by commas. 


__________________________________________________________________________________________




when using version constraints, we can use:


- pessimistic operator "~>"

- "!=" operator

- combination comparison operation to use specific version within a range

- comparison operator


__________________________________________________________________________________________





### see the version of providers    -->    `terraform version`


The "terraform version" command provides the version of terraform as well as the version of the provider plugins that are downloaded in the configuration directory.

For example, the below command shows that the version of aws provider is v3.69.0 and that of local provider is v2.1.0

```bash

iac-server $ terraform version

Terraform v0.13.3 + provider registry.terraform.io/hashicorp/aws v3.69.0 + provider registry.terraform.io/hashicorp/local v2.1.0

```
__________________________________________________________________________________________





## Version constraints:

1- terraform --> `required_providers` --> version (`Provider` Version)

2- terraform --> `required_version` (`Terraform` Version)

3- module --> `version` (`Module` Version)



__________________________________________________________________________________________






### Where can we make use of version constraints?


Version constraints can be used anywhere terraform allows us to specify versions. Most commonly they can be set at:

1. Within the `provider` `version` `configuration` (Inside the `required_providers` block nested inside the `terraform block`)

you can use a specific version of the terraform provider: (default = latest version)


The functionality of a provider plugin may vary drastically from one version to another.

Our terraform configuration may not work as expected when using a version different than the one it was written in.



```bash
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = ">= 3.0, < 4.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"
}
```


2. The `required_version` argument which is used to set the `version of Terraform` to use.



```bash
terraform {
  required_version = ">= 0.14, < 0.15"
}

provider "aws" {
  region = "us-west-2"
}

# Resources and other configurations here
```



3. Within `modules`.




```bash
module_aws_s3_bucket/
  ├── main.tf
  └── variables.tf
```



module_aws_s3_bucket/variables.tf

```bash
variable "bucket_name" {
  type    = string
  default = "my-tf-bucket"
}
```


module_aws_s3_bucket/main.tf

```bash
provider "aws" {
  region = "us-west-2"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = var.bucket_name
  # Other bucket configuration here
}
```



my-tf-bucket.tf

```bash
module "s3_bucket" {
  source = "./module_aws_s3_bucket"
  version = ">= 1.0, < 2.0"

  bucket_name = "my-tf-bucket"
}

```






__________________________________________________________________________________________



What is the default behaviour of Terraform when it doesn’t have an acceptable version of a required plugin or module?

It will attempt to download the newest version that meets the applicable constraints.



__________________________________________________________________________________________




What is the default behaviour of Terraform when it doesn’t have an acceptable version of a required `plugin` or `module`?


It will attempt to download the `newest` (`latest`) version that meets the applicable constraints.

__________________________________________________________________________________________







