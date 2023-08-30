


# Data sources    -->    `data` block


Data sources allow Terraform to read attributes from resources which are provisioned outside its control.



the "data" block only reads the infrastructure,

but "resource" block create,update,destroy infrastructure

__________________________________________________________________________________________



### Data Block --> retrieve information about existing resources

__________________________________________________________________________________________


Example:

we want to get the data of the file that is already created "without terraform" and put its content into an output variable called "os-version":

```bash

data "local_file" "os" {
  filename = "/etc/os-release"
}

output "os-version" {
  value = data.local_file.os.content
}

```



__________________________________________________________________________________________


Example:


a data source that will be used to read data of an existing S3 bucket

```bash
data "aws_s3_bucket" "selected" {
  bucket = "bucket.test.com"
}
```



__________________________________________________________________________________________



data rource with filter:

```bash
data "aws_ec2_transit_gateway" "tgw" {
  filter {
    name   = "tag:Name"
    values = ["wahlnetwork-tgw-prod"]
  }
}
```



__________________________________________________________________________________________




### Terraform Data Sources:

Data sources are used to query and fetch information about existing resources in your infrastructure environment.

They allow you to access attributes of resources that are already created outside of Terraform, like information from cloud providers or other systems.

Data sources provide input values for your Terraform configuration, helping you make informed decisions when creating or configuring resources.



__________________________________________________________________________________________




### Terraform Import Command:

The terraform import command is used to `bring` existing resources `into` `Terraform's` `management`.

It allows you to include resources that were created manually or through other means into your Terraform configuration, making them part of your infrastructure as code setup.

Importing resources helps Terraform understand the existing state of those resources, allowing you to further manage and modify them using Terraform.

Before importing, you need to define the resource in your Terraform configuration, After importing you need to to align its desired state with the actual state.


__________________________________________________________________________________________




In summary, data sources fetch information about existing resources, while the terraform import command adds existing resources to be managed by Terraform, enabling you to manage them consistently using your Terraform configuration.





__________________________________________________________________________________________


Data resources have the different dependency resolution behavior as defined for managed resources    -->    FALSE

__________________________________________________________________________________________

The behavior of `local-only` data sources is the `same` as all other data sources,

but their result data exists only `temporarily` during a Terraform operation,

and is `re-calculated` each time a `new plan` is created.

__________________________________________________________________________________________

Resources declared using `data block` are known as `data resource`s.

Resources declared by a `resource block` are known as `managed resources`.

`Managed resources` are often referred to just as `resources` when the meaning is clear from context.

__________________________________________________________________________________________




Each data source in turn belongs to a provider.



__________________________________________________________________________________________



#### output variable  -->  `output` block

#### data source      -->  `data` block


__________________________________________________________________________________________


