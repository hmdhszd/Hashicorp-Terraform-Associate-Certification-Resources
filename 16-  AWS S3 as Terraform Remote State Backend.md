



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
