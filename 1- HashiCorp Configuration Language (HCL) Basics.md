


a Resource is an object that Terraform manages it.


it could be a file, s3 bucket, virtual machine, ec2, DynamoDB, IAM user and Groups, Roles, Policies,...


a HCL tile (.tf) consist of blocks and arguments,






__________________________________________________________________________________________


Example:


```bash
resource "local_file" "foo" {
  content  = "This is the content inside the foo.bar file"
  filename = "${path.module}/foo.bar"
}
```



Block Type = resource

Resource Type = "local_file"

Provider = local

Resource = file

Logical Name to identify the resource (can be anything) = foo

Arguments = content / filename






__________________________________________________________________________________________






# terraform init: This command is used to initialize a new or existing Terraform configuration in a working directory. During initialization, Terraform downloads and installs the required providers and modules specified in the configuration.

# terraform plan: After initialization, this command is used to create an execution plan. Terraform inspects the configuration files, compares the current state with the desired state, and generates a detailed plan of what actions (create, modify, delete) will be taken to achieve the desired configuration.

# terraform apply: Once you review and approve the execution plan, you can apply it using this command. Terraform will then execute the planned actions, making the necessary changes to the infrastructure to match the desired state.

#### In summary, terraform init sets up the environment, terraform plan creates an execution plan, and terraform apply applies the changes to the infrastructure. This process enables you to automate the creation and management of infrastructure resources in a consistent and reproducible manner.

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
