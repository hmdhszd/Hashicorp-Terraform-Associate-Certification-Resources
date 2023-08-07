


#### In Terraform, an alias is a feature that allows you to define multiple instances of the same provider configuration with different settings.

#### It provides a way to manage multiple environments, regions, or profiles within a single Terraform configuration.



__________________________________________________________________________________________



Example:


```bash
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
