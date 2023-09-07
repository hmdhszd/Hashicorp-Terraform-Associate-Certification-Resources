




Terraform Cloud, developed by HashiCorp, offers a centralized platform for managing Terraform code.

__________________________________________________________________________________________



## Key features:

- `version control integration`

- `secure variable storage`

- `remote state management`

- `policy enforcement`

- `enabling organizations`


__________________________________________________________________________________________




What feature of Terraform Cloud allows you to publish and maintain a set of `custom` `modules` which can be used within your organization? `Private` `Module` `Registry`


__________________________________________________________________________________________



### Terraform Cloud supported VCS providers: `GitHub` , `GitLab` , `Bitbucket` , `Azure`



  - `GitHub`

  - GitHub.com (OAuth)

  - GitHub Enterprise

  - GitLab.com

  - `GitLab` EE and CE

  - `Bitbucket` Cloud

  - Bitbucket Server

  - `Azure` DevOps Server

  - Azure DevOps Services



__________________________________________________________________________________________




## Terraform Cloud workspace linked to a GitHub repo


After approving a `merge` `request` that modifies Terraform configurations in a GitHub repository linked to a Terraform Cloud workspace, the default action that can be expected to run `automatically` is a `speculative plan` operation.


then validate the changes against `Sentinel Policy`


__________________________________________________________________________________________




When using variables in Terraform Cloud, what level of scope can the variable be applied to?

- a specific terraform run in a `single` `workspace`

- `multiple` `workspaces` using a `variable` `set`

- all `current` and `future` `workspaces` in a project using a `variable` `set`


__________________________________________________________________________________________




Select the workflows that Terraform cloud utilizes to manage Terraform runs: 

- `UI/VCS`-driven run workflow,

- `API`-driven run workflow,

- `CLI`-driven run workflow


__________________________________________________________________________________________





In the `UI/VCS` workflow, `every workspace` is associated with a `specific branch` of a VCS repo of Terraform configurations.




__________________________________________________________________________________________




In Terraform `OSS`, `workspaces` generally use the `same` `code` repository

while workspaces in Terraform `Enterprise/Cloud` are often mapped to `different` `code` `repositories`.



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


## Terraform Enterprise & Terraform Cloud

Terraform Enterprise is our self-hosted distribution of Terraform Cloud.

Terraform Enterprise is used for the AirGapped systems

It offers enterprises a private instance of the Terraform Cloud application, with no resource limits and with additional enterprise-grade architectural features like audit logging and SAML single sign-on.

Terraform Enterprise provides several added advantage compared to Terraform Cloud.

Some of these include:

● `Single Sign-On (SSO)`

● `Auditing`

● `Private Data Center Networking`

● `Clustering`

Team & Governance features are not available for Terraform Cloud Free (it's a Paid features)


__________________________________________________________________________________________


migrating from terraform OSS to terraform cloud --> on the cloud we use the `same Terraform Version` that was used on the OSS

__________________________________________________________________________________________

### `API` `TOKEN`

Terraform Cloud can be managed from the CLI but requires an _____`API TOKEN`_____?


__________________________________________________________________________________________


__________________________________________________________________________________________


### Terraform Cloud for Business

`Terraform` `Cloud` `Agents` are a feature that allows Terraform Cloud to communicate with `private` `infrastructure`, such as `VMware` hosts running on-premises.

Which version of Terraform Cloud supports this feature?  `Terraform` `Cloud` `for` `Business`

__________________________________________________________________________________________


### enhanced storage backend

Using an enhanced storage backend allows you to execute your Terraform on infrastructure either locally or in Terraform Cloud.

__________________________________________________________________________________________


### Sentinel

You can use a `combination` of Terraform Cloud's `cost estimation` feature and `Sentinel policies` to ensure your organization doesn't apply changes to your environment that would result in `exceeding` your monthly operating `budget`.

__________________________________________________________________________________________


### Sentinel --> Proactive


What is the use of Sentinel policy as a code in Terraform Enterprise provides what security posture?

Sentinel `proactively` prevents provisioning of out-of-policy infrastructure


Sentinel policy as code is  proactive governance , prevent you to create/update resource unless your terraform code adhered to  the sentinel policy.



__________________________________________________________________________________________

Where is the most secure place to store `credentials` when using a `remote backend`? `define outside of terraform`

do NOT use environment variable

__________________________________________________________________________________________


