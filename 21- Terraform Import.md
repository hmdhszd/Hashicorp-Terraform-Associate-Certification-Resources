
### Terraform Import:

#### import existing infrastructure into the Terraform configuration using Terraform import command

Terraform Import lets you target a resource that already exists, and map it to a resource you've defined in the code




__________________________________________________________________________________________



### First, we should create the block related to that resource:


```bash
resource "aws_instance" "jade-mw" {

}
```



__________________________________________________________________________________________



### Then, use the terraform import command:

by running this command, terraform will update the stats file and add the new resource.

```bash
terraform import aws_instance.jade-mw <id-of-the-resource>
```





__________________________________________________________________________________________


Here is the command to fetch the id of the resource:



```bash
aws ec2 describe-instances --endpoint http://aws:4566  --filters "Name=image-id,Values=ami-082b3eca746b12a89" | jq -r '.Reservations[].Instances[].InstanceId'
```



__________________________________________________________________________________________



### Finally, we should update the configuration file manually from the data of the stats:

You can use the jq tool to display the details of a specific resource instance from the terraform show command.

```bash
terraform show -json | jq '.values.root_module.resources[] | select(.type == "aws_instance" and .name == "jade-mw")'
```







### And define the required arguments to create this resource looks like the below:

```bash
resource "aws_instance" "jade-mw" {
  ami           = "ami-082b3eca746b12a89"
  instance_type = "t2.large"
  key_name      = "jade"
  tags = {
    Name = "jade-mw"
  }
```


__________________________________________________________________________________________





You intend to import two resources to your terraform configuration. You executed only the `terraform` `import` command until now and it worked. Will the `terraform` `apply` work if executed now?




It will throw an error,We haven’t updated the resource with correct argument values yet



__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






__________________________________________________________________________________________






