




Terraform Cloud, developed by HashiCorp, offers a centralized platform for managing Terraform code.

Key features include version control integration, secure variable storage, remote state management, and policy enforcement, enabling organizations to efficiently maintain control over their cloud infrastructure.



__________________________________________________________________________________________




What feature of Terraform Cloud allows you to publish and maintain a set of `custom` `modules` which can be used within your organization? `Private` `Module` `Registry`


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





## Sentinel




### Policy Enforcement:

Sentinel and OPA enable you to define and enforce policies that govern the configurations and changes made to your infrastructure. You can create custom policies tailored to your organization's needs, ensuring compliance with regulatory requirements, security best practices, and internal standards.

### Automated Governance:

With Sentinel and OPA, you can implement automated governance and compliance checks in your Terraform workflows. This means that every time changes are proposed or applied, Sentinel or OPA evaluates those changes against the defined policies, automatically preventing non-compliant configurations from being deployed.

### Enhanced Security:

By incorporating Sentinel or OPA into your Terraform Cloud environment, you can bolster your infrastructure security. Sentinel can flag and block any potentially risky configurations, helping to minimize security vulnerabilities and ensuring that only approved, secure changes are allowed.

### Version-controlled Policies:

Sentinel and OPA policies are defined as code, which means they can be stored in version control alongside your Terraform configurations. This allows your policies to be managed, reviewed, and updated through the same version control system, improving collaboration and maintaining a history of policy changes.

### Custom Approval Workflows:

You can create customized approval workflows based on policy conditions using Sentinel or OPA. This means that changes to the infrastructure can be automatically approved or flagged for manual review, depending on the defined policies, ensuring tighter control over infrastructure modifications.

### Preventing Costly Mistakes:

Sentinel and OPA policies can help catch potential mistakes or misconfigurations before they impact your infrastructure. By running policy checks in real-time, you can identify issues early on and avoid costly downtime or unexpected behavior caused by incorrect configurations.

### Consistency and Best Practices:

Utilizing Sentinel/OPA allows you to enforce consistent naming conventions, tagging standards, and other best practices across your infrastructure. This consistency leads to improved manageability and makes it easier for teams to collaborate effectively.

### Auditing and Compliance Reporting:

With Sentinel's logging and reporting capabilities, you can track policy decisions and changes made to your infrastructure over time. This audit trail is valuable for compliance purposes and can be used to demonstrate adherence to regulatory requirements.





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

