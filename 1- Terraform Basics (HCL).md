


a Resource is an object that Terraform manages it.


it could be a file, s3 bucket, virtual machine, ec2, DynamoDB, IAM user and Groups, Roles, Policies,...


a HCL file (.tf) consist of blocks and arguments,






__________________________________________________________________________________________


Example:

main.tf

```bash
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = "FIFA 21"
}
```



#### Block Type = resource

#### Resource Type = "local_file"

#### Provider = local

there are lots of providers such as AWS, GCP,...

each provider has a list of resources that can be created on that platform such as S3, DynamoDB,...

each resource has a list of required or optional arguments

#### Resource = file

#### Logical Name to identify the resource (can be anything) = games

#### Arguments = content / filename






__________________________________________________________________________________________






# terraform init:

### This command is used to initialize a new or existing Terraform configuration in a working directory. During initialization, Terraform downloads and installs the required providers and modules specified in the configuration.


```bash
iac-server $ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/local...
- Installing hashicorp/local v2.4.0...
- Installed hashicorp/local v2.4.0 (self-signed, key ID 34365D9472D7468F)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/plugins/signing.html

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, we recommend adding version constraints in a required_providers block
in your configuration, with the constraint strings suggested below.

* hashicorp/local: version = "~> 2.4.0"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```



__________________________________________________________________________________________

# terraform plan:

### After initialization, this command is used to create an execution plan. Terraform inspects the configuration files, compares the current state with the desired state, and generates a detailed plan of what actions (create, modify, delete) will be taken to achieve the desired configuration.


```bash
iac-server $ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.


------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.games will be created
  + resource "local_file" "games" {
      + content              = "FIFA 21"
      + content_base64sha256 = (known after apply)
      + content_base64sha512 = (known after apply)
      + content_md5          = (known after apply)
      + content_sha1         = (known after apply)
      + content_sha256       = (known after apply)
      + content_sha512       = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "/root/favorite-games"
      + id                   = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

Note: You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.
```

__________________________________________________________________________________________

# terraform apply:

### Once you review and approve the execution plan, you can apply it using this command. Terraform will then execute the planned actions, making the necessary changes to the infrastructure to match the desired state.



```bash
iac-server $ terraform apply

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.games will be created
  + resource "local_file" "games" {
      + content              = "FIFA 21"
      + content_base64sha256 = (known after apply)
      + content_base64sha512 = (known after apply)
      + content_md5          = (known after apply)
      + content_sha1         = (known after apply)
      + content_sha256       = (known after apply)
      + content_sha512       = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "/root/favorite-games"
      + id                   = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

local_file.games: Creating...
local_file.games: Creation complete after 0s [id=f68b901eb16aff12e9458bdb656a7df8d3425d4c]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

__________________________________________________________________________________________

##### In summary, terraform init sets up the environment, terraform plan creates an execution plan, and terraform apply applies the changes to the infrastructure. This process enables you to automate the creation and management of infrastructure resources in a consistent and reproducible manner.




```bash
iac-server $ ls -l /root/favorite-games

-rwxr-xr-x 1 root root 7 Jul 23 15:34 /root/favorite-games
```

__________________________________________________________________________________________

# terraform show:

### The terraform show command is used to display the current state of the infrastructure managed by Terraform.

### When you apply a Terraform configuration using terraform apply, it creates or modifies resources to match the desired state described in your configuration files.

### The current state of those resources is stored in a state file, typically named terraform.tfstate.



terraform.tfstate

```bash
iac-server $ ls
main.tf  terraform.tfstate


iac-server $ cat terraform.tfstate

{
  "version": 4,
  "terraform_version": "0.13.3",
  "serial": 1,
  "lineage": "1f40ce15-d9de-7979-f991-5f7a031c7d09",
  "outputs": {},
  "resources": [
    {
      "mode": "managed",
      "type": "local_file",
      "name": "games",
      "provider": "provider[\"registry.terraform.io/hashicorp/local\"]",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "content": "FIFA 21",
            "content_base64": null,
            "content_base64sha256": "0QatlfVl9H412mXNB5/Y9evwrDIxEW4ooJpmph2eoUY=",
            "content_base64sha512": "F0zLI9RS+tFB53xwISp1R3wvRQ/Sw4hsxwysWamsAk/cNyHr/X/pmmykTTCuvkRvr+3y+5c7Sc/J/ObRRX1mIg==",
            "content_md5": "44a271e06ddd134cdbeab299288422f3",
            "content_sha1": "f68b901eb16aff12e9458bdb656a7df8d3425d4c",
            "content_sha256": "d106ad95f565f47e35da65cd079fd8f5ebf0ac3231116e28a09a66a61d9ea146",
            "content_sha512": "174ccb23d452fad141e77c70212a75477c2f450fd2c3886cc70cac59a9ac024fdc3721ebfd7fe99a6ca44d30aebe446fafedf2fb973b49cfc9fce6d1457d6622",
            "directory_permission": "0777",
            "file_permission": "0777",
            "filename": "/root/favorite-games",
            "id": "f68b901eb16aff12e9458bdb656a7df8d3425d4c",
            "sensitive_content": null,
            "source": null
          }
        }
      ]
    }
  ]
}
```



__________________________________________________________________________________________




By default, when use trraform apply, the output will be shown on the screen.

in order to prevent this behavior, we should use "local_sensitive_file" resource type:


```bash
resource "local_sensitive_file" "games" {
  filename     = "/root/favorite-games"
  content  = "FIFA 21"
}
```



__________________________________________________________________________________________




# Destroy the resource


# terraform destroy




```bash
iac-server $ terraform destroy

local_sensitive_file.games: Refreshing state... [id=f68b901eb16aff12e9458bdb656a7df8d3425d4c]

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # local_sensitive_file.games will be destroyed
  - resource "local_sensitive_file" "games" {
      - content              = (sensitive value)
      - content_base64sha256 = "0QatlfVl9H412mXNB5/Y9evwrDIxEW4ooJpmph2eoUY=" -> null
      - content_base64sha512 = "F0zLI9RS+tFB53xwISp1R3wvRQ/Sw4hsxwysWamsAk/cNyHr/X/pmmykTTCuvkRvr+3y+5c7Sc/J/ObRRX1mIg==" -> null
      - content_md5          = "44a271e06ddd134cdbeab299288422f3" -> null
      - content_sha1         = "f68b901eb16aff12e9458bdb656a7df8d3425d4c" -> null
      - content_sha256       = "d106ad95f565f47e35da65cd079fd8f5ebf0ac3231116e28a09a66a61d9ea146" -> null
      - content_sha512       = "174ccb23d452fad141e77c70212a75477c2f450fd2c3886cc70cac59a9ac024fdc3721ebfd7fe99a6ca44d30aebe446fafedf2fb973b49cfc9fce6d1457d6622" -> null
      - directory_permission = "0700" -> null
      - file_permission      = "0700" -> null
      - filename             = "/root/favorite-games" -> null
      - id                   = "f68b901eb16aff12e9458bdb656a7df8d3425d4c" -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

local_sensitive_file.games: Destroying... [id=f68b901eb16aff12e9458bdb656a7df8d3425d4c]
local_sensitive_file.games: Destruction complete after 0s

Destroy complete! Resources: 1 destroyed.
```



__________________________________________________________________________________________
