


toset: Converts a list to a set






```bash
variable "my_list" {
  default = [1, 2, 2, 3, 3, 4, 5]
}

output "set_from_list" {
  value = toset(var.my_list)
}

```



__________________________________________________________________________________________





min: Returns the minimum value from a list of numbers




```bash
variable "my_numbers" {
  default = [42, 17, 99, 23, 8]
}

output "min_value" {
  value = min(var.my_numbers)
}

```



__________________________________________________________________________________________





max: Returns the maximum value from a list of numbers




```bash
variable "my_numbers" {
  default = [42, 17, 99, 23, 8]
}

output "max_value" {
  value = max(var.my_numbers)
}

```



__________________________________________________________________________________________





ceil: Rounds a number up to the nearest integer




```bash
variable "decimal_number" {
  default = 3.14
}

output "ceil_result" {
  value = ceil(var.decimal_number)
}

```



__________________________________________________________________________________________



floor: Rounds a number down to the nearest integer






```bash
variable "decimal_number" {
  default = 3.14
}

output "floor_result" {
  value = floor(var.decimal_number)
}

```



__________________________________________________________________________________________






split: Splits a string into a list using a delimiter



```bash
variable "csv_string" {
  default = "apple,banana,cherry,grape"
}

output "split_result" {
  value = split(",", var.csv_string)
}

```



__________________________________________________________________________________________




lower: Converts a string to lowercase





```bash
variable "mixed_case_string" {
  default = "Hello WoRLd"
}

output "lowercase_string" {
  value = lower(var.mixed_case_string)
}

```



__________________________________________________________________________________________





upper: Converts a string to uppercase




```bash
variable "mixed_case_string" {
  default = "Hello WoRLd"
}

output "uppercase_string" {
  value = upper(var.mixed_case_string)
}

```



__________________________________________________________________________________________




title: Converts the first letter of each word in a string to uppercase





```bash
variable "sentence" {
  default = "this is a title case example"
}

output "title_case_string" {
  value = title(var.sentence)
}

```



__________________________________________________________________________________________





substr: Extracts a substring from a string based on start index and length




```bash
variable "source_string" {
  default = "abcdefgh"
}

output "substring_result" {
  value = substr(var.source_string, 2, 3)
}

```



__________________________________________________________________________________________






join: Joins elements of a list into a string using a separator



```bash
variable "my_list" {
  default = ["apple", "banana", "cherry"]
}

output "joined_string" {
  value = join(", ", var.my_list)
}

```



__________________________________________________________________________________________





length: Returns the number of elements in a list or the length of a string




```bash
variable "my_list" {
  default = [1, 2, 3, 4, 5]
}

output "list_length" {
  value = length(var.my_list)
}

```



__________________________________________________________________________________________





index: Returns the index of a value in a list




```bash
variable "my_list" {
  default = ["apple", "banana", "cherry"]
}

output "index_of_banana" {
  value = index(var.my_list, "banana")
}

```



__________________________________________________________________________________________




element: Returns the nth element from a list





```bash
variable "my_list" {
  default = ["apple", "banana", "cherry"]
}

output "second_element" {
  value = element(var.my_list, 1)  # Indexing starts from 0
}

```



__________________________________________________________________________________________




contains: Checks if a list contains a specific value





```bash
variable "my_list" {
  default = ["apple", "banana", "cherry"]
}

output "contains_banana" {
  value = contains(var.my_list, "banana")
}

```



__________________________________________________________________________________________



keys: Returns a list of keys from a map






```bash
variable "my_map" {
  default = {
    key1 = "value1",
    key2 = "value2"
  }
}

output "map_keys" {
  value = keys(var.my_map)
}

```



__________________________________________________________________________________________



values: Returns a list of values from a map






```bash
variable "my_map" {
  default = {
    key1 = "value1",
    key2 = "value2"
  }
}

output "map_values" {
  value = values(var.my_map)
}

```



__________________________________________________________________________________________




lookup: Looks up a value in a map using a key





```bash
variable "my_map" {
  default = {
    key1 = "value1",
    key2 = "value2"
  }
}

output "lookup_value" {
  value = lookup(var.my_map, "key1")
}

```



__________________________________________________________________________________________
