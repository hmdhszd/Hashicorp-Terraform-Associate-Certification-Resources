

### TF_LOG

to see more logs when you run "terraform apply" command,

You can set the Terraform log level and location via the TF_LOG and TF_LOG_PATH environment variables.



__________________________________________________________________________________________






```bash
Bash: export TF_LOG="DEBUG"
```



```bash
PowerShell: $env:TF_LOG="DEBUG"
```



__________________________________________________________________________________________



You can set TF_LOG to one of the log levels (in order of decreasing verbosity) 

TRACE, DEBUG, INFO, WARN or ERROR to change the verbosity of the logs.


__________________________________________________________________________________________



### TF_LOG_PATH

The environment variable TF_LOG_PATH specifies the file in which Terraform will write logs.


If TF_LOG_PATH is not set, output is sent to standard output and error in the terminal.




__________________________________________________________________________________________






```bash
PowerShell: $env:TF_LOG_PATH="C:\tmp\terraform.log"
```




```bash
Bash: export TF_LOG_PATH="tmp/terraform.log"
```



__________________________________________________________________________________________


### Disable

To disable debug mode and reset the logging verbosity to its default level, clear the TF_LOG environment variable by running: unset TF_LOG.



__________________________________________________________________________________________


You can set TF_LOG to one of the log levels (in order of decreasing verbosity) TRACE, DEBUG, INFO, WARN or ERROR to change the verbosity of the logs. Also if we set TF_LOG to JSON, it output logs at the TRACE level or higher, and uses a parseable JSON encoding as the formatting.

__________________________________________________________________________________________


How would you achieve the force replacement of a particular object even though there are no configuration changes? Choose the most appropriate option among the following:

Usage of terraform apply -replace=”<resource_name>” is preferred overterraform taint`


__________________________________________________________________________________________



Your team is working collaboratively on a project that uses terraform scripts heavily. In your team one team member was not familiar with terraform, so he was making the required changes manually, using the GUI console of that specific cloud provider on the resources provisioned using terraform. Since these unmanaged changes are hampering the efficiency of the team , you want to revert these changes. How would you go about doing this?


Use terraform destroy and then terraform apply commands in this specific order,You will taint the resources that you want removed on the next terraform apply.


__________________________________________________________________________________________


