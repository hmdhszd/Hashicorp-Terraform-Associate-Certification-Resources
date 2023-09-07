



user_create.tf


```hcl
terraform {

required_providers {

    aws = {

    source  = "hashicorp/aws"

    version = "~> 3.27"

    }

  }

}

```
```hcl

provider "aws" {

  region    = "us-west-1"

  access_key = "user_access_key"

  secret_key = "user_secret"

}

```
```hcl


resource "aws_iam_user" "new_user" {

  name = "NewUserExample"

}

```
```hcl


resource "aws_iam_access_key" "AccK" {

  user = aws_iam_user.new_user.name

}

```
```hcl


output "secret_key" {

  value = aws_iam_access_key.AccK.secret

  sensitive = true

}

```
```hcl


output "access_key" {

  value = aws_iam_access_key.AccK.id

}

```
```hcl



resource "aws_iam_user_policy" "iam" {

  name = "ListBuckets"

  user = aws_iam_user.new_user.name

  policy = <<EOF

{

    "Version": "2022-1-6",

    "Statement": [

    {

    "Effect": "Allow",

    "Action": "s3:ListAllMyBuckets",

    "Resource": "*"

    }

    ]

}

EOF

}
```



__________________________________________________________________________________________
