


### First, we create a key pair to connect to the ec2 instance.

the file "terraform-demo.pub" is previously created.




```bash
resource "aws_key_pair" "terraform-demo" {
  key_name   = "terraform-demo"
  public_key = "${file("terraform-demo.pub")}"
}
```



### Then create a security group to give permission to the ec2.



```bash
resource "aws_security_group" "ec2_sg" {
  name        = "allow_http"
  description = "Allow http and ssh traffic"
  vpc_id      = data.aws_vpc.GetVPC.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port       = 0
    to_port         = 0
    protocol        = "-1"
    cidr_blocks     = ["0.0.0.0/0"]
  }
  tags = {
    Name = "terraform-ec2-security-group"
  }
}

```




### Finally create the ec2 with the "key_name" and "vpc_security_group_ids" configuration:


```bash
resource "aws_instance" "my-instance" {
	ami = "ami-04169656fea786776"
	instance_type = "t2.nano"
	key_name = "${aws_key_pair.terraform-demo.key_name}"
	vpc_security_group_ids = [aws_security_group.ec2_sg.id]
	user_data = << EOF
		#! /bin/bash
		sudo apt-get update
		sudo apt-get install -y apache2
		sudo systemctl start apache2
		sudo systemctl enable apache2
		echo "<h1>Deployed via Terraform</h1>" | sudo tee /var/www/html/index.html
	EOF
	tags = {
		Name = "Terraform"	
		Batch = "5AM"
	}
}
```









__________________________________________________________________________________________



we can get the public IP of the machine for further uses:



```bash
output "publicip" {
  value  =  aws_instance.my-instance.public_ip
}
```



__________________________________________________________________________________________

##

AWS user_data is the set of commands/data you can provide to a instance at launch time.

if it's already run, and you add user_data, it will not be applied on the instance.

