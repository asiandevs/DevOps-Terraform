Step 1: FORMAT 
To format any unformatted code before deployment
```
[ec2-user@ip-10-0-14-30 terraform]$ cat outputs.tf
output "PrivateIP" {
  description = "Private IP of EC2 instance"
  value       = aws_instance.webserver.private_ip
}

output "Time-Date" {
  description = "Date/Time of Execution"
         value       = timestamp()                   <====== [ it is going tobe formatted] 
}
```
Sample output:
```
[ec2-user@ip-10-0-14-30 terraform]$ terraform fmt
outputs.tf
[ec2-user@ip-10-0-14-30 terraform]$ cat outputs.tf
output "PrivateIP" {
  description = "Private IP of EC2 instance"
  value       = aws_instance.webserver.private_ip
}

output "Time-Date" {
  description = "Date/Time of Execution"
  value       = timestamp()
}
```
Step 2: OUTPUT
add a outputs.tf file in the same directory to returns the specific values after deployment  
```
[ec2-user@ip-10-0-14-30 terraform]$ cat outputs.tf
output "PrivateIP" {
  description = "Private IP of EC2 instance"
  value       = aws_instance.webserver.private_ip
}

output "Time-Date" {
  description = "Date/Time of Execution"
  value       = timestamp()
}
```
sample output at the bottom is as below when you execute terraform apply

Apply complete! Resources: 7 added, 0 changed, 0 destroyed.

Outputs:
```
PrivateIP = "10.0.1.91"
Time-Date = "2023-05-06T09:22:16Z"
Webserver-Public-IP = "44.212.17.113"
```
Step 3: TRACE
To enable trace you can set TF_LOG environment variable
```
export TF_LOG=TRACE
```
For a persist logged output use the TF_LOG_PATH environment variable
```
export TF_LOG_PATH=./trfm.log
```
Then get the information from that file 
Sample output:
```
[ec2-user@ip-10-0-14-30 terraform]$ tail -3 trfm.log
2023-05-06T09:47:36.977Z [TRACE] LoadSchemas: retrieving schema for provisioner "remote-exec"
2023-05-06T09:47:37.052Z [TRACE] statemgr.Filesystem: removing lock metadata file .terraform.tfstate.lock.info
2023-05-06T09:47:37.052Z [TRACE] statemgr.Filesystem: unlocking terraform.tfstate using fcntl flock
```
Step 4: To disable trace file
```
[ec2-user@ip-10-0-14-30 s3]$ export TF_LOG=
[ec2-user@ip-10-0-14-30 s3]$ export TF_LOG_PATH=
```
