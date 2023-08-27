
# lifecycle


- ### create_before_destroy


- ### prevent_destroy


- ### Ignore Changes





__________________________________________________________________________________________


### create_before_destroy

By default, terraform is `immutable`, meaning it `first deletes` a resource and `then creates` the new one with the updated configuration.


but we can change that by add "lifecycle" :

```bash
resource "azurerm_resource_group" "example" {
  # ...

  lifecycle {
    create_before_destroy = true
  }
}
```



__________________________________________________________________________________________


### prevent_destroy

sometimes we do not want a resource to be destroyed for any reason, 

and Terraform will reject any changes that result in destroy of the resources


```bash
resource "azurerm_resource_group" "example" {
  # ...

  lifecycle {
    prevent_destroy = true
  }
}
```
 


__________________________________________________________________________________________




### Ignore Changes

When you want Terraform to ignore changes between subsequent apply commands you can use the lifecycle ignore_changes meta-argument.

The ignore_changes argument means that Terraform will set the value when the resource is first deployed and then forever ignore any changes to it.

```bash
resource "aws_instance" "example" {
  # ...

  lifecycle {
    ignore_changes = [
      # Ignore changes to tags, e.g. because a management agent
      # updates these based on some ruleset managed elsewhere.
      tags,
    ]
  }
}
```

OR

we can use "ALL" to ignore all of them

```bash
resource "aws_instance" "example" {
  # ...

  lifecycle {
    ignore_changes = all
  }
}
```


__________________________________________________________________________________________
