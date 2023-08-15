
# Terraform block

you can use a specific version of the terraform provider: (default = latest version)

we use "terraform" block to configure settings related to terraform itself.

inside this block, we use `required_providers` to specify the version of the provider.



__________________________________________________________________________________________




The functionality of a provider plugin may vary drastically from one version to another.

Our terraform configuration may not work as expected when using a version different than the one it was written in.

As a best practice, always declare the exact version of the provider we want to use within the `required_providers` block.



main.tf

```bash
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "> 3.45.0, !=3.46.0, < 3.48.0"
    }
  }
}

resource "google_compute_instance" "special" {
  name         = "aone"
  machine_type = "e2-micro"
  zone         = "us-west1-c"

}
```







__________________________________________________________________________________________





 `Comma` `,` 

version = ">= 1.2.0, < 2.0.0"


A version constraint is a string literal containing one or more conditions, which are separated by commas. 


__________________________________________________________________________________________




when using version constraints, we can use:


- pessimistic operator "~>"

- "!=" operator

- "~>" operator

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

1- required_providers

2- required_version

3- modules

Version constraints can be used anywhere terraform allows us to specify versions.

Most commonly they can be set at:

1. Within the provider version configuration (Inside the required_providers block nested inside the terraform block)

2. The "required_version" argument which is used to set the version of Terraform to use.

3. Within modules. This is where we specify the version of module to be used.



__________________________________________________________________________________________






### Where can we make use of version constraints?


Version constraints can be used anywhere terraform allows us to specify versions. Most commonly they can be set at:

1. Within the `provider` `version` `configuration` (Inside the `required_providers` block nested inside the `terraform block`)


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


__________________________________________________________________________________________



