




Workspaces are technically equivalent to renaming your state file.

Terraform then includes a set of protections and support for remote state.

Workspaces are also meant to be a shared resource.

They are not private, unless you use purely local state and do not commit your state to version control.



__________________________________________________________________________________________




with Terraform Workspaces, we can use the `same` `configuration` `directory`, to create `multiple` `environment` infrastructure.



__________________________________________________________________________________________




with Terraform Workspaces, we can have `multiple` `state` `files` of a `single` `configuration`.



__________________________________________________________________________________________

`multiple` `workspaces`, `different` `environment` `variable` for each workspace

__________________________________________________________________________________________






```hcl
project/
├── main.tf
├── variables.tf
```





variables.tf

```hcl
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

```hcl
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






### Roger is implementing Terraform in production. He realized that every region in AWS has a different AMI ID for CentOS 7 OS. He wants to create a Terraform code that works for all the regions. He has already created the EC2 resource but needs to figure on how he can deal with different AMI IDs based on regions? What is the best approach?


create a `map` of the `REGION` to `AMI ID`



__________________________________________________________________________________________





### Create a `new` workspace


```hcl
terraform workspace new ProjectA
```


```hcl
terraform workspace new ProjectB
```

once we create a `NEW` `workspace`, Terraform will immidietely switch to it.


__________________________________________________________________________________________



### `list` all workspaces


```hcl
terraform workspace list

default
ProjectA
* ProjectB

```



__________________________________________________________________________________________



### `select` and apply configuration on a specific terraform workspace


```hcl
terraform workspace select ProjectA

terraform apply
```



```hcl
terraform workspace select ProjectB

terraform apply
```



__________________________________________________________________________________________



### `show` current workspace


```hcl
terraform workspace show
ProjectB
```



__________________________________________________________________________________________





when using workspaces, we will have a directory called "terraform.tfstate.d" for the state files:

`terraform.tfstate.d`/`<workspace_name>`/`terraform.tfstate`

```hcl
terraform.tfstate.d/
├── default.tfstate
├── ProjectA
│   └── terraform.tfstate
└── ProjectB
    └── terraform.tfstate
```



__________________________________________________________________________________________




`Each` `Terraform` `workspace` uses its own `state` `file` to manage the infrastructure associated with that particular workspace.



__________________________________________________________________________________________



### `${terraform.workspace}`

Within your Terraform configuration, how can you include the name of the current workspace?    ${terraform.workspace}



__________________________________________________________________________________________



### default workspace


This workspace cannot be deleted.

It is the default workspace.


__________________________________________________________________________________________




Terraform worksoace is Not suitable for isolation for strong separation between workspace (stage/prod)



__________________________________________________________________________________________



In the `UI` and `VCS` workflow, `every workspace` is associated with a `specific branch` of a VCS repo of Terraform configurations.



__________________________________________________________________________________________





