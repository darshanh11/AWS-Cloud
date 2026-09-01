# Lab 20 - Terraform

## Objective

The objective of this lab is to understand **Terraform** and practically learn how to create, configure, deploy, modify, and destroy AWS infrastructure using Infrastructure as Code (IaC).

This lab covers:

- Terraform
- Infrastructure as Code (IaC)
- Terraform Installation
- Terraform CLI
- Terraform Providers
- Terraform Configuration Files
- Terraform Resources
- Terraform Variables
- Terraform Outputs
- Terraform Data Sources
- Terraform State
- Terraform Plan
- Terraform Apply
- Terraform Destroy
- Terraform Init
- Terraform Validate
- Terraform Format
- Terraform Modules
- Terraform Dependencies
- Terraform State Management
- Terraform with AWS
- EC2
- S3
- VPC
- Security Groups
- IAM
- Terraform and CloudWatch
- Terraform and CloudTrail
- Terraform Security
- Practical Terraform Configuration
- Troubleshooting
- Best Practices

---

## 1. What is Terraform?

### Explanation

**Terraform** is an Infrastructure as Code (IaC) tool used to define and provision infrastructure using configuration files.

Terraform can manage infrastructure across AWS and many other platforms.

Instead of manually creating resources through the AWS Management Console, Terraform allows infrastructure to be described using configuration files.

### Example

```text
Terraform Configuration
        |
        v
Terraform
        |
        v
AWS Provider
        |
        v
AWS Resources
```

### Result

**Successfully understood that Terraform is an Infrastructure as Code tool used to define and manage infrastructure through configuration files.**

---

## 2. What is Infrastructure as Code?

### Explanation

**Infrastructure as Code (IaC)** means defining infrastructure in files instead of manually creating every resource.

### Traditional Method

```text
AWS Console
    |
    +---- Create VPC
    |
    +---- Create Subnet
    |
    +---- Create Security Group
    |
    +---- Create EC2
```

### Terraform Method

```text
Terraform Code
      |
      v
Terraform
      |
      v
AWS Provider
      |
      v
AWS Infrastructure
```

### Benefits

```text
Automation
Consistency
Repeatability
Version Control
Reusability
Faster Deployment
```

### Result

**Successfully understood how Terraform supports Infrastructure as Code and automated infrastructure management.**

---

## 3. Terraform Configuration Language

### Explanation

Terraform uses **HashiCorp Configuration Language (HCL)** for configuration files.

Terraform files normally use the `.tf` extension.

Example:

```text
main.tf
variables.tf
outputs.tf
```

### Example

```hcl
resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-unique"
}
```

### Result

**Successfully understood that Terraform commonly uses HCL configuration files with the `.tf` extension.**

---

## 4. Terraform File Structure

### Explanation

A Terraform project can be organized into multiple `.tf` files.

Example:

```text
terraform-lab/
 |
 +---- main.tf
 |
 +---- variables.tf
 |
 +---- outputs.tf
 |
 +---- providers.tf
 |
 +---- terraform.tfvars
 |
 +---- .gitignore
```

Terraform loads configuration from all `.tf` files in the working directory.

### Result

**Successfully understood the basic structure of a Terraform project.**

---

## 5. Terraform Provider

### Explanation

A **provider** is a Terraform plugin that allows Terraform to interact with an external platform or service.

For AWS infrastructure, Terraform uses the **AWS provider**.

### Example

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}
```

### Architecture

```text
Terraform
    |
    v
AWS Provider
    |
    v
AWS API
    |
    v
AWS Resources
```

### Result

**Successfully understood the role of the AWS provider in allowing Terraform to communicate with AWS.**

---

## 6. Terraform Resource

### Explanation

A **resource** represents an infrastructure object that Terraform manages.

Examples include:

```text
aws_instance
aws_s3_bucket
aws_vpc
aws_subnet
aws_security_group
aws_iam_role
```

### Example

```hcl
resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-unique"
}
```

### Structure

```text
resource
   |
   +---- Resource Type
   |
   +---- Resource Name
   |
   +---- Arguments
```

### Result

**Successfully understood how Terraform resources represent AWS infrastructure objects.**

---

## 7. Terraform Resource Naming

### Explanation

A Terraform resource has two important identifiers:

```text
Resource Type
Resource Name
```

Example:

```hcl
resource "aws_s3_bucket" "lab_bucket" {
}
```

Here:

```text
aws_s3_bucket
       |
       +---- Resource Type

lab_bucket
       |
       +---- Resource Name
```

### Result

**Successfully understood the structure of Terraform resource declarations.**

---

## 8. Installing Terraform

### Explanation

Terraform must be installed before Terraform CLI commands can be executed.

### Practical Steps

1. Install Terraform on the operating system.
2. Add Terraform to the system PATH if required.
3. Open Command Prompt, PowerShell, or Terminal.
4. Run:

```bash
terraform version
```

### Example Result

```text
Terraform v1.x.x
```

The exact version depends on the installed Terraform release.

### Result

**Successfully installed Terraform and verified the installation using the Terraform CLI.**

---

## 9. Terraform CLI

### Explanation

Terraform provides a command-line interface for managing infrastructure.

Common commands include:

```text
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform show
terraform output
```

### Example

```text
Terminal
   |
   v
Terraform CLI
   |
   v
Terraform Configuration
   |
   v
AWS Infrastructure
```

### Result

**Successfully understood the main Terraform CLI commands.**

---

## 10. Terraform Init

### Explanation

`terraform init` initializes a Terraform working directory.

It downloads the required providers and prepares the directory for Terraform operations.

### Command

```bash
terraform init
```

### Example

```text
Terraform Configuration
        |
        v
terraform init
        |
        v
Download Provider
        |
        v
Initialized
```

### Result

**Successfully understood the purpose of `terraform init`.**

---

## 11. Terraform Format

### Explanation

`terraform fmt` formats Terraform configuration files into Terraform's standard formatting style.

### Command

```bash
terraform fmt
```

### Result

```text
Terraform Files
      |
      v
terraform fmt
      |
      v
Formatted Configuration
```

### Result

**Successfully understood how `terraform fmt` formats Terraform configuration files.**

---

## 12. Terraform Validate

### Explanation

`terraform validate` checks whether the Terraform configuration is syntactically valid and internally consistent.

### Command

```bash
terraform validate
```

### Example Result

```text
Success! The configuration is valid.
```

### Result

**Successfully understood how to validate Terraform configuration before deployment.**

---

## 13. Terraform Plan

### Explanation

`terraform plan` shows the changes Terraform intends to make to infrastructure.

It helps review changes before applying them.

### Command

```bash
terraform plan
```

### Example

```text
Terraform Plan
      |
      +---- Create
      |
      +---- Change
      |
      +---- Destroy
```

Terraform commonly displays symbols such as:

```text
+ create
~ update
- destroy
```

### Result

**Successfully understood how `terraform plan` previews infrastructure changes before deployment.**

---

## 14. Terraform Apply

### Explanation

`terraform apply` applies the Terraform configuration and creates or modifies the infrastructure.

### Command

```bash
terraform apply
```

Terraform normally displays the proposed plan and asks for confirmation before making changes.

### Example

```text
Terraform Code
      |
      v
terraform apply
      |
      v
AWS API
      |
      v
AWS Resources
```

### Result

**Successfully understood how `terraform apply` provisions or modifies infrastructure.**

---

## 15. Terraform Destroy

### Explanation

`terraform destroy` removes resources managed by the Terraform configuration.

### Command

```bash
terraform destroy
```

Terraform normally shows the planned deletions and asks for confirmation.

### Example

```text
Terraform State
      |
      v
terraform destroy
      |
      v
AWS Resources
      |
      v
Deleted
```

### Result

**Successfully understood how `terraform destroy` removes Terraform-managed resources.**

---

## 16. Terraform Variables

### Explanation

Terraform variables allow configuration values to be supplied without hard-coding them directly into resource definitions.

### Example

```hcl
variable "aws_region" {
  description = "AWS Region"
  type        = string
  default     = "ap-south-1"
}
```

Use the variable:

```hcl
provider "aws" {
  region = var.aws_region
}
```

### Result

**Successfully understood how Terraform variables make configurations more reusable and configurable.**

---

## 17. Terraform Variable Types

### Explanation

Terraform supports different variable types.

Examples:

```text
string
number
bool
list
set
map
object
tuple
```

### Example

```hcl
variable "instance_type" {
  type    = string
  default = "t3.micro"
}
```

### Result

**Successfully understood the purpose of Terraform variable types.**

---

## 18. Terraform tfvars File

### Explanation

A `.tfvars` file can be used to provide values for Terraform variables.

### Example

```text
terraform.tfvars
```

Content:

```hcl
aws_region    = "ap-south-1"
instance_type = "t3.micro"
environment   = "dev"
```

### Result

**Successfully understood how `.tfvars` files can provide Terraform variable values.**

---

## 19. Terraform Outputs

### Explanation

Terraform outputs display useful information after infrastructure is created.

Examples:

```text
EC2 Instance ID
S3 Bucket Name
VPC ID
Subnet ID
Public IP
```

### Example

```hcl
output "bucket_name" {
  description = "Name of the S3 bucket"
  value       = aws_s3_bucket.lab_bucket.id
}
```

### Command

```bash
terraform output
```

### Result

**Successfully understood how Terraform outputs provide useful information about managed infrastructure.**

---

## 20. Terraform State

### Explanation

Terraform uses a **state file** to keep track of the infrastructure it manages.

The default local state file is:

```text
terraform.tfstate
```

The state allows Terraform to compare the desired configuration with the infrastructure it manages.

### Architecture

```text
Terraform Configuration
        |
        v
Desired State
        |
        v
Terraform State
        |
        v
Actual Infrastructure
```

### Result

**Successfully understood the purpose of Terraform state in infrastructure management.**

---

## 21. terraform.tfstate

### Explanation

The `terraform.tfstate` file contains Terraform's state information.

It can contain sensitive infrastructure information depending on the resources and configuration.

### Security Rule

```text
terraform.tfstate
       |
       X
Do NOT commit to public GitHub repositories
```

### Result

**Successfully understood why Terraform state files must be protected.**

---

## 22. Terraform State and GitHub

### Explanation

Terraform projects should use `.gitignore` to prevent sensitive or generated Terraform files from being committed accidentally.

### Example `.gitignore`

```gitignore
.terraform/
*.tfstate
*.tfstate.*
crash.log
*.tfvars
*.tfvars.json
override.tf
override.tf.json
*_override.tf
*_override.tf.json
.terraform.lock.hcl
```

For real projects, the exact `.gitignore` should be chosen carefully because some files, such as the dependency lock file, are often intentionally committed.

### Result

**Successfully understood how `.gitignore` can help prevent sensitive Terraform files and local state from being committed to GitHub.**

---

## 23. Terraform Dependency

### Explanation

Terraform automatically understands dependencies when one resource references another.

### Example

```hcl
resource "aws_vpc" "lab_vpc" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "lab_subnet" {
  vpc_id     = aws_vpc.lab_vpc.id
  cidr_block = "10.0.1.0/24"
}
```

The subnet references the VPC.

Therefore:

```text
VPC
 |
 v
Subnet
```

### Result

**Successfully understood how Terraform determines resource dependencies from references.**

---

## 24. Terraform Data Sources

### Explanation

A **data source** allows Terraform to retrieve information about existing infrastructure or external data rather than creating the resource.

### Example

```hcl
data "aws_caller_identity" "current" {}

output "account_id" {
  value = data.aws_caller_identity.current.account_id
}
```

### Result

**Successfully understood that Terraform data sources retrieve information about existing resources or external data.**

---

## 25. Terraform Modules

### Explanation

A **module** is a reusable collection of Terraform configuration files.

Modules help organize and reuse infrastructure code.

### Example

```text
terraform-project/
 |
 +---- main.tf
 |
 +---- modules/
       |
       +---- network/
       |      |
       |      +---- main.tf
       |
       +---- ec2/
              |
              +---- main.tf
```

### Result

**Successfully understood how Terraform modules help organize and reuse infrastructure configurations.**

---

## 26. Terraform with AWS

### Explanation

Terraform can manage AWS infrastructure through the AWS provider.

### Architecture

```text
Terraform
    |
    v
AWS Provider
    |
    v
AWS API
    |
    +---- EC2
    +---- S3
    +---- VPC
    +---- IAM
    +---- RDS
    +---- Lambda
    +---- CloudWatch
```

### Result

**Successfully understood how Terraform manages AWS infrastructure through the AWS provider.**

---

## 27. Terraform AWS Provider Configuration

### Example

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}
```

### Result

**Successfully configured the Terraform AWS provider for the Mumbai Region.**

---

## 28. Terraform Practical Lab - S3 Bucket

### Explanation

In this practical lab, an S3 bucket is created using Terraform.

### File

```text
main.tf
```

### Code

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-unique-bucket-name"

  tags = {
    Name        = "Lab20-Terraform-Bucket"
    Environment = "Lab"
    ManagedBy   = "Terraform"
  }
}

output "bucket_name" {
  description = "Terraform managed S3 bucket name"
  value       = aws_s3_bucket.lab_bucket.id
}
```

### Practical Steps

### Step 1 - Create Directory

```bash
mkdir terraform-lab
cd terraform-lab
```

### Step 2 - Create Terraform File

```text
main.tf
```

### Step 3 - Add Code

Paste the Terraform configuration into:

```text
main.tf
```

### Step 4 - Initialize Terraform

```bash
terraform init
```

### Step 5 - Format Configuration

```bash
terraform fmt
```

### Step 6 - Validate

```bash
terraform validate
```

### Step 7 - Preview Changes

```bash
terraform plan
```

### Step 8 - Apply Configuration

```bash
terraform apply
```

Enter:

```text
yes
```

when Terraform asks for confirmation.

### Step 9 - Verify Output

```bash
terraform output
```

### Step 10 - Verify AWS

Open:

```text
AWS Console
   |
   v
S3
   |
   v
Buckets
```

Verify the Terraform-created bucket.

### Result

**Successfully created and verified an S3 bucket using Terraform.**

---

## 29. Terraform with EC2

### Explanation

Terraform can create EC2 instances and supporting infrastructure.

### Architecture

```text
Terraform
   |
   v
VPC
 |
 +---- Subnet
 |
 +---- Security Group
 |
 +---- EC2 Instance
```

### Result

**Successfully understood how Terraform can provision EC2 infrastructure.**

---

## 30. Terraform EC2 Example

### Example

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "lab_instance" {
  ami           = "ami-xxxxxxxxxxxxxxxxx"
  instance_type = "t3.micro"

  tags = {
    Name      = "Lab20-Terraform-EC2"
    ManagedBy = "Terraform"
  }
}

output "instance_id" {
  description = "EC2 Instance ID"
  value       = aws_instance.lab_instance.id
}
```

The AMI ID must be replaced with a valid AMI available in the selected Region.

### Result

**Successfully understood how Terraform can define and provision an EC2 instance.**

---

## 31. Terraform with VPC

### Explanation

Terraform can create networking infrastructure such as:

```text
VPC
Subnet
Route Table
Internet Gateway
Security Group
```

### Architecture

```text
Terraform
    |
    v
VPC
 |
 +---- Subnet
 |
 +---- Route Table
 |
 +---- Internet Gateway
 |
 +---- Security Group
```

### Result

**Successfully understood how Terraform can provision AWS networking infrastructure.**

---

## 32. Terraform VPC Example

### Code

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_vpc" "lab_vpc" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name      = "Lab20-Terraform-VPC"
    ManagedBy = "Terraform"
  }
}

resource "aws_subnet" "lab_subnet" {
  vpc_id     = aws_vpc.lab_vpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "Lab20-Terraform-Subnet"
  }
}

output "vpc_id" {
  value = aws_vpc.lab_vpc.id
}

output "subnet_id" {
  value = aws_subnet.lab_subnet.id
}
```

### Result

**Successfully understood how Terraform can create a VPC and subnet and expose their IDs through outputs.**

---

## 33. Terraform with Security Groups

### Explanation

Terraform can create Security Groups and configure network rules.

### Example

```hcl
resource "aws_security_group" "lab_sg" {
  name        = "lab20-terraform-sg"
  description = "Security group for Terraform lab"
  vpc_id      = aws_vpc.lab_vpc.id

  tags = {
    Name      = "Lab20-Terraform-SG"
    ManagedBy = "Terraform"
  }
}
```

Security rules should be added only when required by the workload.

### Result

**Successfully understood how Terraform can manage AWS Security Groups.**

---

## 34. Terraform with IAM

### Explanation

Terraform can manage IAM resources such as:

```text
IAM Roles
IAM Policies
IAM Users
IAM Groups
```

IAM resources should be managed carefully because incorrect permissions can create security risks.

### Example

```hcl
resource "aws_iam_role" "lab_role" {
  name = "Lab20-Terraform-Role"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
        Action = "sts:AssumeRole"
      }
    ]
  })
}
```

### Result

**Successfully understood how Terraform can define IAM resources and why IAM configurations require careful security controls.**

---

## 35. Terraform with RDS

### Explanation

Terraform can manage RDS resources.

Example:

```text
Terraform
    |
    v
RDS
    |
    +---- DB Instance
    +---- Parameter Group
    +---- Subnet Group
    +---- Security Group
```

### Result

**Successfully understood that Terraform can manage RDS infrastructure using the AWS provider.**

---

## 36. Terraform with Lambda

### Explanation

Terraform can create and manage Lambda functions and related IAM resources.

### Example Architecture

```text
Terraform
    |
    v
Lambda
    |
    +---- Function
    +---- IAM Role
    +---- CloudWatch Logs
    +---- Trigger
```

### Result

**Successfully understood how Terraform can manage Lambda functions and their supporting infrastructure.**

---

## 37. Terraform with CloudWatch

### Explanation

Terraform can define CloudWatch resources such as:

```text
CloudWatch Alarms
Dashboards
Log Groups
```

### Example

```hcl
resource "aws_cloudwatch_log_group" "lab_logs" {
  name              = "/aws/lab/terraform"
  retention_in_days = 7

  tags = {
    ManagedBy = "Terraform"
  }
}
```

### Result

**Successfully understood how Terraform can manage CloudWatch monitoring resources.**

---

## 38. Terraform with CloudTrail

### Explanation

Terraform can define CloudTrail resources and supporting infrastructure.

### Example Architecture

```text
Terraform
    |
    v
CloudTrail
    |
    v
Trail
    |
    v
S3
```

### Result

**Successfully understood how Terraform can be used to define CloudTrail infrastructure.**

---

## 39. Terraform Plan and Apply Workflow

### Explanation

Terraform follows a workflow where configuration is initialized, validated, planned, and applied.

### Workflow

```text
Terraform Code
      |
      v
terraform init
      |
      v
terraform fmt
      |
      v
terraform validate
      |
      v
terraform plan
      |
      v
Review Changes
      |
      v
terraform apply
      |
      v
AWS Infrastructure
```

### Result

**Successfully understood the standard Terraform deployment workflow.**

---

## 40. Terraform State Management

### Explanation

Terraform state is important because Terraform uses it to track managed resources.

For team environments, local state files can create collaboration and security problems.

A remote backend can be used for centralized state management.

### Example

```text
Terraform
    |
    v
Remote Backend
    |
    v
Terraform State
    |
    v
Team
```

### Result

**Successfully understood the importance of Terraform state management and remote state for collaborative environments.**

---

## 41. Terraform Backend

### Explanation

A **backend** determines where Terraform stores state.

For example, a team may use an S3-based backend with appropriate state-locking or concurrency controls according to the current Terraform and AWS setup.

### Example

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-bucket"
    key    = "lab20/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

The bucket must already exist and should be secured appropriately.

### Result

**Successfully understood the purpose of a Terraform backend for state storage.**

---

## 42. Terraform State Security

### Explanation

Terraform state may contain sensitive information depending on the infrastructure being managed.

Important practices include:

```text
Protect state files
Use encrypted remote storage
Restrict state access
Do not commit local state to GitHub
Use appropriate IAM permissions
Avoid exposing sensitive outputs
```

### Example

```text
Terraform State
      |
      v
Secure Backend
      |
      +---- Encryption
      +---- Access Control
      +---- Versioning
```

### Result

**Successfully understood the importance of protecting Terraform state.**

---

## 43. Terraform Sensitive Variables

### Explanation

Terraform variables can be marked as sensitive so their values are not normally displayed in Terraform CLI output.

### Example

```hcl
variable "database_password" {
  description = "Database password"
  type        = string
  sensitive   = true
}
```

Sensitive values still need proper secret management and should not be treated as automatically secure merely because `sensitive = true` is used.

### Result

**Successfully understood how Terraform can mark variables as sensitive and why secret management remains important.**

---

## 44. Terraform Security

### Explanation

Terraform infrastructure should follow least-privilege and secure Infrastructure as Code practices.

Important practices include:

```text
Use least-privilege IAM permissions
Protect Terraform state
Do not hard-code credentials
Do not commit secrets
Use secure secret management
Review terraform plan before apply
Protect remote state
Use version control
Validate configurations
Restrict Terraform execution permissions
```

### Example

```text
Terraform
    |
    v
IAM
    |
    v
Least Privilege
    |
    v
AWS API
    |
    v
AWS Resources
```

### Result

**Successfully understood important security practices for Terraform and AWS Infrastructure as Code.**

---

## 45. Terraform Practical Lab - Complete VPC

### Explanation

In this practical lab, Terraform is used to create a VPC, subnet, and Security Group.

### Complete Code

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_vpc" "lab_vpc" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name      = "Lab20-Terraform-VPC"
    Environment = "Lab"
    ManagedBy = "Terraform"
  }
}

resource "aws_subnet" "lab_subnet" {
  vpc_id     = aws_vpc.lab_vpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name      = "Lab20-Terraform-Subnet"
    ManagedBy = "Terraform"
  }
}

resource "aws_security_group" "lab_sg" {
  name        = "lab20-terraform-sg"
  description = "Security group for Terraform lab"
  vpc_id      = aws_vpc.lab_vpc.id

  tags = {
    Name      = "Lab20-Terraform-SG"
    ManagedBy = "Terraform"
  }
}

output "vpc_id" {
  description = "Terraform Lab VPC ID"
  value       = aws_vpc.lab_vpc.id
}

output "subnet_id" {
  description = "Terraform Lab Subnet ID"
  value       = aws_subnet.lab_subnet.id
}

output "security_group_id" {
  description = "Terraform Lab Security Group ID"
  value       = aws_security_group.lab_sg.id
}
```

### Practical Steps

### Step 1 - Create Directory

```bash
mkdir terraform-vpc-lab
cd terraform-vpc-lab
```

### Step 2 - Create File

```text
main.tf
```

### Step 3 - Add Code

Paste the complete Terraform configuration into:

```text
main.tf
```

### Step 4 - Initialize

```bash
terraform init
```

### Step 5 - Format

```bash
terraform fmt
```

### Step 6 - Validate

```bash
terraform validate
```

### Step 7 - Plan

```bash
terraform plan
```

### Step 8 - Apply

```bash
terraform apply
```

Enter:

```text
yes
```

when prompted.

### Step 9 - Check Outputs

```bash
terraform output
```

### Step 10 - Verify AWS

Open:

```text
AWS Console
 |
 +---- VPC
 |      |
 |      +---- VPC
 |      +---- Subnet
 |      +---- Security Group
```

### Result

**Successfully created a VPC, subnet, and Security Group using Terraform and verified the resulting AWS infrastructure.**

---

## 46. Terraform Practical Lab - Complete S3

### Complete Code

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

variable "environment" {
  description = "Environment name"
  type        = string
  default     = "lab"
}

resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-unique-bucket-name"

  tags = {
    Name        = "Lab20-S3-Bucket"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

output "bucket_name" {
  description = "S3 bucket name"
  value       = aws_s3_bucket.lab_bucket.id
}

output "bucket_arn" {
  description = "S3 bucket ARN"
  value       = aws_s3_bucket.lab_bucket.arn
}
```

### Practical Steps

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

Verify:

```bash
terraform output
```

Then verify the bucket in:

```text
AWS Console
   |
   v
S3
```

### Result

**Successfully created an S3 bucket using Terraform variables, resources, tags, and outputs.**

---

## 47. Terraform Practical Lab - Variables and Outputs

### File Structure

```text
terraform-lab/
 |
 +---- main.tf
 +---- variables.tf
 +---- outputs.tf
 +---- terraform.tfvars
```

### `variables.tf`

```hcl
variable "aws_region" {
  description = "AWS Region"
  type        = string
  default     = "ap-south-1"
}

variable "environment" {
  description = "Environment"
  type        = string
  default     = "dev"
}
```

### `main.tf`

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = var.aws_region
}

resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-variable-unique"

  tags = {
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}
```

### `outputs.tf`

```hcl
output "bucket_name" {
  description = "S3 bucket name"
  value       = aws_s3_bucket.lab_bucket.id
}

output "bucket_arn" {
  description = "S3 bucket ARN"
  value       = aws_s3_bucket.lab_bucket.arn
}
```

### `terraform.tfvars`

```hcl
aws_region  = "ap-south-1"
environment = "dev"
```

### Practical Steps

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform output
```

### Result

**Successfully used Terraform variables and outputs to create a reusable and configurable infrastructure configuration.**

---

## 48. Terraform Practical Lab - Plan Before Apply

### Explanation

The `terraform plan` command should be reviewed before applying infrastructure changes.

### Practical Steps

```bash
terraform init
```

Then:

```bash
terraform validate
```

Then:

```bash
terraform plan
```

Review:

```text
+ create
~ update
- destroy
```

If the plan is correct:

```bash
terraform apply
```

### Workflow

```text
Code
 |
 v
Validate
 |
 v
Plan
 |
 v
Review
 |
 v
Apply
```

### Result

**Successfully understood the importance of reviewing Terraform plans before applying infrastructure changes.**

---

## 49. Terraform Practical Lab - Destroy

### Explanation

After completing a test lab, Terraform can remove the resources it manages.

### Practical Steps

1. Review the current state:

```bash
terraform show
```

2. Review the planned destruction:

```bash
terraform plan -destroy
```

3. Destroy the resources:

```bash
terraform destroy
```

4. Confirm the operation when prompted.
5. Verify the resources are removed from AWS.

### Result

**Successfully understood how to safely review and destroy Terraform-managed test infrastructure.**

---

## 50. Terraform Troubleshooting

### Explanation

If Terraform fails, check:

```text
Terraform Installation
AWS Credentials
AWS Region
Provider Configuration
IAM Permissions
Terraform Syntax
Resource Configuration
Resource Dependencies
State
Network Connectivity
AWS Service Availability
```

### Troubleshooting Flow

```text
Terraform Error
      |
      v
Check Error Message
      |
      v
terraform validate
      |
      v
Check Provider
      |
      v
Check AWS Credentials
      |
      v
Check IAM Permissions
      |
      v
Check Region
      |
      v
Check Resource Configuration
      |
      v
Check State
      |
      v
terraform plan
      |
      v
Apply Again
```

### Result

**Successfully understood the basic troubleshooting workflow for Terraform deployment errors.**

---

## 51. Terraform Common Errors

### Explanation

Common Terraform problems include:

```text
Provider Configuration Error
Authentication Error
AccessDenied
Invalid Resource Configuration
Invalid Region
State Lock Problem
Resource Already Exists
Dependency Error
Syntax Error
```

### Example

```text
Error
 |
 v
Read Error Message
 |
 v
Identify Resource
 |
 v
Check Configuration
 |
 v
Check IAM
 |
 v
Check AWS
 |
 v
Correct Configuration
```

### Result

**Successfully understood common Terraform errors and the basic troubleshooting process.**

---

## 52. Terraform and GitHub

### Explanation

Terraform projects can be stored in GitHub for version control and collaboration.

A repository can contain:

```text
README.md
main.tf
variables.tf
outputs.tf
providers.tf
modules/
.gitignore
```

### Important Security Rule

```text
DO NOT COMMIT:

AWS Access Keys
AWS Secret Access Keys
Passwords
Private Keys
Terraform State
Sensitive Variables
```

### Example `.gitignore`

```gitignore
.terraform/
*.tfstate
*.tfstate.*
crash.log
*.tfvars
*.tfvars.json
override.tf
override.tf.json
*_override.tf
*_override.tf.json
```

### Result

**Successfully understood how Terraform code can be version-controlled in GitHub while protecting credentials, state, and sensitive configuration.**

---

## 53. Terraform vs CloudFormation

### Explanation

Both Terraform and CloudFormation are Infrastructure as Code tools.

### Terraform

```text
Terraform
 |
 v
Providers
 |
 +---- AWS
 +---- Azure
 +---- GCP
 +---- Other Platforms
```

### CloudFormation

```text
CloudFormation
 |
 v
AWS
 |
 +---- EC2
 +---- S3
 +---- VPC
 +---- RDS
```

### Comparison

| Feature | Terraform | CloudFormation |
|---|---|---|
| IaC | Yes | Yes |
| AWS Support | Yes | Yes |
| Multi-Cloud | Yes | Primarily AWS |
| Configuration | HCL | YAML / JSON |
| State | Terraform State | CloudFormation Stack State |
| Plan Preview | `terraform plan` | Change Sets |
| Apply | `terraform apply` | Stack Update/Create |
| Destroy | `terraform destroy` | Delete Stack |
| Provider Model | Yes | AWS-native resource model |

### Result

**Successfully understood the major differences between Terraform and AWS CloudFormation.**

---

## 54. Terraform Complete Architecture

```text
                         Terraform
                             |
                             v
                    Terraform Configuration
                             |
             +---------------+---------------+
             |               |               |
             v               v               v
          Resources       Variables        Outputs
             |
             v
         AWS Provider
             |
             v
          AWS API
             |
    +--------+--------+--------+--------+
    |        |        |        |        |
    v        v        v        v        v
   VPC      EC2       S3      RDS      Lambda
    |
    v
Terraform State
    |
    v
State Management
```

---

## 55. Terraform Complete Deployment Workflow

### Workflow

```text
Write Terraform Code
        |
        v
terraform fmt
        |
        v
terraform init
        |
        v
terraform validate
        |
        v
terraform plan
        |
        v
Review Plan
        |
        v
terraform apply
        |
        v
AWS Infrastructure
        |
        v
terraform output
        |
        v
Monitor Infrastructure
        |
        v
Modify Code
        |
        v
terraform plan
        |
        v
terraform apply
        |
        v
terraform destroy
```

### Result

**Successfully understood the complete Terraform Infrastructure as Code lifecycle from configuration and initialization through deployment, modification, monitoring, and destruction.**

---

## 56. Terraform Security Best Practices

### Explanation

Important Terraform security practices include:

```text
1. Never hard-code AWS credentials.

2. Never commit AWS credentials to GitHub.

3. Protect Terraform state.

4. Use secure remote state for team environments.

5. Use least-privilege IAM permissions.

6. Review terraform plan before apply.

7. Protect sensitive variables.

8. Use appropriate secret-management solutions.

9. Keep Terraform providers updated.

10. Validate Terraform configurations.

11. Use version control.

12. Review infrastructure changes.

13. Restrict access to Terraform state.

14. Avoid unnecessary public network access.

15. Remove unused test infrastructure.
```

### Result

**Successfully understood important security practices for Terraform-based AWS infrastructure.**

---

## 57. Terraform End-to-End Practical Lab

### Explanation

This practical lab demonstrates the complete Terraform workflow by creating AWS infrastructure, checking the plan, applying the configuration, viewing outputs, and destroying the test resources.

### File Structure

```text
lab20-terraform/
 |
 +---- main.tf
 +---- variables.tf
 +---- outputs.tf
 +---- .gitignore
```

### `main.tf`

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

provider "aws" {
  region = var.aws_region
}

resource "aws_vpc" "lab_vpc" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name        = "Lab20-Terraform-VPC"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

resource "aws_subnet" "lab_subnet" {
  vpc_id     = aws_vpc.lab_vpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name        = "Lab20-Terraform-Subnet"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

resource "aws_security_group" "lab_sg" {
  name        = "lab20-terraform-sg"
  description = "Security group for Terraform lab"
  vpc_id      = aws_vpc.lab_vpc.id

  tags = {
    Name        = "Lab20-Terraform-SG"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

resource "aws_s3_bucket" "lab_bucket" {
  bucket = "aws-lab-terraform-end-to-end-unique"

  tags = {
    Name        = "Lab20-Terraform-Bucket"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}
```

### `variables.tf`

```hcl
variable "aws_region" {
  description = "AWS Region used for the Terraform lab"
  type        = string
  default     = "ap-south-1"
}

variable "environment" {
  description = "Environment name"
  type        = string
  default     = "lab"
}
```

### `outputs.tf`

```hcl
output "vpc_id" {
  description = "VPC ID"
  value       = aws_vpc.lab_vpc.id
}

output "subnet_id" {
  description = "Subnet ID"
  value       = aws_subnet.lab_subnet.id
}

output "security_group_id" {
  description = "Security Group ID"
  value       = aws_security_group.lab_sg.id
}

output "bucket_name" {
  description = "S3 bucket name"
  value       = aws_s3_bucket.lab_bucket.id
}

output "bucket_arn" {
  description = "S3 bucket ARN"
  value       = aws_s3_bucket.lab_bucket.arn
}
```

### `.gitignore`

```gitignore
.terraform/
*.tfstate
*.tfstate.*
crash.log
*.tfvars
*.tfvars.json
override.tf
override.tf.json
*_override.tf
*_override.tf.json
```

### Practical Steps

### Step 1 - Create Project Directory

```bash
mkdir lab20-terraform
cd lab20-terraform
```

### Step 2 - Create Files

```text
main.tf
variables.tf
outputs.tf
.gitignore
```

### Step 3 - Add Terraform Code

Paste the corresponding code into each file.

### Step 4 - Initialize Terraform

```bash
terraform init
```

### Step 5 - Format Code

```bash
terraform fmt
```

### Step 6 - Validate Code

```bash
terraform validate
```

Expected result:

```text
Success! The configuration is valid.
```

### Step 7 - Create Plan

```bash
terraform plan
```

Review:

```text
+ create
```

### Step 8 - Apply Configuration

```bash
terraform apply
```

Confirm:

```text
yes
```

### Step 9 - View Outputs

```bash
terraform output
```

Expected output includes:

```text
vpc_id
subnet_id
security_group_id
bucket_name
bucket_arn
```

### Step 10 - Verify AWS Resources

Open:

```text
AWS Console
 |
 +---- VPC
 +---- Subnets
 +---- Security Groups
 +---- S3
```

Verify the Terraform-created resources.

### Step 11 - Review State

```bash
terraform show
```

### Step 12 - Review Infrastructure Changes

Modify the Terraform configuration if required and run:

```bash
terraform plan
```

### Step 13 - Apply Changes

```bash
terraform apply
```

### Step 14 - Destroy Test Resources

Review the destroy plan:

```bash
terraform plan -destroy
```

Then:

```bash
terraform destroy
```

Confirm:

```text
yes
```

### Step 15 - Verify Cleanup

Check AWS:

```text
VPC
Subnet
Security Group
S3 Bucket
```

Verify that the test resources have been removed as expected.

### Result

**Successfully completed an end-to-end Terraform Infrastructure as Code lab by configuring the AWS provider, creating VPC, subnet, Security Group, and S3 resources, using variables and outputs, initializing and validating Terraform, reviewing plans, applying infrastructure, inspecting Terraform state, and destroying the test infrastructure.**

---

## 58. Final Terraform Workflow

```text
                         TERRAFORM
                             |
                             v
                  Infrastructure as Code
                             |
                             v
                         HCL Files
                             |
          +------------------+------------------+
          |                  |                  |
          v                  v                  v
      Resources          Variables           Outputs
          |                  |                  |
          +------------------+------------------+
                             |
                             v
                      terraform init
                             |
                             v
                      terraform fmt
                             |
                             v
                    terraform validate
                             |
                             v
                      terraform plan
                             |
                             v
                       Review Plan
                             |
                             v
                     terraform apply
                             |
                             v
                       AWS Provider
                             |
                             v
                         AWS API
                             |
       +---------------------+---------------------+
       |          |          |          |          |
       v          v          v          v          v
      VPC        EC2         S3        RDS      Lambda
       |
       v
Terraform State
       |
       v
State Management
       |
       v
Monitoring / Updates
       |
       v
terraform destroy
```

### Final Result

**Successfully completed Lab 20 - Terraform and understood Infrastructure as Code, HCL, Terraform providers, resources, variables, outputs, data sources, dependencies, state, backends, modules, `terraform init`, `terraform fmt`, `terraform validate`, `terraform plan`, `terraform apply`, `terraform destroy`, AWS resource management, VPC, EC2, S3, Security Groups, IAM, RDS, Lambda, CloudWatch, CloudTrail, GitHub integration, troubleshooting, state security, and Terraform best practices.**
