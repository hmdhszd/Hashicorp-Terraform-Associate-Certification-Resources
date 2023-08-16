

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


?????

### What are the steps required to remove a resource from the management of terraform?    -lock=false



terraform apply -lock=false




__________________________________________________________________________________________



### What are the steps required to remove a resource from the management of terraform?

Use the terraform state rm command followed by manual removal of corresponding resources from the configuration file as well


__________________________________________________________________________________________




Areas of Terraform’s behavior that are not determined by the backend:    none!


__________________________________________________________________________________________



If supported by your backend, Terraform will lock your state for all operations that could write state. This prevents others from acquiring the lock and potentially corrupting your state.




__________________________________________________________________________________________






__________________________________________________________________________________________





__________________________________________________________________________________________





__________________________________________________________________________________________





__________________________________________________________________________________________


