


### if (If the variable is true)

In this example, the count parameter is conditionally set based on the value of the variable create_web_servers.

If the variable is true, three instances of type "t2.micro" will be created; otherwise, no instances will be created.

```bash
# Example: Conditional Expression - "count"
resource "aws_instance" "web_servers" {
  count = var.create_web_servers ? 3 : 0

  instance_type = "t2.micro"
  ami           = "ami-0c55b159cbfafe1f0"
  subnet_id     = aws_subnet.public.id
}
```



__________________________________________________________________________________________



### for_each

Here, the resource block for creating AWS security groups uses the for_each expression.

If the variable create_security_groups is true, the security groups will be created based on the rules defined in the security_group_rules map;

otherwise, no security groups will be created.

```bash
# Example: Conditional Expression - "for_each"
resource "aws_security_group" "firewall_rules" {
  for_each = var.create_security_groups ? var.security_group_rules : {}

  name_prefix = "firewall-"
  
  # Other security group configuration...
}
```



__________________________________________________________________________________________



### if

In this example, an AWS S3 bucket is created conditionally using the if expression.

If the variable use_private_bucket is true, a bucket named "private-bucket" will be created;

otherwise, the bucket creation will be skipped by setting the value to null.

```bash
# Example: Conditional Expression - "if"
resource "aws_s3_bucket" "private_bucket" {
  bucket = var.use_private_bucket ? "private-bucket" : null

  # Other bucket configuration...
}
```



__________________________________________________________________________________________




### coalesce

In this scenario, the coalesce function is used to set the TTL value for a Route 53 record.

If the variable custom_domain_ttl is set, it will be used as the TTL;

otherwise, the default value of 3600 will be used.

```bash
# Example: Conditional Expression - "coalesce"
resource "aws_route53_record" "custom_domain" {
  zone_id = aws_route53_zone.main.zone_id
  name    = var.custom_domain_name
  type    = "A"
  ttl     = coalesce(var.custom_domain_ttl, 3600)

  # Other record configuration...
}
```



__________________________________________________________________________________________



### contains

In this example, the AMI ID for the instance is conditionally determined using the contains function.

If the variable use_monitoring_ami is true and the monitoring_ami_ids list contains the specified AMI ID, that AMI ID will be used;

otherwise, a fallback AMI ID is used.

```bash
# Example: Conditional Expression - "contains"
resource "aws_instance" "monitoring_instance" {
  instance_type = "t2.micro"
  ami           = var.use_monitoring_ami && contains(var.monitoring_ami_ids, "ami-12345678") ? "ami-12345678" : "ami-87654321"

  # Other instance configuration...
}
```



__________________________________________________________________________________________
