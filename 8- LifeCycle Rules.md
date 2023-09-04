
# lifecycle


- ### create_before_destroy


- ### prevent_destroy


- ### Ignore Changes (list)





__________________________________________________________________________________________








### Immutable Infrastructure:

Immutable infrastructure is another paradigm in which it ensures that resources are `never` `modified` after they have been deployed.

If a change is to be made, a new instance of that resource will be provisioned in place of the old one.



__________________________________________________________________________________________


### create_before_destroy

By default, terraform is `immutable`, meaning it `first deletes` a resource and `then creates` the new one with the updated configuration.


but we can change that by add "lifecycle" :

```hcl
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


```hcl
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

```hcl
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

```hcl
resource "aws_instance" "example" {
  # ...

  lifecycle {
    ignore_changes = all
  }
}
```


__________________________________________________________________________________________
