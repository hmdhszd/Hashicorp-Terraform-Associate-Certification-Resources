

# Terraform State

#### The primary purpose of Terraform state is to store bindings between objects in a remote system and resource instances declared in your configuration.


after running the "terraform apply" command for the first time, one JSON file will be created: terraform.tfstate

it has the complete state of the resources that created by terraform.


and the output of the command "terraform show" comes from the "terraform.tfstate" file


__________________________________________________________________________________________




main.tf

```bash
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = "FIFA 21"
}
```



__________________________________________________________________________________________






```bash
iac-server $ terraform show

# local_file.games:
resource "local_file" "games" {
    content              = "FIFA 21"
    content_base64sha256 = "0QatlfVl9H412mXNB5/Y9evwrDIxEW4ooJpmph2eoUY="
    content_base64sha512 = "F0zLI9RS+tFB53xwISp1R3wvRQ/Sw4hsxwysWamsAk/cNyHr/X/pmmykTTCuvkRvr+3y+5c7Sc/J/ObRRX1mIg=="
    content_md5          = "44a271e06ddd134cdbeab299288422f3"
    content_sha1         = "f68b901eb16aff12e9458bdb656a7df8d3425d4c"
    content_sha256       = "d106ad95f565f47e35da65cd079fd8f5ebf0ac3231116e28a09a66a61d9ea146"
    content_sha512       = "174ccb23d452fad141e77c70212a75477c2f450fd2c3886cc70cac59a9ac024fdc3721ebfd7fe99a6ca44d30aebe446fafedf2fb973b49cfc9fce6d1457d6622"
    directory_permission = "0777"
    file_permission      = "0777"
    filename             = "/root/favorite-games"
    id                   = "f68b901eb16aff12e9458bdb656a7df8d3425d4c"
}
```



__________________________________________________________________________________________



### What are the steps required to remove a resource from the management of terraform?

Use the terraform state rm command followed by manual removal of corresponding resources from the configuration file as well


__________________________________________________________________________________________




Areas of Terraform’s behavior that are not determined by the backend:    none!


__________________________________________________________________________________________



If supported by your backend, Terraform will lock your state for all operations that could write state. This prevents others from acquiring the lock and potentially corrupting your state.




__________________________________________________________________________________________





#### force-unlock Manually unlock the state for the defined configuration


```bash
terraform force-unlock [options] LOCK_ID
```

__________________________________________________________________________________________



By default, Terraform does not provide the ability to mask secrets in the Terraform plan and state files regardless of what provider you are using.



__________________________________________________________________________________________

### `terraform plan -refresh-only`

The terraform plan -refresh-only command is used to create a plan whose goal is only to `update` the `Terraform` `state` to match any changes made to remote objects outside of Terraform.


__________________________________________________________________________________________


### `.gitignore`

### Which of the following Terraform files should be ignored by Git when committing code to a repo? 




`.terraform` directory

`terraform.tfstate` and `terraform.tfstate.backup`


`.tfvars` files

`*.tfplan` files

__________________________________________________________________________________________





### state encryption

- `local state`, state is stored in `plain-text` JSON files

- `Terraform Cloud`, state is alwasys `encrypted` at-rest




__________________________________________________________________________________________




## You can run `terraform init` over and over again and it will NOT create/change your state file.


__________________________________________________________________________________________



 ####  these backends support `state` `locking`


- Kubernetes

- Consul

- S3 / DynamoDB


but local backend does not support state locking

__________________________________________________________________________________________




Terraform `State` File can be `encrypted` on `S3` (it is not encrypted on S3 by default)

Terraform `State` File is always `encrypted` on `Terraform Cloud` 


__________________________________________________________________________________________



In both `Terraform OSS` and `Terraform Cloud`, workspaces provide similar functionality of using a `separate` `state` `file` for each workspace.







__________________________________________________________________________________________







What allows Terraform to make use of a declarative approach?    state file




__________________________________________________________________________________________





when you want to delete all the resources except one of them,

you should remove that one resource from terraform by this command:  `terraform` `state` `rm`

then destroy the rest of the infrastructure:  `terraform` `destroy`


__________________________________________________________________________________________

