Step 1: Log in to the Linux server using the credential

Step 2: Download Terraform Software and install  

https://developer.hashicorp.com/terraform/downloads

In this case I have used Amazon Linux 
Execute below command
```
sudo yum install -y yum-utils shadow-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
```
Step 3: validate software 
```
terraform --version
```
Sample output:
[ec2-user@ip-10-0-14-30 terraform]$ terraform --version
Terraform v1.4.6
on linux_amd64
+ provider registry.terraform.io/hashicorp/aws v4.66.0

