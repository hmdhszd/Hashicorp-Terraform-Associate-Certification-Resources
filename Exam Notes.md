



The terraform refresh command is used to reconcile the state Terraform knows about (via its state file) with the real-world infrastructure.

This can be used to detect any drift from the last-known state and to update the state file. This does not modify infrastructure, but does modify the state file.



__________________________________________________________________________________________



the refresh command is automatically issued by the "terraform plan" command.

The -refresh=false option is used in normal planning mode to skip the default behavior of refreshing Terraform state before checking for configuration changes.

CLI:

terraform plan -refresh=false

OR

terraform apply -refresh=false




__________________________________________________________________________________________




state file keeps the dependency between the resources


__________________________________________________________________________________________



state lock in terraform


If supported by your backend, Terraform will lock your state for all operations that could write state.

This prevents others from doing changes and potentially corrupting your state.

State locking happens automatically on all operations that could write state.


__________________________________________________________________________________________


### Configuration drift

Configuration drift in Terraform refers to the situation where changes are made directly to resources in your cloud environment, bypassing Terraform.

This causes a mismatch between the actual state of resources and what Terraform expects.

It can lead to confusion, inconsistencies, and difficulties in managing your infrastructure.

To prevent configuration drift, always make changes through Terraform and regularly audit for any discrepancies.

This helps maintain a reliable and predictable infrastructure.


__________________________________________________________________________________________


### Immutable infrastructure

Immutable infrastructure in Terraform involves creating new instances of resources instead of modifying existing ones.

It ensures reliability, consistency, and easy management by automating changes through code and enabling easy rollbacks.

It's about treating infrastructure components as disposable and replaceable entities, making updates predictable and scalable.


__________________________________________________________________________________________




"In-place updates" mean making changes directly to existing resources. It's different from the "immutable" approach that creates new instances for changes.


__________________________________________________________________________________________







__________________________________________________________________________________________



### output variable  -->  `output` block

### data source      -->  `data` block





__________________________________________________________________________________________




__________________________________________________________________________________________
