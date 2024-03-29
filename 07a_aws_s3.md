This is specific to create a S3 and enable some features there (versioning, lifecycle rule)

Step 1: To make this separate - For this task I have created a separate directory
```
mkdir s3
```
Step 2: Add entry for the required variables
```
vars.tf
```
```
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "bucket_name" {
  description = "S3 bucket name"
  type        = string
  default     = "amity01"
}
```
Step 3: I have added resource to create bucket with few features
```
main.tf
```
```
provider "aws" {
  region = "us-east-1"
}

########################
# Bucket creation
########################
resource "aws_s3_bucket" "amity01" {
  bucket = var.bucket_name
}

##########################
# Bucket private access
##########################
#resource "aws_s3_bucket_acl" "amity01-acl" {
#  bucket = aws_s3_bucket.amity01.id
#  acl    = "private"
#}

#resource "aws_s3_bucket_ownership_controls" "amity01-acl-ownership" {
#  bucket = aws_s3_bucket.amity01.id
#  rule {
#    object_ownership = "BucketOwnerEnforced"
#  }
  # Add just this depends_on condition
#  depends_on = [aws_s3_bucket_acl.amity01-acl]
#}

#############################
# Enable bucket versioning
#############################
resource "aws_s3_bucket_versioning" "amity01_versioning" {
  bucket = aws_s3_bucket.amity01.id
  versioning_configuration {
    status = "Enabled"
  }
}

############################
# Creating Lifecycle Rule
############################
resource "aws_s3_bucket_lifecycle_configuration" "amity01_lifecycle_rule" {
  # Must have bucket versioning enabled first
  depends_on = [aws_s3_bucket_versioning.amity01_versioning]

  bucket = aws_s3_bucket.amity01.bucket

  rule {
    id = "basic_config"
    status = "Enabled"

    filter {
      prefix = "config/"
    }

    noncurrent_version_transition {
      noncurrent_days = 30
      storage_class   = "STANDARD_IA"
    }

    noncurrent_version_transition {
      noncurrent_days = 60
      storage_class   = "GLACIER"
    }

    noncurrent_version_expiration {
      noncurrent_days = 90
    }
  }
}
# Enable Encryption on Bucket
resource "aws_s3_bucket_server_side_encryption_configuration" "amity01-encryption" {
  bucket = aws_s3_bucket.amity01.bucket

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}

# Server side Encryption
resource "aws_kms_key" "demokey" {
  description             = "key to encrypt bucket objects"
  deletion_window_in_days = 7
}

resource "aws_s3_bucket_server_side_encryption_configuration" "demo_encryption" {
  bucket = aws_s3_bucket.amity01.bucket

  rule {
    apply_server_side_encryption_by_default {
      kms_master_key_id = aws_kms_key.demokey.arn
      sse_algorithm     = "aws:kms"
    }
  }
}
#Prevent objects from becoming public
resource "aws_s3_bucket_public_access_block" "amity_public_block" {
  bucket = aws_s3_bucket.amity01.bucket

  block_public_acls   = true
  block_public_policy = true
  ignore_public_acls = true
  restrict_public_buckets = true
}
```
Step 4: terraform init

Step 5: terraform plan

Step 6: terraform apply --auto-approve 

Step 7 :  terraform state list
