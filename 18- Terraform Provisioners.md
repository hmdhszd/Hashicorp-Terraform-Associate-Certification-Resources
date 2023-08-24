#### Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction.

__________________________________________________________________________________________

# 1- remote-exec Provisioner:

## The remote-exec provisioner invokes a script on a remote resource after it is created. This can be used to run a configuration management tool, bootstrap into a cluster, etc.

but there should be a network connectivity between the local machine and the instance. (`SSH` for Linux / `WINRM` for Windows)

so we make use of a AWS security group.

also, we need an AWS ssh key pair for authentication to the machine. and we use connection block







__________________________________________________________________________________________



### First, we create a security group


```bash
resource "aws_security_group" "allow_ssh" 
  name        = "tf_Remote_Provisioner"
  description = "Allow SSH Inbound Traffic"


  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
    description = "Run http server"
  }


  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
    description = "Enable  SSh"
  }


  # Outboud Rule for SG
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
  tags = {
    Name = "Rempote_Provisioner"
  }
}
```



__________________________________________________________________________________________



### Then, create a key to connect to the machine


```bash
resource "aws_key_pair" "web" {
  key_name   = "web"
  public_key = tls_private_key.oskey.public_key_openssh
}
```



__________________________________________________________________________________________






```bash
resource "aws_instance" "my_ec2" 
  ami                    = "ami-0e742cca61fb65051"
  instance_type          = "t2.micro"
  key_name               = aws_key_pair.web.id
  vpc_security_group_ids = [aws_security_group.allow_ssh.id]


  # Connect with AWS Resources
  connection {
    type        = "ssh"
    user        = "ec2-user"
    host        = self.public_ip
    private_key = file("root/.ssh/web")
  }


  # Remote Provisioner for User Data
  provisioner "remote-exec" {
    inline = [
      "sudo yum install -y httpd.x86_64",
      "sudo systemctl start httpd.service",
      "sudo  systemctl enable httpd.service",
      "sudo chmod -R 777 /var/www/html",
      "sudo  echo “User Data Installed by Terraform $(hostname -f)” >> /var/www/html/index.html"
    ]
  }

 tags = {
    Name = "Remote_Provisioner"
  }
}
```



__________________________________________________________________________________________




# 2- local-exec Provisioner:

## The local-exec provisioner invokes a local executable after a resource is created.

## This invokes a process on the machine running Terraform, not on the resource. Basically, this provisioner is used when you want to perform some tasks onto your local machine where you have installed the terraform.




__________________________________________________________________________________________




we can store the IP address of the created instance in a file (private_ip.txt) on our local machine

```bash
resource "aws_instance" "my_vm" {
 ami           = var.ami //Amazon Linux AMI
 instance_type = var.instance_type
 
 provisioner "local-exec" {
   command = "echo ${self.private_ip} >> private_ip.txt"
 }
 
 tags = {
   Name = var.name_tag,
 }
}
```



__________________________________________________________________________________________



write on a file when the instance is created or destroyed


```bash
resource "aws_instance" "my_vm" {
 ami           = var.ami //Amazon Linux AMI
 instance_type = var.instance_type
 
 provisioner "local-exec" {
   command = "echo 'Creation is successful.' >> creation.txt"
 }
 
 provisioner "local-exec" {
   when = destroy
   command = "echo 'Destruction is successful.' >> destruction.txt"
 }
 
 tags = {
   Name = var.name_tag,
 }
}
```



__________________________________________________________________________________________



# 3- file Provisioner:

## The file provisioner is used to copy files or directories from the machine executing Terraform to the newly created resource.

The file provisioner supports both ssh and winrm type connections.



__________________________________________________________________________________________




install nginx on the machine using file provisioner and remote_exec privisioner:

```bash
resource "aws_instance" "my_vm" {
 ami           = var.ami //Amazon Linux AMI
 instance_type = var.instance_type
 
 key_name        = "tfsn"
 security_groups = [aws_security_group.http_access.name]
 
 provisioner "file" {
   source      = "./installnginx.sh"
   destination = "/home/ec2-user/installnginx.sh"
 }
 
 provisioner "remote-exec" {
   inline = [
     "chmod 777 ./installnginx.sh",
     "./installnginx.sh"
   ]
 }
 
 connection {
   type        = "ssh"
   host        = self.public_ip
   user        = "ec2-user"
   private_key = file("./tfsn.cer")
   timeout     = "4m"
 }
 
 tags = {
   Name = var.name_tag,
 }
}
```



__________________________________________________________________________________________




in the provisioners, we can use "when" and "on_failure"

if running the command is not important for us, we use: on_failure = continue, otherwise we use on_failure = fail

If when = destroy is specified, the provisioner will run when the resource it is defined within is destroyed.





__________________________________________________________________________________________






What happens when provisioners fail to execute successfully?

it will taint the resource and that will be replaced on the next run







__________________________________________________________________________________________




Provisioner Block --> nested block inside the resource block


__________________________________________________________________________________________



## Creation-Time Provisioner:


Creation-time provisioners are only run during creation, not during updating or any other lifecycle

If a creation-time provisioner fails, the resource is marked as tainted.

__________________________________________________________________________________________


## Destroy-Time Provisioner

Destroy provisioners are run before the resource is destroyed.


__________________________________________________________________________________________



__________________________________________________________________________________________







