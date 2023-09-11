


## terraform validate

to check if the `syntax` is correct

```hcl
iac-server $ terraform validate

Error: Unsupported argument

  on main.tf line 8, in resource "tls_private_key" "private_key":
   8:   dsa_bits  = 2048

An argument named "dsa_bits" is not expected here. Did you mean "rsa_bits"?
```

```hcl
iac-server $ terraform validate

Success! The configuration is valid.
```



__________________________________________________________________________________________




Which configuration inconsistency errors does terraform validate report?




declaring resources identifier more than once



__________________________________________________________________________________________







## terraform fmt

The terraform fmt command is used to rewrite Terraform configuration files to a canonical format and style.

to improve readability



## terraform fmt -recursive


you can use the -recursive flag to instruct terraform fmt to also process files in subdirectories.

__________________________________________________________________________________________



## terraform show

## terraform show -json

shows the current state of the infra as seen by terraform

to see terraform attributes after creation of a resource, use "terraform show"


__________________________________________________________________________________________



## terraform providers

to see all the providers used in the current configuration directory


```hcl
iac-server $ terraform providers 

Providers required by configuration:
.
├── provider[registry.terraform.io/hashicorp/local]
└── provider[registry.terraform.io/hashicorp/aws]
```



__________________________________________________________________________________________



## terraform output

to see all output variables in the configuration directory

```hcl
iac-server $ terraform output

id1 = a3449786-c28b-2617-8833-e80d74f0505b
order1 = 75392
```



__________________________________________________________________________________________



## terraform refresh

sync terraform with the real-world infrastructure (it will only update the state file NOT the infrastructure)

the command `terraform refresh` is called automatically with `terraform plan` and `terraform apply` command





__________________________________________________________________________________________



What is not processed when running a terraform refresh?



Configuration file




__________________________________________________________________________________________







The `terraform apply -refresh-only` command creates a plan whose goal is `only` to `update` the `Terraform` `state` and any root module output values to match changes made to remote objects outside of Terraform.



__________________________________________________________________________________________




## terraform console

The Terraform console is an interpreter that you can use to evaluate Terraform expressions and explore your Terraform project's state. 

In order to use the terraform console command, the `CLI` must be able to `lock state` to prevent changes.

```hcl
$ terraform console
Acquiring state lock. This may take a few moments...
> 
```

__________________________________________________________________________________________

## terraform login

The terraform login command can be used to automatically obtain and save an API token for Terraform Cloud, Terraform Enterprise, or any other host that offers Terraform services.

__________________________________________________________________________________________





## terraform graph ( ‍`.DOT format` )

create a visual representation of the dependencies in a terraform configuration or execution plan.

```hcl
iac-server $ terraform graph
digraph {
        compound = "true"
        newrank = "true"
        subgraph "root" {
                "[root] local_file.key_data (expand)" [label = "local_file.key_data", shape = "box"]
                "[root] provider[\"registry.terraform.io/hashicorp/local\"]" [label = "provider[\"registry.terraform.io/hashicorp/local\"]", shape = "diamond"]
                "[root] provider[\"registry.terraform.io/hashicorp/tls\"]" [label = "provider[\"registry.terraform.io/hashicorp/tls\"]", shape = "diamond"]
                "[root] tls_cert_request.csr (expand)" [label = "tls_cert_request.csr", shape = "box"]
                "[root] tls_private_key.private_key (expand)" [label = "tls_private_key.private_key", shape = "box"]
                "[root] local_file.key_data (expand)" -> "[root] provider[\"registry.terraform.io/hashicorp/local\"]"
                "[root] local_file.key_data (expand)" -> "[root] tls_private_key.private_key (expand)"
                "[root] meta.count-boundary (EachMode fixup)" -> "[root] tls_cert_request.csr (expand)"
                "[root] provider[\"registry.terraform.io/hashicorp/local\"] (close)" -> "[root] local_file.key_data (expand)"
                "[root] provider[\"registry.terraform.io/hashicorp/tls\"] (close)" -> "[root] tls_cert_request.csr (expand)"
                "[root] root" -> "[root] meta.count-boundary (EachMode fixup)"
                "[root] root" -> "[root] provider[\"registry.terraform.io/hashicorp/local\"] (close)"
                "[root] root" -> "[root] provider[\"registry.terraform.io/hashicorp/tls\"] (close)"
                "[root] tls_cert_request.csr (expand)" -> "[root] local_file.key_data (expand)"
                "[root] tls_private_key.private_key (expand)" -> "[root] provider[\"registry.terraform.io/hashicorp/tls\"]"
        }
}
```



__________________________________________________________________________________________




### Every terraform command listed is useful for inspecting infrastructure:

- terraform output


- terraform graph


- terraform show


- terraform state list


- terraform state show





__________________________________________________________________________________________


### FIRST, run terraform init  -->  THEN, run terraform validate

to validate a Terraform configuration using the terraform validate command, it's important to FIRST, run terraform init in order to set up the necessary dependencies and initialize the configuration directory.





__________________________________________________________________________________________



Certainly, here's a concise description of each command in two lines:

1. **`terraform fmt`**: Automatically formats Terraform code for consistent layout, **`improving readability`** by adjusting indentation and spacing as per the style guide.

2. **`terraform validate`**: Checks Terraform configuration files for **`syntax errors`** and verifies the correctness of references to providers and modules, helping prevent invalid configurations.


__________________________________________________________________________________________


What is the significance of -chdir option in terraform?


It instructs Terraform to change its working directory to the given directory before running the given subcommand.


__________________________________________________________________________________________
