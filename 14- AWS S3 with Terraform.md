



First, create a bucket:


```bash
resource "aws_s3_bucket" "finance" {
  bucket  = "finanace-21092020"
  tags    =  {
    Description  =  "Finance and Payroll"
  }
}
```



upload a file to the created S3 bucket:


```bash
resource "aws_s3_bucket_object" "finance-2020" {
  content  =  "/root/finance/finance-2020.doc"
  key  =  "finance-2020.doc"
  bucket  =  aws_s3_bucket.finance.id
}
```



the the info of the previously created "iam group":


```bash
data "aws_iam_group" "finance-data" {
  group_name  =  "finance-analysts"
}
```





create a bucket policy and give access to the group members to the bucket:



```bash
resource "aws_s3_bucket_policy" "finance-policy" {
  bucket  =  aws_s3_bucket.finance.id
  policy  =  <<EOF


  {
    "Version": "2012-10-17",
    "Statement": [
    {
      "Action": “*",
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::${aws_s3_bucket.finance.id}/*",
      "Principal": {
        "AWS": [
          "${data.aws_iam_group.finance-data.arn}"
        ]
      }
    }
    ]
  }


EOF
}
```



__________________________________________________________________________________________
