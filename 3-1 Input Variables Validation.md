



## Strings

String may not contain character

Scenario: String may not contain a /


```bash
variable "string_may_not_contain" {
  type = string
  default = "test"

  validation {
    error_message = "Value cannot contain a \"/\"."
    condition = !can(regex("/", var.string_may_not_contain))
  }
}
```



__________________________________________________________________________________________



## String with valid options

Scenario: Here we have a string and we only allow to values "approved" or "disapproved".

I show 2 examples of the same check using different methods:


```bash
variable "string_only_valid_options" {
  type = string
  default = "approved"

  # using regex
  validation {
    condition     = can(regex("^(approved|disapproved)$", var.string_only_valid_options))
    error_message = "Invalid input, options: \"approved\", \"disapproved\"."
  }

  # using contains()
  validation {
    condition     = contains(["approved", "disapproved"], var.string_only_valid_options)
    error_message = "Invalid input, options: \"approved\", \"disapproved\"."
  }
}
```



__________________________________________________________________________________________



## Valid AWS Region Name

Scenario: string must be like AWS region



```bash
variable "string_like_aws_region" {
  type = string
  default = "us-east-1"

  validation {
    condition     = can(regex("[a-z][a-z]-[a-z]+-[1-9]", var.string_like_aws_region))
    error_message = "Must be valid AWS Region names."
  }
```



__________________________________________________________________________________________



## Valid IAM Role Name

Scenario: Your string must be a valid IAM role name


```bash
variable "string_valid_iam_role_name" {
    type = string
    default = "MyCoolRole"
    # arn example: "arn:aws:iam::123456789012:role/MyCoolRole"

    validation {
      condition     = can(regex("^[a-zA-Z][a-zA-Z\\-\\_0-9]{1,64}$", var.string_valid_iam_role_name))
      error_message = "IAM role name must start with letter, only contain letters, numbers, dashes, or underscores and must be between 1 and 64 characters."
    }
}
```



__________________________________________________________________________________________



## Valid IPv4 CIDR



```bash
variable "string_like_valid_ipv4_cidr" {
  type    = string
  default = "10.0.0.0/16"

  validation {
    condition     = can(cidrhost(var.string_like_valid_ipv4_cidr, 0))
    error_message = "Must be valid IPv4 CIDR."
  }
}
```



__________________________________________________________________________________________



## Semantic Version



```bash
variable "semv1" {
  default = "10.57.123"

  validation {
    error_message = "Must be valid semantic version."
    condition     = can(regex("^(0|[1-9]\\d*)\\.(0|[1-9]\\d*)\\.(0|[1-9]\\d*)(?:-((?:0|[1-9]\\d*|\\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\\.(?:0|[1-9]\\d*|\\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\\+([0-9a-zA-Z-]+(?:\\.[0-9a-zA-Z-]+)*))?$", var.semv1))
  }
}
```



__________________________________________________________________________________________



## Number within a range

Scenario: number must be between 1-16


```bash
variable "num_in_range" {
  type        = number
  default     = 1

  validation {
    condition     = var.num_in_range >= 1 && var.num_in_range <= 16 && floor(var.num_in_range) == var.num_in_range
    error_message = "Accepted values: 1-16."
  }
}
```



__________________________________________________________________________________________



## Valid ami Name


```bash
variable "ami_id" {
    type = string

    validation {
    condition = (
        length(var.ami_id) > 4 &&
        substr(var.ami_id, 0, 4) == "ami-"
    )
    error_message = "The ami_id value must start with \"ami-\"."
    }
}
```



__________________________________________________________________________________________
