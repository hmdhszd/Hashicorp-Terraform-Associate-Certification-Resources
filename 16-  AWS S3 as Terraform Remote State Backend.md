



State Locking: when one person starts a change by using "terraform apply" command, the state file will be locked and no other one can use it.



Version control systems such as github cannot do State Locking, so we should store the state file in a "remote state backend"


like:

- AWS S3

- Terraform Cloud

- Google Cloud Storage

- HashiCorp Consul


by using a "remote state backend", it will get the state file before doing any changes, it will also upload it after doing the changes.


__________________________________________________________________________________________



to use S3 as the remote backend, we need S3 for the "Terraform State" and DynamoDB for the "State Locking"


```bash
terraform {
  backend "s3" {
    bucket = "mybucket"
    key    = "my-state-dir/terraform.tfstate"
    region = "us-east-1"
  }
}
```




__________________________________________________________________________________________

# Terraform State Commands:



### terraform state list

### terraform state list <resource-name>

The terraform state list command is used to list resources within a Terraform state.




__________________________________________________________________________________________


### terraform state show

### terraform state show <resource-name> 




The state show command is used to display all the properties and their values of a specified resource in the key-value format. The complete command format is terraform state show <Resource type>. <Resource name> . The state pull command is used to display data in the current state.



__________________________________________________________________________________________


### terraform state mv

terraform state mv aws_instance.foo aws_instance.bar

The terraform state mv command moves resources from one state file to another. You can also rename resources with mv . The move command will update the resource in state, but not in your configuration file.



__________________________________________________________________________________________


### terraform state pull

This command will download the state from its current location and output the raw format to stdout. 

__________________________________________________________________________________________



### terraform state push

terraform state push: The terraform state push command is used to manually upload a local state file to remote state.



__________________________________________________________________________________________


### terraform state rm
 


terraform state rm [options] ADDRESS... Terraform will search the state for any instances matching the given resource address, and remove the record of each one so that Terraform will no longer be tracking the corresponding remote objects.



__________________________________________________________________________________________
