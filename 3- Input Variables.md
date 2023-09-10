

### We can have our variables in a separate file (like: variables.tf) and refer to them with a "var." prefix

ex: var.aws_region

__________________________________________________________________________________________


main.tf

```hcl
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "ec2_instance" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_pair_name
}

output "public_ip" {
  value = aws_instance.ec2_instance.public_ip
}
```



__________________________________________________________________________________________

variables.tf

if we don't define the "default" value, it will ask us to enter in manually at the moment of issue the command "terraform apply"

```hcl
variable "aws_region" {
  description = "The AWS region where the EC2 instance will be created."
  default     = "us-west-2"
}

variable "ami_id" {
  description = "The ID of the Amazon Machine Image (AMI) for the EC2 instance."
  default     = "ami-0c55b159cbfafe1f0"  # Replace this with your desired AMI ID
}

variable "instance_type" {
  description = "The instance type for the EC2 instance."
  default     = "t2.micro"
}

variable "key_pair_name" {
  description = "The name of the key pair to associate with the EC2 instance."
  default     = "my-key-pair"  # Replace this with the name of your key pair
}
```



__________________________________________________________________________________________



## in the variable block, the "Type", "Description" and "Default" arguments are optional


Type: string, number, bool, list(string), list(number), map(string), set(number), object, tuple

Default Type: any

__________________________________________________________________________________________

## Variable Types:

####  - `tuple` (different variable type)

####  - `list` (same variable type)

####  - `set` (no duplicate values)

####  - `string`

####  - `bool`

####  - `object`

####  - `map`

####  - `number`


"float" is NOT a valid variable type

__________________________________________________________________________________________


## string

```hcl
# Declaring a string variable
variable "string_var" {
  type        = string
  description = "A string variable"
  default     = "Hello, Terraform!"
}
```
__________________________________________________________________________________________

## number

```hcl
# Declaring a number variable
variable "number_var" {
  type        = number
  description = "A number variable"
  default     = 42
}
```
__________________________________________________________________________________________

## bool

```hcl
# Declaring a boolean variable
variable "bool_var" {
  type        = bool
  description = "A boolean variable"
  default     = true
}
```

__________________________________________________________________________________________

## list(string)

```hcl
# Declaring a list variable
variable "list_var" {
  type        = list(string)
  description = "A list of strings variable"
  default     = ["item1", "item2", "item3"]
}
```



```hcl
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = var.list_var[0]
}
```
__________________________________________________________________________________________

## map(string)

```hcl
# Declaring a map variable
variable "map_var" {
  type        = map(string)
  description = "A map of strings variable"
  default     = {
    key1 = "value1"
    key2 = "value2"
    key3 = "value3"
  }
}
```



```hcl
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = var.map_var[key1]
}
```

__________________________________________________________________________________________

## map(number)

```hcl
# Declaring a map variable
variable "map_var" {
  type        = map(number)
  description = "A map of number variable"
  default     = {
    key1 = "100"
    key2 = "400"
    key3 = "3123"
  }
}
```

__________________________________________________________________________________________

## set(number)


the difference between set and list is that in the set we cannot have duplicate values.


```hcl
# Declaring a set variable
variable "set_var" {
  type        = set(number)
  description = "A set of numbers variable"
  default     = [1, 2, 3]
}
```
__________________________________________________________________________________________

## object

```hcl
# Declaring an object variable
variable "object_var" {
  type = object({
    name    = string
    age     = number
    is_male = bool
  })
  description = "An object variable"
  default = {
    name    = "John Doe"
    age     = 30
    is_male = true
  }
}
```
__________________________________________________________________________________________

## tuple

the difference between tuple and list is that a list uses elements of the same variable type, but in tuple, we can use `different` `variable` `types`


```hcl
# Declaring a tuple variable
variable "tuple_var" {
  type        = tuple([string, number, bool])
  description = "A tuple variable"
  default     = ["tuple_value", 123, false]
}

```

__________________________________________________________________________________________
__________________________________________________________________________________________

## sensitive variable: (sensitive = true)

Here's an example:

In this example, db_password is a sensitive variable. The sensitive attribute ensures that Terraform will treat this variable as sensitive and hide its value in the console output.

- it will be saved in the State file clear text!

```hcl
variable "db_password" {
  description = "The password for the database"
  type = string
  sensitive = true
}
```


__________________________________________________________________________________________



# other methods of use variables

*** set explicit values for the current working directory that will `override` the `default` `variable` values

__________________________________________________________________________________________



### use environment variables ( `TF_VAR_< variable name >` )

set the environment variable before apply 

```hcl
export TF_VAR_filename="/root/pets.txt"

terraform apply
```



__________________________________________________________________________________________


### Automatically loaded

### - `terraform.tfvars`

### - `terraform.tfvars.json`

### - `*.auto.tfvars`

### - `*.auto.tfvars.json`

it will be added `automatically`

```hcl
terraform apply
```



__________________________________________________________________________________________



### use separate variable file ( `*.tfvars` OR `*.tfvars.json` )

it should be added `manually` by `-var-file`

```hcl
terraform apply -var-file variables.tfvars
```



__________________________________________________________________________________________



### use variables in command line

it should be added `manually` by `-var`

```hcl
terraform apply -var "filename=/root/pets.txt"
```



__________________________________________________________________________________________

### Variable Input:

When using Terraform with remote backends, such as Terraform Cloud or AWS S3, you can input variable values through the backend's interface.

__________________________________________________________________________________________



## The Order of Precedence

#### 1. `Environment` `variables`

#### 2. `terraform.tfvars` OR `terraform.tfvars.json`

#### 3. `*.auto.tfvars` OR `*.auto.tfvars.json`

#### 4. Any `-var` and `-var-file` options on the `command line`


__________________________________________________________________________________________



A variable name or a label must be unique within the same "module" or "configuration"





__________________________________________________________________________________________

### Here are some examples of invalid variable names:

- Names that start with a number: 1_invalid_variable_name

- Names that contain spaces or special characters (space) (other than underscores): invalid variable name

- Names that contain only numbers: 12345

- Names that are the same as Terraform reserved words, such as var, module, data, count, etc.



__________________________________________________________________________________________


### Invalid variable names:

We can use any name for a variable except for:


-  source

-  version

-  providers

-  count

-  for_each

-  lifecycle

-  depends_on

-  locals


__________________________________________________________________________________________


### `Manage` `Secrets` (Credentials)

Which among the following are the techniques that could be used to safely and securely `manage` `secrets` inside terraform?



- `Secret` `Stores` (e.g., `Vault`, `AWS Secrets manager`)

- `Encrypted` `Files` (e.g., `KMS`, PGP, SOPS)

- Store Terraform `state` in a `backend` that `supports` `encryption`.

- `Environment` `Variables`



__________________________________________________________________________________________




When configuring a remote backend in Terraform, it might be a good idea to purposely omit some of the required arguments to ensure `secrets` and other relevant data are not inadvertently shared with others. 

What alternatives are available to provide the remaining values to Terraform to initialize and communicate with the remote backend?

#### With a partial configuration, the remaining configuration arguments must be provided as part of the initialization process. There are several ways to supply the remaining arguments:

- `Command-line` `key/value` pairs: To specify a single key/value pair, when running terraform init.

- `Interactively` on the `command line`: Terraform will interactively ask you for the required values unless interactive input is disabled.

- `File` (`-backend-config=PATH`): To specify a configuration file, use the -backend-config=PATH option when running terraform init.


*** do NOT use Vault

__________________________________________________________________________________________


#### `null` --> `default value`

if you put a terraform variable as "null", terraform will ommit this value and use default value instead of that.



__________________________________________________________________________________________


the porrisble values for "number" type: 10 10000 19.2323

__________________________________________________________________________________________


James  has created a variable and has explicitly defined the type as a string. Following is the snippet:

```hcl
variable "myvar" {
  type = string
}
```


Which of the following value will be accepted?


`"2"`    -->    is accepted


`2`    -->    is `NOT` accepted




__________________________________________________________________________________________



The safest method to inject sensitive variables into your Terraform run in a CI/CD pipeline is:

- Pass variables to Terraform with a -var flag.








__________________________________________________________________________________________


