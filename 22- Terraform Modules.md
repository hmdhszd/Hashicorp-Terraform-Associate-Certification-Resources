

## Terraform Modules: `Official`, `Verified`, `Community`

in the Terraform Registry, you can find 3 types of modules:

- `Official` Modules own and maintain by HashiCorp

- `Verified` Modules (have verified checkmark beside its name)

- `Community` Modules


__________________________________________________________________________________________

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






#### Terraform get

we use this command to download the modules from the registry


__________________________________________________________________________________________



## 1- Public Module - Terraform Registry


in the modules, we can use our variables by adding them inside the module block


main.tf

```hcl
module "iam_iam-user" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"
  version = "3.4.0"
  # insert the required variables here
  name = "max"
}
```



__________________________________________________________________________________________


To pass values to a Terraform module when calling the module in your code, you use `input` `variables`. 

__________________________________________________________________________________________


#### to use a variable from a module ===> `output` `block`

When using modules to deploy infrastructure, how would you export a value from one module to import into another module? output block



__________________________________________________________________________________________




## 2- Local Module

directory structure:

```hcl
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


```hcl
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


```hcl
# This is the variables.tf file in the root directory

variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}

# You can add more variables here if needed
```


__________________________________________________________________________________________


my_terraform_project/terraform.tfvars


```hcl
# This is the terraform.tfvars file in the root directory

bucket_name = "my-unique-bucket-name"
```


__________________________________________________________________________________________

my_terraform_project/modules/s3_bucket/main.tf

```hcl
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

```hcl
# This is the variables.tf file for the local module named "s3_bucket"

variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}
```



__________________________________________________________________________________________




my_terraform_project/modules/s3_bucket/outputs.tf


```hcl
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



#### Choose the ways available to `DOWNLOAD` and `UPDATE` the `module` in your current terraform configuration directory.

- terraform `init`

- terraform `get`


__________________________________________________________________________________________





## use GIT as the source of module




**Example 1: Using `HTTPS` as the Git Source**

```hcl
# git_https_example/main.tf
module "example_module" {
  source = "git::https://github.com/your-username/your-module-repo.git"

  # Input variables (if any)
  variable_name = "example_value"
}
```

Replace `"https://github.com/your-username/your-module-repo.git"` with the actual HTTPS URL of your Git repository containing the Terraform module code.


**Example 2: Using `SSH` as the Git Source**


```hcl
# git_ssh_example/main.tf
module "example_module" {
  source = "git::ssh://github.com/your-username/your-module-repo.git"

  # Input variables (if any)
  variable_name = "example_value"
}
```

Replace `"git::ssh://github.com/your-username/your-module-repo.git"` with the actual SSH URL of your Git repository containing the Terraform module code.

Remember that when using SSH, you need to have your SSH key properly configured and the repository accessible using SSH authentication.






__________________________________________________________________________________________

### `Terraform Public Module Registry`

- #### GitHub: The module must be on `GitHub` and must be a `public` repo.

- #### Named `terraform-<PROVIDER>-<NAME>`


- #### Repository description: The `GitHub` `repository` `description` is used to populate the short description of the module.


- #### `Standard` `module` `structure` : (readme.md, main.tf, variable.tf, output.tf)

- #### `x.y.z` tags for releases: The registry uses tags to identify module versions. Release tag names must be a `semantic version`, which can optionally be `prefixed` with a `v` .



__________________________________________________________________________________________


Which of the following Terraform features supports the versioning of a module? 


- Private Module Registry (in private registry, VERSION is required)



- Public Module Registry





__________________________________________________________________________________________


### Private Module Registry

helps you share Terraform providers and Terraform modules across your organization. It includes support for versioning, a searchable list of available providers and modules, and a configuration designer to help you build new workspaces faster.

__________________________________________________________________________________________




You have a number of different variables in a parent module that calls multiple child modules. Can the child modules refer to any of the variables declared in the parent module?



No, it cannot refer to the variable

BUT

it can only refer to values that are passed to the child module


However,

the child module can declare output values to selectively export certain values to be accessed by the calling module (parent module).

__________________________________________________________________________________________



Every Terraform configuration has `at least` `one module`, known as its `root` module, which consists of the resources defined in the .tf files in the main working directory.



__________________________________________________________________________________________



 The module always should be public and open-source to be able to use?  NO - False



You can have your own private module in `Terraform cloud private registry` or `Terraform Enterprise private registry`  or  `Github repository`


__________________________________________________________________________________________



 
The module always should be public and open-source to be able to use? NO

modules can be both public and private




__________________________________________________________________________________________


Modules do not inherit variables from the parent module.


All modules are self-contained units.

So you have to explicitly define variables in the child module, and then explicit set these variables in the parent module, when you instantiate the child module.



__________________________________________________________________________________________



 
