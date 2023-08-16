

### TF_LOG

to see more logs when you run "terraform apply" command,

You can set the Terraform log level and location via the `TF_LOG` and `TF_LOG_PATH` environment variables.



__________________________________________________________________________________________






```bash
Bash: export TF_LOG="DEBUG"
```



```bash
PowerShell: $env:TF_LOG="DEBUG"
```



__________________________________________________________________________________________



You can set TF_LOG to one of the log levels (in order of decreasing verbosity) 



`TRACE`: The most verbose level, providing extremely detailed information, often at a lower level in the code.

`DEBUG`: Detailed information that can help you trace the flow of your program and diagnose issues.

`INFO`: General information about the progress of your program, like what operations are being executed or the status of certain components.

`WARN`: Used for warnings that might not be errors, but could lead to potential issues or unexpected behavior.

`ERROR`: Used for errors that do not necessarily lead to program termination but indicate a problem that needs attention.

__________________________________________________________________________________________


#### TF_LOG="JSON"

Also if we set TF_LOG to JSON, it output logs at the `TRACE` level or HIGHER, and uses a parseable JSON encoding as the formatting.


```bash
Bash: export TF_LOG="JSON"
```

__________________________________________________________________________________________



### TF_LOG_PATH

The environment variable `TF_LOG_PATH` specifies the file in which Terraform will write logs.


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

To disable debug mode and debug path and reset the logging verbosity and path to its default, clear the TF_LOG and TF_LOG_PATH environment variable by running:


```bash
unset TF_LOG
unset TF_LOG_PATH
```

__________________________________________________________________________________________



Your team is working collaboratively on a project that uses terraform scripts heavily. In your team one team member was not familiar with terraform, so he was making the required changes manually, using the GUI console of that specific cloud provider on the resources provisioned using terraform. Since these unmanaged changes are hampering the efficiency of the team , you want to revert these changes. How would you go about doing this?


-  Use `terraform destroy` and then `terraform apply` commands in this specific order,

-  You will `taint` the resources that you want removed on the next terraform apply.


__________________________________________________________________________________________




Logging can be enabled separately for terraform itself and the provider plugins using the `TF_LOG_CORE` or `TF_LOG_PROVIDER` environment variables.

These take the same level arguments as `TF_LOG`, but only activate a subset of the logs.




__________________________________________________________________________________________

