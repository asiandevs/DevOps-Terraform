## Terraform Commands Usage
In this section I will go through Terraform commands.

## prerequisite:
I have provisioned a AWS EC2 linux instance

```diff
- NOTE
! Make sure any Software Licence requirements from your side. Please do modify path or vriables based on your own setup. 
```

## Advise - when you learning
```diff
- NOTE
! Please remove the resources/s to avoid unnecessary cost -- make sure you are in right workspace before executing destroy command 
```
```
terraform destroy --auto-approve
```
## Files

File                 | tasks
---------------------- | ----------------------------------------------------------------------
01_terraform-install   |  **Install Terraform software in Linux platform**
02_configure-awscli    |  **Configure aws CLI**
03_setawsusercredential|  **Setup AWS IAM user credential**
04_configure-resources |  **Setting up resources - I have done for EC2 related components [VPC, SG, ...]**
05_basic-commands      | **Basic commands**
06_state-function      |  **Terraform resource status**
07_format_output_debug | **Formatting and debugging**
08_taint_import        | **taint and import**  
09_workspace           | **workspace**
10_s3                  |**AWS S3**
```
