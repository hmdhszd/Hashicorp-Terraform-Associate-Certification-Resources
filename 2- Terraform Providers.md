


## Terraform Providers:

- official: owned by HashiCorp

  * hashicorp/local
 
    organization --> hashicorp
    
    type         --> local

  there can be hostname as well

- partner: owned by a third-party company (reviewed and tested by HashiCorp)

- community: publish and contribute by individual contributers








__________________________________________________________________________________________


`Terraform Privider` = `Terraform Plugin`

__________________________________________________________________________________________


you can find terraform providers here at `terraform registry`:    https://registry.terraform.io/browse/providers


with the `terraform init` command, the terraform `provider` `plugins` will be `installed`.

these plugins will be downloaded in the `.terraform/providers` in the current working directory



ex:

```bash
* hashicorp/local: version = "~> 2.4.0"
```

Orgazinational Namespace: hashicorp (registry.terraform.io/hashicorp/local)

Provider: local




__________________________________________________________________________________________

we can have multiple terraform files (.tf)

when we use, "terraform apply" command ,terraform will use all the .tf files within the current directory

Also, we can have one single configuration file that contains all the resource blocks required to provision the infrastructure. for example:  main.tf

other configuration files can be created for specific reasons like: main.tf , variables.tf , providers.tf , output.tf






__________________________________________________________________________________________



### terraform providers mirror


Terraform Providers Mirror is a feature that allows organizations to host a local copy of external providers' plugins, enhancing control and reliability in infrastructure provisioning through Terraform.


The terraform providers mirror command downloads the providers required for the current configuration and copies them into a directory in the local filesystem.

In normal use, terraform init will automatically download needed providers from provider registries as part of initializing the current working directory.





__________________________________________________________________________________________



The terraform providers ______ command can automatically populate a directory that will be used as a local filesystem mirror in the provider installation configuration.



terraform providers mirror


__________________________________________________________________________________________


### terraform providers schema

The terraform providers schema command is used to `print detailed schemas` for the `providers used` in the current configuration.


__________________________________________________________________________________________



### terraform providers lock

Terraform provider locking involves specifying a specific `version` of a provider in your configuration, ensuring stability and predictability by preventing automatic provider updates.

This helps maintain consistent infrastructure management.



__________________________________________________________________________________________




#### When you run terraform apply, you see an error that states - “Failed to instantiate provider”. What could be the reason for this error?

the used provider was not initilized for the configuration

__________________________________________________________________________________________



#### Select the reasons why we may need to specify the `provider’s argument`?



To use `multiple configurations` of the `same provider` ???????????????

To change the `default` `Provider` `Configurations`


__________________________________________________________________________________________

### There are two reasons to use a `Provider` `Argument` in the Configuration.


1. To `override` the `default` `provider` `configuration`.

For example, the default configuration may be to deploy resources in the "us-east-1" region.

If the requirement is to deploy resources in a different region, we can use the provider argument to override the default.


2. In some cases, a configuration may need to use `multiple` `versions` of the `same` `provider`.

For example - a resource that deploys to the "us-east-1" and another resource within the same configuration that deploys to the "us-west-2" region.




*** to use multiple versions of the same provider NOT multiple configurations of the same provider ???????????????



__________________________________________________________________________________________

#### Choose the easiest way to list the versions of all installed plugins in terraform along with terraform versions


```bash
terraform version
```


__________________________________________________________________________________________


### Plugin-based architecture


Providers use a ______-based architecture that is available for most infrastructure platforms within the public Terraform registry.




__________________________________________________________________________________________



### Version of a provider:

in this example it can be 1.0.0 1.0.1 1.0.2 1.0.3 ...

```hcl
terraform {
  required_providers {
    aws = "~> 1.0.0"
  }
}
```




__________________________________________________________________________________________


`Multiple` `providers` can be declared within a `single` Terraform configuration `file`.


__________________________________________________________________________________________


#### What function does the `terraform init -upgrade` command perform?



upgrade all previously-selected plugins to the `newest` (`latest`) available version that complies with the configuration's version constraints.




__________________________________________________________________________________________


#### how add `credentials` to access the API for the underlying platform, such as VMware, AWS, or Google Cloud?


- in the `provider` `block` by hardcoding or using variable


- `integrated` `services`: AWS IAM, Azure Managed Service Identity


- `Environment` `Variable`


__________________________________________________________________________________________



where can you `install` `providers` from?

- Terraform Public or Private `registry`

- Official HashiCorp Releases `Site`

- `Local` Plugins `Directory`

- Terraform `Plugin` `Cache`


__________________________________________________________________________________________



Official Terraform providers and modules are owned and maintained by HashiCorp.


__________________________________________________________________________________________


You want to upgrade the provider version to the latest acceptable one. What is the approach to do it?

specify new version of provider under terraform block, then issue terraform init.



__________________________________________________________________________________________




