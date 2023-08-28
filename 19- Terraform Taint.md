


### NOTE: This used to be `terraform taint` and has been replaced with `terraform apply -replace`



__________________________________________________________________________________________



### terraform apply -replace=aws_instance.web

recreate the one resource without having to destroy everything that was created

we use replace instead of taint


__________________________________________________________________________________________




### when you apply and the resource creation fails for any reason, Terraform marks the resource as tainted.

### this can be seen when we run the terraform plan command again, and terraform will recreate it at the next apply.


#### The Terraform Taint command allows you to manually flag a resource as tainted, which means it will be destroyed and recreated on the next Terraform apply.

#### Terraform untaint allows you to remove that tainted condition from the resource.

Terraform represents this by marking the object as "tainted" in the Terraform state, and Terraform will propose to replace it in the next plan you create.




__________________________________________________________________________________________




#### Usage:

for example, if someone does a change manually on one resource, and we want the terraform to revert this change, we taint this resource, and it will be recreated on the next apply.




__________________________________________________________________________________________






```hcl
terraform taint aws_instance.my_vm_1
```



__________________________________________________________________________________________


#### terraform apply -replace=”<resource_name>”

How would you achieve the force replacement of a particular object even though there are no configuration changes? Choose the most appropriate option among the following:

Usage of terraform apply -replace=”<resource_name>” is preferred overterraform taint


__________________________________________________________________________________________
