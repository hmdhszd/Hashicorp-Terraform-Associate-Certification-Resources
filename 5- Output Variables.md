


### We can use output variables to organize data to be easily queried and shown back to the Terraform user.

### While Terraform stores hundreds or thousands of attribute values for all our resources, we are more likely to be interested in a few values of importance, such as a load balancer IP, VPN address, etc.



__________________________________________________________________________________________




main.tf

```bash
resource "random_uuid" "id1" {
   
}
resource "random_uuid" "id2" {
   
}
resource "random_uuid" "id3" {
   
}
resource "random_uuid" "id4" {
   
}
resource "random_uuid" "id5" {
   
}
resource "random_uuid" "id6" {
   
}
resource "random_uuid" "id7" {
   
}
resource "random_integer" "order1" {
  min     = 1
  max     = 99999
 
}
resource "random_integer" "order2" {
  min     = 1
  max     = 222222
 
}
```




# we use "output" block type

output.tf


```bash
output "id1" {
   value = random_uuid.id1.result
}
output "id2" {
    value = random_uuid.id2.result
   
}
output "id3" {
    value = random_uuid.id3.result
   
}

output "id4" {
    value = random_uuid.id4.result
   
}
output "id5" {
    value = random_uuid.id5.result
}
   
output "id6" {
    value = random_uuid.id6.result
   
}
output "id7" {
    value = random_uuid.id7.result
   
}
output "order1" {
 value = random_integer.order1.result
 
}
output "order2" {
 value = random_integer.order1.result
 
}
```



__________________________________________________________________________________________




to see the output use "terraform output" command:

```bash
iac-server $ terraform output

id1 = a3449786-c28b-2617-8833-e80d74f0505b
id2 = 228acb50-efb1-7caf-5358-6024d8d5cc1e
id3 = 02138440-0bdb-dbc5-eed9-1b7fd1ab43d4
id4 = 6ca56342-b4c4-f2c1-3af4-cc98059b89e8
id5 = 322b4ebb-81a3-6e16-aba0-807d5c08151d
id6 = 083af532-dcd5-ee3f-2ad6-d7e9b053bfb6
id7 = f3fc7369-bebe-5cd1-0e73-bfa5df4509d4
order1 = 75392
order2 = 75392
```



__________________________________________________________________________________________



#### another example:


```bash
resource "local_file" "welcome" {
    filename = "/root/message.txt"
    content = "Welcome to Kodekloud."
}

output "welcome_message" {
  value = local_file.welcome.content
}
```



__________________________________________________________________________________________


```bash

iac-server $ terraform output welcome_message

Welcome to Kodekloud.
```



__________________________________________________________________________________________



Running the "terraform plan" will NOT render outputs

Running the “terraform apply” will render the output variables defined

Running the “terraform output” will render the output variables defined


__________________________________________________________________________________________


Choose the suitable option that could be used to access one of the module’s output values:


module.[MODULE NAME].[OUTPUT NAME]





__________________________________________________________________________________________




## splat expression


```bash
resource "aws_instance" "example" {
  count         = 5
  ami           = "ami-12345678"
  instance_type = "t2.micro"

  tags = {
    Name = "Example Instance ${count.index}"
  }
}

output "instance_public_ips" {
  value = aws_instance.example[*].public_ip
}
```


__________________________________________________________________________________________


