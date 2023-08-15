# 3 ways of setting the  "access_key" and "secret_key"


for connect terraform to AWS, we need to set the "access_key" and "secret_key"


__________________________________________________________________________________________


### 1- we can have it inside our configuration file as a "provider" block:



main.tf

```bash
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}
```



__________________________________________________________________________________________


### 2- or we can have another hidden file for store the credentials called: ".aws/config/credentials"

.aws/config/credentials

```bash
[default]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```



__________________________________________________________________________________________



### 3- we can use the environment variables as well:



```bash
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=us-west-2
```



__________________________________________________________________________________________
