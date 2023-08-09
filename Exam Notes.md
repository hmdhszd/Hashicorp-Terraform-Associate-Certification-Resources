IAC:

1- Configuration Managements: Ansible, Chef, Puppet, SALTSTACK

2- Server Templating: Docker, HashiCorp Packer, HashiCorp Vagrant

3- Provisioning Tools: HashiCorp Terraform, CloudFormation


* We can use "Configuration Managements" tools to provision infrastructure.



__________________________________________________________________________________________




A resource is an object that Terraform manages


__________________________________________________________________________________________




terraform init:

checks the config files, inside the working directory, lists the providers used in the list, and will download the plugin

after running this command, the plugins will be downloaded to ".terraform/plugins" directory


__________________________________________________________________________________________



terraform plan:

shows the plan of all the actions that will be done by terraforming



__________________________________________________________________________________________




terraform apply:

applies the configurations (needs approval)

we can also use: terraform apply -auto-approve


__________________________________________________________________________________________



terraform show:

show the details of the resource that is created (uses state file)



__________________________________________________________________________________________





Terraform Providers:

- official: owned by HashiCorp

  * hashicorp/local
 
    organization --> hashicorp
    
    type         --> local

  there can be hostname as well

- partner: owned by a third-party company (reviewed and tested by HashiCorp)

- community: publish and contribute by individual contributers







__________________________________________________________________________________________



specify the version in the "required_providers" block

terraform {
  required_providers {
    mycloud = {
      source = "mycorp/mycloud"
      version = "~> 1.0" 
    }
  }
}


__________________________________________________________________________________________



The "terraform providers" command shows information about the provider requirements of the configuration in the current working directory. 


__________________________________________________________________________________________





The functionality of a provider plugin may vary drastically from one version to another.

Our terraform configuration may not work as expected when using a version different than the one it was written in.

As a best practice, always declare the exact version of the provider we want to use within the "required_providers" block.


__________________________________________________________________________________________


* see the version of providers:


The "terraform version" command provides the version of terraform as well as the version of the provider plugins that are downloaded in the configuration directory.

For example, the below command shows that the version of aws provider is v3.69.0 and that of local provider is v2.1.0

iac-server $ terraform version Terraform v0.13.3 + provider registry.terraform.io/hashicorp/aws v3.69.0 + provider registry.terraform.io/hashicorp/local v2.1.0


__________________________________________________________________________________________




What allows Terraform to make use of a declarative approach?  state file



__________________________________________________________________________________________




if we change an argument in a resource, after next apply, the resource will re replaced (recreated)



__________________________________________________________________________________________




terraform plan: display the blueprint of the infrastructure to be applied



__________________________________________________________________________________________



Immutable Infrastructure:

Immutable infrastructure is another paradigm in which it ensures that resources are never modified after they have been deployed.

If a change is to be made, a new instance of that resource will be provisioned in place of the old one.



__________________________________________________________________________________________



Ansible:

Ansible makes use of a procedural approach.

This means that an Ansible playbook should specifically contain all the steps needed to achieve a task.



__________________________________________________________________________________________



terraform apply -auto-approve

Skips interactive approval of the plan before applying.

This option is ignored when you pass a previously-saved plan file, because Terraform considers you passing the plan file as the approval and so will never prompt in that case.


__________________________________________________________________________________________




Terraform can be installed on all major Linux Distributions, Windows, MacOS, Solaris and OpenBSD.


__________________________________________________________________________________________


When you run terraform apply, you see an error that states - “Failed to instantiate provider”. What could be the reason for this error?




 a "terraform init" command was not run to download the provider plugin for the provider.


__________________________________________________________________________________________



There are two reasons to use a provider argument in the configuration.

1. To override the default provider configuration.

For example, the default configuration may be to deploy resources in the "us-east-1" region.

If the requirement is to deploy resources in a different region, we can use the provider argument to override the default.


2. In some cases, a configuration may need to use multiple versions of the same provider.

For example - a resource that deploys to the "us-east-1" and another resource within the same configuration that deploys to the "us-west-2" region.




*** to use multiple versions of the same provider NOT multiple configurations of the same provider


__________________________________________________________________________________________



The "terraform providers" command shows information about the provider requirements of the configuration in the current working directory. 



__________________________________________________________________________________________



terraform init:  will downloads the latest version of the provider plugins



__________________________________________________________________________________________


Version constraints:

1- required_providers

2- required_version

3- modules

Version constraints can be used anywhere terraform allows us to specify versions.

Most commonly they can be set at:

1. Within the provider version configuration (Inside the required_providers block nested inside the terraform block)

2. The "required_version" argument which is used to set the version of Terraform to use.

3. Within modules. This is where we specify the version of module to be used.



__________________________________________________________________________________________


plugin-based

Providers use a ______-based architecture that is available for most infrastructure platforms within the public Terraform registry.



__________________________________________________________________________________________


 " , "

version = ">= 1.2.0, < 2.0.0"


A version constraint is a string literal containing one or more conditions, which are separated by commas. 


__________________________________________________________________________________________




when using version constraints, we can use:


- pessimistic operator

- "!=" operator

- "~>" operator

- combination comparison operation to use specific version within a range

- comparison operator




__________________________________________________________________________________________




A variable name or a label must be unique within the same module or configuration


__________________________________________________________________________________________



we can NOT use "providers" as a variable name.



__________________________________________________________________________________________




The variable block begins with the "variable" keyword followed by a user defined name/label for the variable.


__________________________________________________________________________________________



to see terraform attributes after creation of a resource, use "terraform show"



__________________________________________________________________________________________




Resource targeting in Terraform is a feature that allows you to apply changes to only a subset of your infrastructure, instead of applying the entire plan at once.


terraform plan -target aws_instance.web -target module.network



__________________________________________________________________________________________



Terraform resources and data sources make all of their arguments available as readable attributes,

and also typically export additional read-only attributes.



__________________________________________________________________________________________


local-only

The behavior of __________ data sources is the same as all other data sources, but their result data exists only temporarily during a Terraform operation, and is re-calculated each time a new plan is created.



__________________________________________________________________________________________




The behavior of local-only data sources is the same as all other data sources, but their result data exists only temporarily during a Terraform operation, and is re-calculated each time a new plan is created.


__________________________________________________________________________________________




The terraform_remote_state data source uses the latest state snapshot from a specified state backend to retrieve the root module output values from some other Terraform configuration. You can use the terraform_remote_state data source without requiring or configuring a provider.



__________________________________________________________________________________________




A data source can be created using the data block.



__________________________________________________________________________________________




Each data source in turn belongs to a provider.



__________________________________________________________________________________________



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







__________________________________________________________________________________________







__________________________________________________________________________________________







__________________________________________________________________________________________







__________________________________________________________________________________________







__________________________________________________________________________________________
