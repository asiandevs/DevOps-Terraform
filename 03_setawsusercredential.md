Step 1: From the Linux session execute 
```
aws configure
```

Step 2: validate the entries are added
```
cat ~/.aws/credentials 
```
NOTE: Get the details [aws_access_key_id and aws_secret_access_key] of the respective user from the AWS console

Sample output: 
```
[ec2-user@ip-10-0-14-30 terraform]$ aws configure
AWS Access Key ID [None]: AKIAQ**********A2HV
AWS Secret Access Key [None]: xwv^^^^^^^^^^^^^^^^Sj4X3
Default region name [None]: us-east-1
Default output format [None]: json
[ec2-user@ip-10-0-14-30 terraform]$ cat ~/.aws/credentials 
[default]
aws_access_key_id = AKIAQ**********A2HV
aws_secret_access_key =xwv^^^^^^^^^^^^^^^^Sj4X3

Note: you can also pass aws credential as Terraform variables - like as below 

[ec2-user@ip-10-0-14-30 terraform]$ cat variables.tf
provider "aws" {
  access_key = "AKIAQ**********A2HV"
  secret_key = "xwv^^^^^^^^^^^^^^^^Sj4X3"
  region     = "us-east-1"
}
```
