




Workspaces are technically equivalent to renaming your state file.

Terraform then includes a set of protections and support for remote state.

Workspaces are also meant to be a shared resource.

They are not private, unless you use purely local state and do not commit your state to version control.



__________________________________________________________________________________________





with Terraform Workspaces, we can use the same configuration directory, to create multiple environment infrastructure.



__________________________________________________________________________________________




with Terraform Workspaces, we can have `multiple` `state` `files` of a `single` `configuration`.



__________________________________________________________________________________________

`multiple` `workspaces`, `different` `environment` `variable` for each workspace

__________________________________________________________________________________________






```bash
project/
├── main.tf
├── variables.tf
```





variables.tf

```bash
variable "ami" {
  description = "Map of AMIs for different projects"
  type        = map(string)
  default = {
    ProjectA = "ami-xxxxxxxxxxxxxxxxx"  # Replace with actual AMI IDs
    ProjectB = "ami-yyyyyyyyyyyyyyyyy"
  }
}
```


main.tf

```bash
provider "aws" {
  region = "us-west-2"  # Update with your desired AWS region
}

resource "aws_instance" "ec2_instance" {
  ami           = lookup(var.ami, terraform.workspace)
  instance_type = "t2.micro"
  tags = {
    Name = "EC2 Instance"
  }
}
```



__________________________________________________________________________________________




### Create a new workspace


```bash
terraform workspace new ProjectA
```


```bash
terraform workspace new ProjectB
```

once we create a workspace, Terraform will immidietely switch to it.


__________________________________________________________________________________________



### list workspaces


```bash
terraform workspace list

default
ProjectA
* ProjectB

```



__________________________________________________________________________________________



### Select and apply configuration on a specific terraform workspace


```bash
terraform workspace select ProjectA
terraform apply
```



```bash
terraform workspace select ProjectB
terraform apply
```



__________________________________________________________________________________________




when using workspaces, we will have a directory called "terraform.tfstate.d" for the state files:

terraform.tfstate.d/<workspace_name>

```bash
terraform.tfstate.d/
├── default.tfstate
├── ProjectA
│   └── terraform.tfstate
└── ProjectB
    └── terraform.tfstate
```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________




`Each` `Terraform` `workspace` uses its own `state` `file` to manage the infrastructure associated with that particular workspace.



__________________________________________________________________________________________





Within your Terraform configuration, how can you include the name of the current workspace?    ${terraform.workspace}



__________________________________________________________________________________________



### default workspace


This workspace cannot be deleted.

It is the default workspace.


__________________________________________________________________________________________




Terraform worksoace is Not suitable for isolation for strong separation between workspace (stage/prod)



__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






