

### We can have our variables in a separate file (variables.tf) and refer to them with a "var." prefix

ex: var.aws_region

__________________________________________________________________________________________


main.tf

```bash
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

```bash
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



## in the variable block, Type and Description are optional


Type: string, number, bool, list(string), list(number), map(string), set(number), object, tuple

Default Type: any

__________________________________________________________________________________________

## string

```bash
# Declaring a string variable
variable "string_var" {
  type        = string
  description = "A string variable"
  default     = "Hello, Terraform!"
}
```
__________________________________________________________________________________________

## number

```bash
# Declaring a number variable
variable "number_var" {
  type        = number
  description = "A number variable"
  default     = 42
}
```
__________________________________________________________________________________________

## bool

```bash
# Declaring a boolean variable
variable "bool_var" {
  type        = bool
  description = "A boolean variable"
  default     = true
}
```

__________________________________________________________________________________________

## list(string)

```bash
# Declaring a list variable
variable "list_var" {
  type        = list(string)
  description = "A list of strings variable"
  default     = ["item1", "item2", "item3"]
}
```



```bash
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = var.list_var[0]
}
```
__________________________________________________________________________________________

## map(string)

```bash
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



```bash
resource "local_file" "games" {
  filename     = "/root/favorite-games"
  content  = var.map_var[key1]
}
```

__________________________________________________________________________________________

## map(number)

```bash
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


```bash
# Declaring a set variable
variable "set_var" {
  type        = set(number)
  description = "A set of numbers variable"
  default     = [1, 2, 3]
}
```
__________________________________________________________________________________________

## object

```bash
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

the difference between a tuple and a list is that list is list uses elements of the same variable type, but in tuple, we can use different variable types


```bash
# Declaring a tuple variable
variable "tuple_var" {
  type        = tuple([string, number, bool])
  description = "A tuple variable"
  default     = ["tuple_value", 123, false]
}

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________






```bash

```



__________________________________________________________________________________________
