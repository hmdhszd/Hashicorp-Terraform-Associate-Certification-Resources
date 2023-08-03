


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
