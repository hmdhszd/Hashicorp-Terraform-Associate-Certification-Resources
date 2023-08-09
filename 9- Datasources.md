



Data sources allow Terraform to read attributes from resources which are provisioned outside its control.


we use "data" block,

"data" block only reads the infrastructure, but "resource" block create,update,destroy infrastructure




__________________________________________________________________________________________


Example:

we want to get the data of the file that is already created "without terraform" and put its content into an output variable called "os-version":

```bash
output "os-version" {
  value = data.local_file.os.content
}
data "local_file" "os" {
  filename = "/etc/os-release"
}
```



__________________________________________________________________________________________


Example:


a data source that will be used to read data of an existing s3 bucket

```bash
data "aws_s3_bucket" "selected" {
  bucket = "bucket.test.com"
}
```



__________________________________________________________________________________________



data rource with filter:

```bash
data "aws_ec2_transit_gateway" "tgw" {
  filter {
    name   = "tag:Name"
    values = ["wahlnetwork-tgw-prod"]
  }
}
```



__________________________________________________________________________________________





