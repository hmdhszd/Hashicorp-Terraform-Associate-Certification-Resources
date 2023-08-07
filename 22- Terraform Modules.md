

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



in the Terraform Registry, you can find 2 types of modules:

- Verified Modules (have verified checkmark beside it's name)

- Community Modules


__________________________________________________________________________________________




#### Terraform get

we use this command to download the modules from the registry


__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________







```bash

```



__________________________________________________________________________________________







```bash

```



__________________________________________________________________________________________







```bash

```



__________________________________________________________________________________________
