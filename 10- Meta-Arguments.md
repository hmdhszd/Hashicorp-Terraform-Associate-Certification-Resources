# lifecycle

The `lifecycle` meta-argument in Terraform controls how resources are managed during their lifecycle, like creation, updates, and deletion. It lets you specify actions for updates, replacements, and prevent accidental deletions.


```bash
resource "aws_s3_bucket" "example_bucket" {
  bucket = "example-bucket-name"
  acl    = "private"

  # Other bucket configuration settings...

  lifecycle {
    prevent_destroy = true

    # Define actions to be taken when the resource is replaced
    create_before_destroy = true
  }
}

```





__________________________________________________________________________________________




# depends_on

## These dependencies come in two flavours: 

#### Implicit – where a resource may reference another resource/data source.

#### Explicit – where an engineer explicitly calls out a dependency between two resources/data sources.

for explicit dependency, we should use "depends_on" : 


```bash
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




# count

we've seen 2 meta arguments: "depends_on" and "lifecycle"

but there are other meta arguments, such as "count"

the created resource gonna be a `list`


we use `count.index`

__________________________________________________________________________________________


main.tf

```bash
resource "local_sensitive_file" "name" {
    filename = var.users[count.index]
    content = var.content
    count = length(var.users)

}
```



variable.tf

```bash
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

the resource gonna be a "map"

we use `each.value`

main.tf


```bash
resource "local_sensitive_file" "name" {
    filename = each.value
    for_each = toset(var.users)
    content = var.content

}
```



__________________________________________________________________________________________






variable.tf

```bash
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


```bash
iac-server $ terraform state list

local_sensitive_file.name["/root/user10"]
local_sensitive_file.name["/root/user11"]
local_sensitive_file.name["/root/user12"]
```



__________________________________________________________________________________________



### the meta-argument which is not supported by the data block. ==> lifecycle


__________________________________________________________________________________________


### When a module has multiple configurations for the same provider, which meta-argument can you use to specify the configuration? `providers`


```bash
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



__________________________________________________________________________________________


A given resource or module block CAN NOT use both `count` and `for_each` simultaneously.

__________________________________________________________________________________________


`alias` and `version` are the `meta-arguments` which are available for all provider blocks.


__________________________________________________________________________________________


Which argument of the `lifecycle` meta-argument supports a `list` as a value ?


`ignore_changes` (list of attribute names)


By default, Terraform detects any difference in the current settings of a real infrastructure object and plans to update the remote object to match configuration.



__________________________________________________________________________________________




The for_each meta-argument accepts: `maps` and `set of strings`



__________________________________________________________________________________________



`lifecycle` is a nested block that can appear within a resource block.

The lifecycle block and its contents are meta-arguments, available for `all` `resource` `blocks` regardless of type.


__________________________________________________________________________________________






