


## terraform validate

to check if the syntax is correct

```bash
iac-server $ terraform validate

Error: Unsupported argument

  on main.tf line 8, in resource "tls_private_key" "private_key":
   8:   dsa_bits  = 2048

An argument named "dsa_bits" is not expected here. Did you mean "rsa_bits"?
```

```bash
iac-server $ terraform validate

Success! The configuration is valid.
```



__________________________________________________________________________________________




## terraform fmt

The terraform fmt command is used to rewrite Terraform configuration files to a canonical format and style.

to improve readability


```bash

```



__________________________________________________________________________________________



## terraform show

## terraform show -json

shows the current state of the infra as seen by terraform

```bash

```



__________________________________________________________________________________________



## terraform providers

to see all the providers used in the current configuration directory


```bash
iac-server $ terraform providers 

Providers required by configuration:
.
├── provider[registry.terraform.io/hashicorp/local]
└── provider[registry.terraform.io/hashicorp/aws]
```



__________________________________________________________________________________________



## terraform output

to see all output variables in the configuration directory

```bash

```



__________________________________________________________________________________________



## terraform refresh

sync terraform with the real-world infrastructure (it will only update the state file NOT the infrastructure)

the command "terraform refresh" is called automatically with "terraform plan" and "terraform apply" command

```bash

```



__________________________________________________________________________________________




## terraform graph

create a visual representation of the dependencies in a terraform configuration or execution plan.

```bash
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
