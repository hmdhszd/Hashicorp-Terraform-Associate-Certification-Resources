



###  In Terraform, a `locals` `block` is used to define local variables within a module, allowing you to create reusable expressions and reduce duplication in your code.



__________________________________________________________________________________________





### A local value assigns a name to an expression, so you can use it multiple times within a module without repeating it.



__________________________________________________________________________________________



# Example 1


```hcl
provider "aws" {
  region = "us-west-2"  # Change this to your desired region
}
```



```hcl
locals {
  instance_tags = {
    Name        = "ExampleInstance"
    Environment = "Development"
    Project     = "MyProject"
  }
}
```






```hcl
resource "aws_instance" "example_instance" {
  ami           = "ami-0c55b159cbfafe1f0"  # Change this to your desired AMI
  instance_type = "t2.micro"               # Change this to your desired instance type

  tags = local.instance_tags
}

```



__________________________________________________________________________________________




# Example 2




```hcl
provider "aws" {
  region = "us-west-2"  # Change this to your desired region
}
```



```hcl
resource "random_string" "bucket_suffix" {
  length = 4
  special = false
  upper = false
}
```

```hcl
variable "bucket_prefix" {
  description = "Prefix to be added to the bucket name"
  type        = string
  default     = "my-prefix"
}
```


```hcl
locals {
  bucket_name = "${var.bucket_prefix}-${random_string.bucket_suffix.id}"
}
```



```hcl
resource "aws_s3_bucket" "example_bucket" {
  bucket = local.bucket_name
  acl    = "private"  # Change this to your desired ACL
}
```



__________________________________________________________________________________________


Can a local value reference another local value?


```hcl
variable "base_price" {
  description = "The base price of a product"
  type        = number
  default     = 100
}

variable "tax_rate" {
  description = "The tax rate as a decimal (e.g., 0.10 for 10%)"
  type        = number
  default     = 0.10
}

# Calculate the tax amount
locals {
  calculated_tax = var.base_price * var.tax_rate
}

# Calculate the total price including tax
locals {
  total_price = var.base_price + local.calculated_tax
}

output "calculated_tax" {
  description = "The calculated tax amount"
  value       = local.calculated_tax
}

output "total_price" {
  description = "The total price including tax"
  value       = local.total_price
}
```



The expression of a local value can refer to other locals, but as usual `reference cycles are not allowed`.

That is, a local ca `NOT` `refer` to `itself` or to a variable that refers (directly or indirectly) back to it.



__________________________________________________________________________________________


