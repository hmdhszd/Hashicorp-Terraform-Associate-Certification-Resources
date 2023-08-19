




Terraform Cloud, developed by HashiCorp, offers a centralized platform for managing Terraform code.

Key features include version control integration, secure variable storage, remote state management, and policy enforcement, enabling organizations to efficiently maintain control over their cloud infrastructure.



__________________________________________________________________________________________







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




Select the workflows that Terraform cloud utilizes to manage Terraform runs: 

UI/VCS-driven run workflow,

API-driven run workflow,

CLI-driven run workflow


__________________________________________________________________________________________





In the UI and VCS workflow, every workspace is associated with a specific branch of a VCS repo of Terraform configurations.



__________________________________________________________________________________________


#### Sentinel : policy as code framework

Sentinel Policies are rules which are enforced on Terraform runs to validate that the plan and corresponding resources are in compliance with company policies.

ex: checks if in the s3 bucket, encryption is enabled

`terraform plan` `-->` `sentinel checks` `-->` `terraform apply`

__________________________________________________________________________________________





Which feature is used to manage how members of your organization can use modules from the terraform private registry?    sentien policies



__________________________________________________________________________________________


In the UI and VCS workflow, every workspace is associated with a specific branch of a VCS repo of Terraform configurations.





__________________________________________________________________________________________


### Terraform Enterprise & Terraform Cloud

Terraform Enterprise provides several added advantage compared to Terraform Cloud.

Some of these include:

● Single Sign-On

● Auditing

● Private Data Center Networking

● Clustering

Team & Governance features are not available for Terraform Cloud Free (Paid)


__________________________________________________________________________________________




__________________________________________________________________________________________




__________________________________________________________________________________________




__________________________________________________________________________________________




__________________________________________________________________________________________




__________________________________________________________________________________________




__________________________________________________________________________________________

