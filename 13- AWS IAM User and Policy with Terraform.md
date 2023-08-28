



user_create.tf


```bash
terraform {

required_providers {

    aws = {

    source  = "hashicorp/aws"

    version = "~> 3.27"

    }

  }

}

```
```bash

provider "aws" {

  region    = "us-west-1"

  access_key = "user_access_key"

  secret_key = "user_secret"

}

```
```bash


resource "aws_iam_user" "new_user" {

  name = "NewUserExample"

}

```
```bash


resource "aws_iam_access_key" "AccK" {

  user = aws_iam_user.new_user.name

}

```
```bash


output "secret_key" {

  value = aws_iam_access_key.AccK.secret

  sensitive = true

}

```
```bash


output "access_key" {

  value = aws_iam_access_key.AccK.id

}

```
```bash



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
