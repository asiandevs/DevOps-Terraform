Step 1. There is a *.tfstate file under the directory to hold the resource information

Get the list all the resources being tracked by the Terraform state file
  a) see the options available for this command
  ```
   terraform state or terraform state -help
   ```
  b)terraform state list
```   
Sample output:
[ec2-user@ip-10-0-14-30 terraform]$ terraform state list
data.aws_availability_zones.azs
data.aws_route_table.main_route_table
data.aws_ssm_parameter.webserver-ami
aws_default_route_table.internet_route
aws_instance.webserver
aws_internet_gateway.igw
aws_key_pair.webserver-key
aws_security_group.sg
aws_subnet.subnet
aws_vpc.vpc
```
Step 2: Show details of a specific resource tracked 
```
  terraform state show <resource name>
  
  Sample output:
  terraform state show aws_vpc.vpc
    # aws_vpc.vpc:
resource "aws_vpc" "vpc" {
    arn                                  = "arn:aws:ec2:us-east-1:027777522454:vpc/vpc-002673b3cb1999d4c"
    assign_generated_ipv6_cidr_block     = false
    cidr_block                           = "10.0.0.0/16"
    default_network_acl_id               = "acl-08ccd9e2e3fce40e6"
    default_route_table_id               = "rtb-006ced4b66c37f4c1"
    default_security_group_id            = "sg-02cd322def5d6543b"
    dhcp_options_id                      = "dopt-0ddc679897749cb5f"
    enable_classiclink                   = false
    enable_classiclink_dns_support       = false
    enable_dns_hostnames                 = true
    enable_dns_support                   = true
    enable_network_address_usage_metrics = false
    id                                   = "vpc-002673b3cb1999d4c"
    instance_tenancy                     = "default"
    ipv6_netmask_length                  = 0
    main_route_table_id                  = "rtb-006ced4b66c37f4c1"
    owner_id                             = "027777522454"
    tags                                 = {
        "Name" = "terraform-vpc"
    }
    tags_all                             = {
        "Name" = "terraform-vpc"
    }
}
```
Step 3: To delete a resource from the state file
terraform state rm <resource>
```
sample output:
[ec2-user@ip-10-0-14-30 terraform]$ terraform state rm aws_vpc.vpc
Removed aws_vpc.vpc
Successfully removed 1 resource instance(s).

[ec2-user@ip-10-0-14-30 terraform]$ ls -ltr
total 80
-rw-r--r--. 1 ec2-user ec2-user   143 May  5 12:41 variables.tf
-rw-r--r--. 1 ec2-user ec2-user 18104 May  5 12:45 terraform.tfstate.1683290702.backup
-rw-r--r--. 1 ec2-user ec2-user  2301 May  5 12:49 setup.tf
-rw-r--r--. 1 ec2-user ec2-user   212 May  5 12:50 outputs.tf
drwxr-xr-x. 3 ec2-user ec2-user    78 May  5 21:12 aws
-rw-r--r--. 1 ec2-user ec2-user   867 May  6 07:05 main.tf
-rw-r--r--. 1 ec2-user ec2-user   181 May  6 09:22 terraform.tfstate.backup
-rw-r--r--. 1 ec2-user ec2-user 18101 May  6 09:34 terraform.tfstate.1683365673.backup
-rw-r--r--. 1 ec2-user ec2-user 16447 May  6 09:34 terraform.tfstate
[ec2-user@ip-10-0-14-30 terraform]$ date
Sat May  6 09:34:49 UTC 2023
```
