



State Locking: when one person starts a change by using "terraform apply" command, the state file will be locked and no other one can use it.



Version control systems such as github cannot do State Locking, so we should store the state file in a "remote state backend"


like:

- AWS S3

- Terraform Cloud

- Google Cloud Storage

- HashiCorp Consul


by using a "remote state backend", it will get the state file before doing any changes, it will also upload it after doing the changes.


"Github is NOT a supported backend"

__________________________________________________________________________________________



to use S3 as the remote backend, we need S3 for the "Terraform State" and DynamoDB for the "State Locking"


```bash
terraform {
  backend "s3" {
    bucket = "mybucket"
    key    = "my-state-dir/terraform.tfstate"
    region = "us-east-1"
    dynamodb_table = "state-locking-table"
  }
}
```




__________________________________________________________________________________________


# Terraform State Commands:



### terraform state list

### terraform state list < resource-name >

The terraform state list command is used to list resources within a Terraform state.




__________________________________________________________________________________________


### terraform state show

### terraform state show  < Resource type > < resource-name > 




The state show command is used to display all the properties and their values of a specified resource in the key-value format. 


__________________________________________________________________________________________


### terraform state mv

### terraform state mv aws_instance.foo aws_instance.bar

The terraform state mv command moves resources from one state file to another.

You can also rename resources with mv .

The move command will update the resource in state, but not in your configuration file.



__________________________________________________________________________________________


### terraform state pull

This command is used to manually download the state file from remote state and output the raw format to stdout.

This command also works with local state.


__________________________________________________________________________________________



### terraform state push

This command is used to manually upload a local state file to remote state.



__________________________________________________________________________________________


### terraform state rm
 
"remove a resource from the management of terraform"


Terraform will search the state for any instances matching the given resource address, and remove the record of each one

so that Terraform will no longer be tracking the corresponding remote objects.



__________________________________________________________________________________________



What are the steps required to remove a resource from the management of terraform?

terraform state rm


__________________________________________________________________________________________


A requirement has come up which requires you to inspect the state file of terraform configuration. Your terraform script is already configured to work with the remote backend. Which of the following commands would you use to view a specific field in the state file?


terraform state pull


__________________________________________________________________________________________



You can `disable` `state` `locking` for most commands with the `-lock` flag but it is not recommended.


__________________________________________________________________________________________




Areas of Terraform’s behavior that are not determined by the backend: none



__________________________________________________________________________________________


### terraform init -migrate-state

After using Terraform locally to deploy cloud resources, you have decided to move your state file to an Amazon S3 remote backend. You configure Terraform with the proper configuration as shown below. What command should be run in order to complete the state migration while copying the existing state to the new backend?


__________________________________________________________________________________________
