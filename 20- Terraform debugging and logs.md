

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
