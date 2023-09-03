


#### In Terraform, an alias is a feature that allows you to define multiple instances of the same provider configuration with different settings.

#### It provides a way to manage multiple environments, regions, or profiles within a single Terraform configuration.

```hcl
  provider = <PROVIDER NAME>.<ALIAS>
```
__________________________________________________________________________________________



Example:


```hcl
provider "aws" {
  alias  = "us_east"
  region = "us-east-1"
}

provider "aws" {
  alias  = "us_west"
  region = "us-west-2"
}

resource "aws_s3_bucket" "bucket_us_east" {
  provider = aws.us_east
  bucket   = "my-bucket-us-east"
  acl      = "private"
}

resource "aws_s3_bucket" "bucket_us_west" {
  provider = aws.us_west
  bucket   = "my-bucket-us-west"
  acl      = "private"
}

```



__________________________________________________________________________________________



### Roger is implementing Terraform in production. He realized that every region in AWS has a different AMI ID for CentOS 7 OS. He wants to create a Terraform code that works for all the regions. He has already created the EC2 resource but needs to figure on how he can deal with different AMI IDs based on regions? What is the best approach?


create a `map` of the `REGION` to `AMI ID`



__________________________________________________________________________________________


