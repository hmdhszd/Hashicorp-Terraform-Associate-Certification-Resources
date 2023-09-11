# lifecycle

- ### create_before_destroy


- ### prevent_destroy


- ### Ignore Changes (list)



The `lifecycle` meta-argument in Terraform controls how resources are managed during their lifecycle, like creation, updates, and deletion. It lets you specify actions for updates, replacements, and prevent accidental deletions.


```hcl
resource "aws_s3_bucket" "example_bucket" {
  bucket = "example-bucket-name"
  acl    = "private"

  # Other bucket configuration settings...

  lifecycle {
    prevent_destroy = true

    # Define actions to be taken when the resource is replaced
    create_before_destroy = true

    ignore_changes = [
      # Ignore changes to tags, e.g. because a management agent
      # updates these based on some ruleset managed elsewhere.
      tags,
    ]
  }

}

```





__________________________________________________________________________________________



`lifecycle` is a nested block that can appear within a `resource` `block`.

The lifecycle block is available for `all` `resource` `blocks` regardless of type.


__________________________________________________________________________________________



`lifecycle` is `NOT` `supported` by the `data` `block` 


__________________________________________________________________________________________




# depends_on

## These dependencies come in two flavours: 

#### - Implicit – where a resource may reference another resource/data source.

#### - Explicit – where an engineer explicitly calls out a dependency between two resources/data sources.

for explicit dependency, we should use "depends_on" : 


```hcl
resource "local_file" "whale" {
  filename   = "/root/whale"
  content    = "whale"
  depends_on = [
      local_file.krill
      ]
}
resource "local_file" "krill" {
  filename = "/root/krill"
  content  = "krill"
}
```


__________________________________________________________________________________________


`state` `file` keeps the `dependency` between the resources ( both Implicit and Explicit )


__________________________________________________________________________________________




# count


The count meta-argument accepts a whole number, and creates that many instances of the resource or module.

The `count` meta-argument accepts: `list`

the created resource gonna be a `list`


we use `count.index`

__________________________________________________________________________________________


main.tf

```hcl
resource "local_sensitive_file" "name" {
    filename = var.users[count.index]
    content = var.content
    count = length(var.users)

}
```



variable.tf

```hcl
variable "users" {
    type = list(string)
    default = [ "/root/user10", "/root/user11", "/root/user12", "/root/user13"]
}

variable "content" {
    default = "password: S3cr3tP@ssw0rd"
  
}
```



__________________________________________________________________________________________



# for-each


when there are duplicate values, we use "toset"


The `for_each` meta-argument accepts: `maps` and `set of strings`

the created resource gonna be a `map`

we use `each.value`

main.tf


```hcl
resource "local_sensitive_file" "name" {
    filename = each.value
    content = var.content
    for_each = toset(var.users)

}
```



__________________________________________________________________________________________






variable.tf

```hcl
variable "users" {
    type = list(string)
    default = [ "/root/user10", "/root/user11", "/root/user12", "/root/user10"]
}

variable "content" {
    default = "password: S3cr3tP@ssw0rd"
  
}
```




__________________________________________________________________________________________



#### terraform state list


```hcl
iac-server $ terraform state list

local_sensitive_file.name["/root/user10"]
local_sensitive_file.name["/root/user11"]
local_sensitive_file.name["/root/user12"]
```



__________________________________________________________________________________________


### When a `module` has multiple configurations for the same provider, which meta-argument can you use to specify the configuration? `providers`


```hcl
provider "aws" {
  alias = "region_a"
  region = "us-east-1"
}

provider "aws" {
  alias = "region_b"
  region = "us-west-2"
}

module "example_module" {
  source = "./example_module"
  
  providers = {
    aws = aws.region_a
  }
}
```

for modules => providerS

for others => provider

__________________________________________________________________________________________


A given resource or module block CAN NOT use both `count` and `for_each` simultaneously.

__________________________________________________________________________________________


Which argument of the `lifecycle` meta-argument supports a `list` as a value ?


`ignore_changes` (list of attribute names)


By default, Terraform detects any difference in the current settings of a real infrastructure object and plans to update the remote object to match configuration.



__________________________________________________________________________________________





`alias` and `version` are the `meta-arguments` which are available for all `provider` `blocks`



__________________________________________________________________________________________





