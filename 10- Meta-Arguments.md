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

the resource gonna be a "list"

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







