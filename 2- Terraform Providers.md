



you can find terraform providers here:    https://registry.terraform.io/browse/providers


with the "terraform init" command, the terraform provider plugins will be installed.

these plugins will be downloaded in the ".terraform/plugins" in the current working directory



ex:

```bash
* hashicorp/local: version = "~> 2.4.0"
```

Orgazinational Namespace: hashicorp (registry.terraform.io/hashicorp/local)

Type: local




__________________________________________________________________________________________

we can have multiple terraform files (.tf)

when we use, "terraform apply" command ,terraform will use all the .tf files within the current directory

Also, we can have one single configuration file that contains all the resource blocks required to provision the infrastructure. for example:  main.tf

other configuration files can be created for specific reasons like: main.tf , variables.tf , providers.tf , output.tf




