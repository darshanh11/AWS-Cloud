# Lab 18 - AWS CLI

## Objective

The objective of this lab is to understand the **AWS Command Line Interface (AWS CLI)** and practically learn how to configure AWS CLI, authenticate securely, manage AWS resources, and perform AWS operations using commands.

This lab covers:

- AWS CLI
- AWS CLI Installation
- AWS CLI Configuration
- AWS Credentials
- Access Key
- Secret Access Key
- AWS Region
- Output Format
- AWS CLI Profiles
- IAM
- STS
- EC2
- S3
- IAM Users
- IAM Roles
- CloudWatch
- CloudTrail
- VPC
- Security
- Authentication
- Authorization
- Practical AWS CLI Commands
- Troubleshooting
- Security Best Practices

---

## 1. What is AWS CLI?

### Explanation

**AWS Command Line Interface (AWS CLI)** is a command-line tool that allows users to interact with AWS services using commands instead of only using the AWS Management Console.

### Example

```text
AWS Management Console
        |
        v
     AWS Services


AWS CLI
   |
   v
Terminal
   |
   v
AWS Services
```

### Result

**Successfully understood that AWS CLI allows users to manage AWS resources from a command-line terminal.**

---

## 2. Why is AWS CLI Used?

### Explanation

AWS CLI is useful for:

- Managing AWS resources
- Automating tasks
- Running repeatable commands
- Troubleshooting
- Scripting
- Deploying resources
- Checking AWS resources quickly

### Example

```text
Terminal
   |
   v
AWS CLI
   |
   +---- EC2
   +---- S3
   +---- IAM
   +---- VPC
   +---- CloudWatch
   +---- CloudTrail
```

### Result

**Successfully understood why AWS CLI is useful for AWS administration, automation, and troubleshooting.**

---

## 3. AWS CLI Command Structure

### Explanation

AWS CLI commands generally follow this structure:

```bash
aws <service> <command> [options]
```

### Example

```bash
aws s3 ls
```

Explanation:

```text
aws
 |
 +---- AWS CLI command

s3
 |
 +---- AWS S3 service

ls
 |
 +---- List command
```

### Result

**Successfully understood the basic structure of an AWS CLI command.**

---

## 4. Installing AWS CLI on Windows

### Explanation

AWS CLI can be installed on Windows using the official AWS CLI installer.

After installation, verify that the CLI is available from Command Prompt or PowerShell.

### Practical Steps

1. Install AWS CLI.
2. Open **Command Prompt** or **PowerShell**.
3. Run:

```powershell
aws --version
```

### Example Result

```text
aws-cli/2.x.x
```

The exact version will depend on the installed AWS CLI version.

### Result

**Successfully installed AWS CLI on Windows and verified the installation using the `aws --version` command.**

---

## 5. Installing AWS CLI on Linux / Ubuntu

### Explanation

AWS CLI can also be installed on Linux systems such as Ubuntu.

After installation, verify the installation from the terminal.

### Practical Steps

1. Open Ubuntu Terminal.
2. Install AWS CLI using the appropriate installation method.
3. Verify the installation:

```bash
aws --version
```

### Example Result

```text
aws-cli/2.x.x
```

### Result

**Successfully understood how to install and verify AWS CLI on a Linux/Ubuntu system.**

---

## 6. AWS CLI Version

### Explanation

The following command displays the installed AWS CLI version.

```bash
aws --version
```

### Example

```text
aws-cli/2.x.x Python/3.x.x Linux/x86_64
```

The exact output depends on the installed version and operating system.

### Result

**Successfully verified the installed AWS CLI version.**

---

## 7. AWS CLI Configuration

### Explanation

Before using AWS CLI to perform authenticated AWS operations, configure credentials and default settings.

The standard configuration command is:

```bash
aws configure
```

### Practical Steps

Run:

```bash
aws configure
```

AWS CLI asks for values such as:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default region name:
Default output format:
```

Example:

```text
AWS Access Key ID:
AKIAxxxxxxxxxxxxxxxx

AWS Secret Access Key:
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

Default region name:
ap-south-1

Default output format:
json
```

**Never put real credentials in a GitHub repository.**

### Result

**Successfully understood the basic AWS CLI configuration process.**

---

## 8. AWS Access Key

### Explanation

An **Access Key ID** identifies the credentials used by an AWS API request.

Example format:

```text
AKIAxxxxxxxxxxxxxxxx
```

Access keys are sensitive credentials and must be protected.

### Security Rule

```text
DO NOT:

Paste Access Key into GitHub
Paste Access Key into README
Share Access Key publicly
Hard-code Access Key into source code
```

### Result

**Successfully understood the purpose and security importance of AWS Access Keys.**

---

## 9. AWS Secret Access Key

### Explanation

The **Secret Access Key** is the secret component associated with an access key credential.

It is used by AWS CLI to authenticate API requests.

### Security Rule

```text
Secret Access Key
       |
       X
    NEVER
       |
       +---- GitHub
       +---- Public Chat
       +---- Public Code
       +---- Screenshots
```

### Result

**Successfully understood why Secret Access Keys must remain private.**

---

## 10. AWS Region

### Explanation

An AWS Region identifies the geographic AWS location where resources are created or managed.

Example:

```text
ap-south-1
```

which represents the Mumbai Region.

### Configure Region

```bash
aws configure
```

Example:

```text
Default region name:
ap-south-1
```

### Check Region

```bash
aws configure get region
```

### Result

**Successfully understood how AWS CLI uses a default AWS Region for commands.**

---

## 11. AWS CLI Output Formats

### Explanation

AWS CLI supports different output formats.

Common formats include:

```text
json
text
table
yaml
yaml-stream
```

### Example

```bash
aws ec2 describe-instances --output table
```

or:

```bash
aws ec2 describe-instances --output json
```

### Result

**Successfully understood how AWS CLI output formats can be changed according to the required use case.**

---

## 12. AWS CLI Profiles

### Explanation

AWS CLI profiles allow different configuration sets to be stored and selected.

Example:

```text
default
dev
test
production
```

### Create a Profile

```bash
aws configure --profile dev
```

### Use a Profile

```bash
aws s3 ls --profile dev
```

### Example

```text
AWS CLI
 |
 +---- default
 |
 +---- dev
 |
 +---- test
```

### Result

**Successfully understood how AWS CLI profiles can be used to manage different AWS configurations.**

---

## 13. Checking AWS CLI Configuration

### Explanation

The following command can display the configured AWS CLI settings and where they are loaded from.

```bash
aws configure list
```

### Example

```text
Name                    Value
----                    -----
profile                 <not set>
access_key              ****************
secret_key              ****************
region                  ap-south-1
```

Sensitive credentials are masked by the CLI.

### Result

**Successfully learned how to inspect the active AWS CLI configuration without displaying the complete secret credentials.**

---

## 14. Testing AWS CLI Authentication

### Explanation

AWS Security Token Service (STS) provides a useful command for checking which AWS identity is being used.

### Command

```bash
aws sts get-caller-identity
```

### Example Result

```json
{
    "UserId": "XXXXXXXXXXXX",
    "Account": "XXXXXXXXXXXX",
    "Arn": "arn:aws:iam::XXXXXXXXXXXX:user/example"
}
```

The exact values depend on the identity being used.

### Result

**Successfully verified the AWS identity being used by AWS CLI.**

---

## 15. AWS CLI Authentication vs Authorization

### Explanation

**Authentication** answers:

```text
Who are you?
```

**Authorization** answers:

```text
What are you allowed to do?
```

### Example

```text
AWS CLI
   |
   v
Authentication
   |
   v
IAM Identity
   |
   v
Authorization
   |
   v
IAM Permissions
   |
   v
AWS Resource
```

### Result

**Successfully understood the difference between authentication and authorization when using AWS CLI.**

---

## 16. AWS CLI and IAM

### Explanation

AWS CLI uses AWS identities and permissions to perform actions.

IAM permissions determine which AWS API operations the authenticated identity is allowed to perform.

### Example

```text
AWS CLI
   |
   v
IAM Identity
   |
   v
IAM Policy
   |
   v
AWS Permission
   |
   v
AWS Service
```

### Result

**Successfully understood how IAM controls AWS CLI access to AWS services.**

---

## 17. AWS CLI - IAM Users

### Explanation

AWS CLI can be used to manage IAM users when the authenticated identity has the required permissions.

### List IAM Users

```bash
aws iam list-users
```

### Result

**Successfully understood how AWS CLI can retrieve IAM user information.**

---

## 18. AWS CLI - Create IAM User

### Explanation

An IAM user can be created using AWS CLI when appropriate permissions are available.

### Command

```bash
aws iam create-user --user-name aws-lab-user
```

### Example Result

```json
{
    "User": {
        "UserName": "aws-lab-user"
    }
}
```

### Result

**Successfully understood how AWS CLI can create an IAM user.**

---

## 19. AWS CLI - Delete IAM User

### Explanation

An IAM user can be deleted using AWS CLI after ensuring that the user and its associated resources are no longer required.

### Command

```bash
aws iam delete-user --user-name aws-lab-user
```

### Result

**Successfully understood how AWS CLI can delete an IAM user when the required permissions and cleanup conditions are satisfied.**

---

## 20. AWS CLI - S3

### Explanation

AWS CLI provides commands for managing Amazon S3 buckets and objects.

### List Buckets

```bash
aws s3 ls
```

### Result

```text
S3 Buckets
   |
   +---- Bucket 1
   +---- Bucket 2
   +---- Bucket 3
```

### Result

**Successfully retrieved the S3 buckets accessible to the configured AWS identity.**

---

## 21. AWS CLI - Create S3 Bucket

### Explanation

An S3 bucket can be created using AWS CLI.

For a bucket in a Region other than `us-east-1`, the create-bucket command normally requires the appropriate location constraint.

### Example for ap-south-1

```bash
aws s3api create-bucket \
    --bucket aws-lab-cli-bucket-unique \
    --region ap-south-1 \
    --create-bucket-configuration LocationConstraint=ap-south-1
```

### Result

**Successfully understood how AWS CLI can create an S3 bucket using the S3 API.**

---

## 22. AWS CLI - Upload File to S3

### Explanation

The `aws s3 cp` command can copy files between local storage and S3.

### Command

```bash
aws s3 cp test.txt s3://aws-lab-cli-bucket-unique/
```

### Example

```text
Local File
    |
    v
AWS CLI
    |
    v
S3 Bucket
```

### Result

**Successfully understood how AWS CLI can upload a local file to an S3 bucket.**

---

## 23. AWS CLI - List S3 Objects

### Command

```bash
aws s3 ls s3://aws-lab-cli-bucket-unique/
```

### Example Result

```text
test.txt
```

### Result

**Successfully verified objects stored in the S3 bucket using AWS CLI.**

---

## 24. AWS CLI - Download S3 Object

### Command

```bash
aws s3 cp s3://aws-lab-cli-bucket-unique/test.txt .
```

### Example

```text
S3
 |
 v
AWS CLI
 |
 v
Local Computer
```

### Result

**Successfully understood how AWS CLI can download an S3 object to local storage.**

---

## 25. AWS CLI - EC2

### Explanation

AWS CLI can be used to retrieve and manage EC2 resources.

### List EC2 Instances

```bash
aws ec2 describe-instances
```

### Example

```text
AWS CLI
   |
   v
EC2
   |
   v
Instances
```

### Result

**Successfully retrieved EC2 instance information using AWS CLI.**

---

## 26. AWS CLI - List Running EC2 Instances

### Explanation

EC2 instance information can be filtered using CLI options and JMESPath queries.

### Command

```bash
aws ec2 describe-instances \
    --filters Name=instance-state-name,Values=running
```

### Result

**Successfully understood how to filter EC2 instances by their running state using AWS CLI.**

---

## 27. AWS CLI - Start EC2 Instance

### Explanation

An EC2 instance can be started using the AWS CLI when the IAM identity has the required permission.

### Command

```bash
aws ec2 start-instances \
    --instance-ids <INSTANCE-ID>
```

### Example

```text
AWS CLI
   |
   v
StartInstances
   |
   v
EC2
   |
   v
Running
```

### Result

**Successfully understood how AWS CLI can start an EC2 instance.**

---

## 28. AWS CLI - Stop EC2 Instance

### Explanation

An EC2 instance can be stopped using AWS CLI when the required permission is available.

### Command

```bash
aws ec2 stop-instances \
    --instance-ids <INSTANCE-ID>
```

### Example

```text
AWS CLI
   |
   v
StopInstances
   |
   v
EC2
   |
   v
Stopped
```

### Result

**Successfully understood how AWS CLI can stop an EC2 instance.**

---

## 29. AWS CLI - VPC

### Explanation

AWS CLI can retrieve information about VPC resources.

### List VPCs

```bash
aws ec2 describe-vpcs
```

### List Subnets

```bash
aws ec2 describe-subnets
```

### List Route Tables

```bash
aws ec2 describe-route-tables
```

### List Internet Gateways

```bash
aws ec2 describe-internet-gateways
```

### Result

**Successfully understood how AWS CLI can retrieve VPC, subnet, route table, and Internet Gateway information.**

---

## 30. AWS CLI - Security Groups

### Explanation

Security Group information can be retrieved using AWS CLI.

### Command

```bash
aws ec2 describe-security-groups
```

### Example

```text
AWS CLI
   |
   v
EC2 API
   |
   v
Security Groups
```

### Result

**Successfully understood how AWS CLI can retrieve Security Group information.**

---

## 31. AWS CLI - CloudWatch

### Explanation

AWS CLI can be used to retrieve CloudWatch metrics and manage CloudWatch resources when the required permissions are available.

### Example

```bash
aws cloudwatch list-metrics
```

### Get a Metric Statistic

```bash
aws cloudwatch get-metric-statistics \
    --namespace AWS/EC2 \
    --metric-name CPUUtilization \
    --dimensions Name=InstanceId,Value=<INSTANCE-ID> \
    --statistics Average \
    --period 300 \
    --start-time <START-TIME> \
    --end-time <END-TIME>
```

### Result

**Successfully understood how AWS CLI can retrieve CloudWatch metric information.**

---

## 32. AWS CLI - CloudTrail

### Explanation

AWS CLI can be used to look up CloudTrail events when the required permissions are available.

### Command

```bash
aws cloudtrail lookup-events
```

### Example

```text
AWS CLI
   |
   v
CloudTrail
   |
   v
Event History
```

### Result

**Successfully understood how AWS CLI can retrieve CloudTrail event information.**

---

## 33. AWS CLI Help Command

### Explanation

AWS CLI includes built-in help documentation.

### General Help

```bash
aws help
```

### Service Help

```bash
aws ec2 help
```

### Command Help

```bash
aws ec2 describe-instances help
```

### Result

**Successfully understood how to use AWS CLI built-in help to learn service and command syntax.**

---

## 34. AWS CLI Dry Run

### Explanation

Some AWS CLI commands support a `--dry-run` option.

Dry run can help verify whether the command is authorized without actually performing the requested operation, where supported.

### Example

```bash
aws ec2 run-instances \
    --image-id <AMI-ID> \
    --instance-type <INSTANCE-TYPE> \
    --dry-run
```

### Result

**Successfully understood the purpose of the AWS CLI dry-run option where supported.**

---

## 35. AWS CLI Query Option

### Explanation

AWS CLI supports the `--query` option to filter and format returned JSON data using JMESPath expressions.

### Example

```bash
aws ec2 describe-instances \
    --query "Reservations[].Instances[].InstanceId"
```

### Result

```text
[
    "i-xxxxxxxxxxxxxxxxx"
]
```

### Result

**Successfully understood how the `--query` option can extract specific information from AWS CLI output.**

---

## 36. AWS CLI Output with Table

### Command

```bash
aws ec2 describe-instances \
    --query "Reservations[].Instances[].{Instance:InstanceId,State:State.Name,Type:InstanceType}" \
    --output table
```

### Example

```text
----------------------------------------
|          DescribeInstances           |
+----------------+---------------------+
| Instance       | State               |
+----------------+---------------------+
| i-xxxxxxxx     | running             |
+----------------+---------------------+
```

### Result

**Successfully understood how AWS CLI can format filtered output into a readable table.**

---

## 37. AWS CLI Environment Variables

### Explanation

AWS CLI can obtain credentials and configuration from environment variables.

Common variables include:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_SESSION_TOKEN
AWS_DEFAULT_REGION
```

### Example

```bash
export AWS_DEFAULT_REGION=ap-south-1
```

For temporary credentials, an appropriate session token may also be required.

### Security Warning

```text
Do NOT:

echo secrets into shared terminals
store credentials in scripts
commit credentials to GitHub
share terminal screenshots containing credentials
```

### Result

**Successfully understood how AWS CLI can use environment variables for configuration and temporary credentials.**

---

## 38. AWS CLI Credentials Files

### Explanation

AWS CLI commonly uses configuration and credential files in the user's AWS configuration directory.

Typical files include:

```text
~/.aws/credentials
~/.aws/config
```

On Windows, the equivalent location is generally under:

```text
%UserProfile%\.aws\
```

### Example Structure

```text
.aws
 |
 +---- credentials
 |
 +---- config
```

### Result

**Successfully understood where AWS CLI commonly stores profile configuration and credentials.**

---

## 39. AWS CLI with IAM Role

### Explanation

When running AWS CLI from an AWS resource such as an EC2 instance, an IAM role can provide temporary credentials without storing long-term access keys on the instance.

### Example

```text
EC2
 |
 v
IAM Role
 |
 v
Temporary Credentials
 |
 v
AWS CLI
 |
 v
AWS Services
```

### Result

**Successfully understood why IAM roles are preferred over storing long-term access keys on AWS resources when applicable.**

---

## 40. AWS CLI Security

### Explanation

AWS CLI credentials provide access to AWS resources and must be protected.

Important security practices include:

```text
Use IAM roles when appropriate
Use least privilege
Avoid long-term access keys when unnecessary
Never commit credentials to GitHub
Rotate credentials when required
Use temporary credentials when appropriate
Protect local credential files
Use separate profiles carefully
```

### Example

```text
Secure Authentication
        |
        v
IAM
        |
        v
Least Privilege
        |
        v
AWS CLI
        |
        v
AWS Resources
```

### Result

**Successfully understood important security practices for AWS CLI authentication and authorization.**

---

## 41. Practical Lab - AWS CLI Configuration

### Explanation

In this practical lab, AWS CLI is installed, configured, authenticated, and tested.

### Practical Steps

### Step 1 - Verify Installation

```bash
aws --version
```

### Step 2 - Configure AWS CLI

```bash
aws configure
```

Enter the required values securely.

Example:

```text
AWS Access Key ID:
<YOUR-ACCESS-KEY>

AWS Secret Access Key:
<YOUR-SECRET-ACCESS-KEY>

Default region name:
ap-south-1

Default output format:
json
```

### Step 3 - Check Configuration

```bash
aws configure list
```

### Step 4 - Verify Identity

```bash
aws sts get-caller-identity
```

### Step 5 - Test S3

```bash
aws s3 ls
```

### Step 6 - Test EC2

```bash
aws ec2 describe-instances
```

### Result

**Successfully configured AWS CLI, verified the active AWS identity, and tested access to AWS services.**

---

## 42. Practical Lab - AWS CLI S3

### Explanation

In this practical lab, AWS CLI is used to create, upload, list, and download an S3 object.

### Practical Steps

### Step 1 - Create Test File

Linux:

```bash
echo "AWS CLI Lab" > test.txt
```

Windows PowerShell:

```powershell
" AWS CLI Lab".Trim() | Out-File test.txt
```

### Step 2 - Create S3 Bucket

Use a globally unique bucket name.

For example:

```bash
aws s3api create-bucket \
    --bucket aws-lab-cli-bucket-unique \
    --region ap-south-1 \
    --create-bucket-configuration LocationConstraint=ap-south-1
```

### Step 3 - Upload File

```bash
aws s3 cp test.txt s3://aws-lab-cli-bucket-unique/
```

### Step 4 - List Object

```bash
aws s3 ls s3://aws-lab-cli-bucket-unique/
```

### Step 5 - Download Object

```bash
aws s3 cp s3://aws-lab-cli-bucket-unique/test.txt downloaded-test.txt
```

### Step 6 - Verify

```text
Local File
    |
    v
AWS CLI
    |
    v
S3 Bucket
    |
    v
S3 Object
```

### Result

**Successfully used AWS CLI to create an S3 bucket, upload an object, list the object, and download it.**

---

## 43. Practical Lab - AWS CLI EC2

### Explanation

In this practical lab, AWS CLI is used to inspect EC2 instances and perform basic instance operations.

### Practical Steps

### Step 1 - List EC2 Instances

```bash
aws ec2 describe-instances
```

### Step 2 - Find Running Instances

```bash
aws ec2 describe-instances \
    --filters Name=instance-state-name,Values=running
```

### Step 3 - Extract Instance IDs

```bash
aws ec2 describe-instances \
    --query "Reservations[].Instances[].InstanceId"
```

### Step 4 - Check Specific Instance

```bash
aws ec2 describe-instances \
    --instance-ids <INSTANCE-ID>
```

### Step 5 - Stop Test Instance

```bash
aws ec2 stop-instances \
    --instance-ids <INSTANCE-ID>
```

### Step 6 - Start Test Instance

```bash
aws ec2 start-instances \
    --instance-ids <INSTANCE-ID>
```

### Result

**Successfully used AWS CLI to inspect and perform basic EC2 instance operations.**

---

## 44. Practical Lab - AWS CLI IAM

### Explanation

In this practical lab, AWS CLI is used to inspect IAM users and understand IAM-based authorization.

### Practical Steps

### Step 1 - List IAM Users

```bash
aws iam list-users
```

### Step 2 - Create Test IAM User

```bash
aws iam create-user \
    --user-name aws-cli-lab-user
```

### Step 3 - Verify User

```bash
aws iam get-user \
    --user-name aws-cli-lab-user
```

### Step 4 - Delete Test User

```bash
aws iam delete-user \
    --user-name aws-cli-lab-user
```

### Result

**Successfully used AWS CLI to perform basic IAM user management operations and understood that IAM permissions control which CLI actions are allowed.**

---

## 45. Practical Lab - AWS CLI CloudWatch

### Explanation

In this practical lab, AWS CLI is used to retrieve CloudWatch metrics.

### Practical Steps

### Step 1 - List Metrics

```bash
aws cloudwatch list-metrics
```

### Step 2 - Filter EC2 Metrics

```bash
aws cloudwatch list-metrics \
    --namespace AWS/EC2
```

### Step 3 - Query CPU Metric

```bash
aws cloudwatch list-metrics \
    --namespace AWS/EC2 \
    --metric-name CPUUtilization
```

### Step 4 - Review the Metric

Identify:

```text
InstanceId
Metric Name
Namespace
```

### Result

**Successfully used AWS CLI to retrieve and inspect CloudWatch EC2 metrics.**

---

## 46. Practical Lab - AWS CLI CloudTrail

### Explanation

In this practical lab, AWS CLI is used to retrieve CloudTrail events.

### Practical Steps

### Step 1 - List Recent Events

```bash
aws cloudtrail lookup-events
```

### Step 2 - Filter Events

Example:

```bash
aws cloudtrail lookup-events \
    --lookup-attributes AttributeKey=EventName,AttributeValue=RunInstances
```

### Step 3 - Review Event

Check:

```text
Event Name
Event Source
Username
Event Time
AWS Region
Source IP Address
```

### Result

**Successfully used AWS CLI to retrieve and investigate CloudTrail events.**

---

## 47. AWS CLI Automation with Shell Script

### Explanation

AWS CLI commands can be combined into scripts to automate repetitive AWS administration tasks.

### Example

```bash
#!/bin/bash

echo "AWS CLI Lab"

echo "Checking AWS identity..."
aws sts get-caller-identity

echo "Listing S3 buckets..."
aws s3 ls

echo "Listing EC2 instances..."
aws ec2 describe-instances \
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name}" \
    --output table
```

### Result

**Successfully understood how AWS CLI commands can be combined in scripts for basic AWS automation.**

---

## 48. AWS CLI Troubleshooting

### Explanation

If an AWS CLI command fails, check:

```text
AWS CLI Installation
Credentials
IAM Permissions
AWS Region
Profile
Network Connectivity
Command Syntax
Resource ID
Service Availability
```

### Troubleshooting Flow

```text
AWS CLI Command Failed
        |
        v
Check AWS CLI Version
        |
        v
Check Credentials
        |
        v
Check AWS Identity
        |
        v
Check IAM Permissions
        |
        v
Check Region
        |
        v
Check Profile
        |
        v
Check Command Syntax
        |
        v
Check Resource ID
        |
        v
Run Again
```

### Result

**Successfully understood the basic troubleshooting process for AWS CLI command failures.**

---

## 49. Common AWS CLI Errors

### Explanation

Common AWS CLI errors include:

```text
Unable to locate credentials
AccessDenied
ExpiredToken
InvalidClientTokenId
ResourceNotFound
ValidationError
Unknown options
```

### Example

```text
Unable to locate credentials
        |
        v
Check:
aws configure
        |
        v
Check:
aws configure list
        |
        v
Check:
aws sts get-caller-identity
```

### Result

**Successfully understood common AWS CLI errors and the basic troubleshooting approach.**

---

## 50. AWS CLI Principle of Least Privilege

### Explanation

The AWS CLI should be used with an identity that has only the permissions required for the task.

### Example

```text
AWS CLI
   |
   v
IAM Policy
   |
   +---- Required Permission
   |
   X---- Unnecessary Permission
```

Instead of granting broad administrative permissions, use specific permissions whenever possible.

### Result

**Successfully understood how the Principle of Least Privilege applies to AWS CLI access.**

---

## 51. AWS CLI Complete Architecture

```text
                              User
                               |
                               v
                            Terminal
                               |
                               v
                            AWS CLI
                               |
                               v
                         Authentication
                               |
                               v
                              IAM
                               |
                       +-------+-------+
                       |               |
                       v               v
                  Credentials       IAM Role
                       |               |
                       +-------+-------+
                               |
                               v
                         Authorization
                               |
                               v
                         AWS API Calls
                               |
             +-----------------+-----------------+
             |        |        |        |        |
             v        v        v        v        v
            EC2      S3       IAM      VPC   CloudWatch
```

---

## 52. AWS CLI Authentication Flow

```text
AWS CLI
   |
   v
Credentials / IAM Role
   |
   v
AWS Authentication
   |
   v
Identify AWS Principal
   |
   v
IAM Authorization
   |
   v
Check Permissions
   |
   +---- Allowed ------> AWS API
   |
   +---- Denied -------> AccessDenied
```

### Result

**Successfully understood the AWS CLI authentication and authorization flow.**

---

## 53. AWS CLI with Previous AWS Labs

### Explanation

AWS CLI can be used with many services covered in previous labs.

### Example

```text
Lab 02 - IAM
       |
       v
AWS CLI
       |
       +---- IAM Commands


Lab 03 - EC2
       |
       v
AWS CLI
       |
       +---- EC2 Commands


Lab 04 - S3
       |
       v
AWS CLI
       |
       +---- S3 Commands


Lab 08 - Internet Gateway
       |
       v
AWS CLI
       |
       +---- VPC Commands


Lab 09 - Security Groups
       |
       v
AWS CLI
       |
       +---- EC2 Security Group Commands


Lab 12 - Load Balancer
       |
       v
AWS CLI
       |
       +---- ELB Commands


Lab 13 - Auto Scaling
       |
       v
AWS CLI
       |
       +---- Auto Scaling Commands


Lab 14 - RDS
       |
       v
AWS CLI
       |
       +---- RDS Commands


Lab 15 - CloudWatch
       |
       v
AWS CLI
       |
       +---- CloudWatch Commands


Lab 16 - CloudTrail
       |
       v
AWS CLI
       |
       +---- CloudTrail Commands


Lab 17 - Lambda
       |
       v
AWS CLI
       |
       +---- Lambda Commands
```

### Result

**Successfully understood how AWS CLI can be used as a command-line management interface across multiple AWS services.**

---

## 54. AWS CLI Service Commands

### Common Commands

```bash
# IAM
aws iam list-users

# EC2
aws ec2 describe-instances

# S3
aws s3 ls

# VPC
aws ec2 describe-vpcs

# Subnets
aws ec2 describe-subnets

# Security Groups
aws ec2 describe-security-groups

# RDS
aws rds describe-db-instances

# Lambda
aws lambda list-functions

# CloudWatch
aws cloudwatch list-metrics

# CloudTrail
aws cloudtrail lookup-events

# Auto Scaling
aws autoscaling describe-auto-scaling-groups

# Load Balancer
aws elbv2 describe-load-balancers
```

### Result

**Successfully understood common AWS CLI commands for the AWS services covered in the lab series.**

---

## 55. AWS CLI Practical End-to-End Lab

### Explanation

This practical lab demonstrates a basic AWS CLI workflow from authentication to resource inspection.

### Practical Steps

### Step 1 - Verify Installation

```bash
aws --version
```

### Step 2 - Configure CLI

```bash
aws configure
```

Configure:

```text
Region:
ap-south-1

Output:
json
```

### Step 3 - Verify Identity

```bash
aws sts get-caller-identity
```

### Step 4 - List S3 Buckets

```bash
aws s3 ls
```

### Step 5 - List EC2 Instances

```bash
aws ec2 describe-instances \
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name}" \
    --output table
```

### Step 6 - List VPCs

```bash
aws ec2 describe-vpcs \
    --output table
```

### Step 7 - List Security Groups

```bash
aws ec2 describe-security-groups \
    --output table
```

### Step 8 - List RDS Databases

```bash
aws rds describe-db-instances \
    --query "DBInstances[].{ID:DBInstanceIdentifier,Status:DBInstanceStatus,Engine:Engine}" \
    --output table
```

### Step 9 - List Lambda Functions

```bash
aws lambda list-functions \
    --query "Functions[].{Name:FunctionName,Runtime:Runtime}" \
    --output table
```

### Step 10 - Check CloudTrail

```bash
aws cloudtrail lookup-events
```

### Step 11 - Check CloudWatch Metrics

```bash
aws cloudwatch list-metrics
```

### Result

**Successfully completed an end-to-end AWS CLI exercise covering authentication, S3, EC2, VPC, Security Groups, RDS, Lambda, CloudTrail, and CloudWatch.**

---

## 56. AWS CLI Security Best Practices

### Explanation

AWS CLI should always be configured with security in mind.

Important practices include:

```text
1. Use IAM roles whenever appropriate.

2. Follow least privilege.

3. Never commit AWS credentials to GitHub.

4. Never place real credentials inside README files.

5. Never hard-code Secret Access Keys into scripts.

6. Use temporary credentials when appropriate.

7. Protect ~/.aws/credentials.

8. Use separate AWS CLI profiles carefully.

9. Rotate long-term credentials when required.

10. Monitor AWS activity using CloudTrail.

11. Remove unused access keys.

12. Use MFA and strong authentication controls where appropriate.

13. Avoid using the root account for routine CLI administration.

14. Review IAM permissions regularly.
```

### Result

**Successfully understood the security practices required when using AWS CLI to manage AWS resources.**

---

## 57. Complete AWS CLI Workflow

### Workflow

```text
Install AWS CLI
       |
       v
Verify Version
       |
       v
Configure Credentials
       |
       v
Configure Region
       |
       v
Configure Output
       |
       v
Verify Identity
       |
       v
IAM Authorization
       |
       v
AWS API Request
       |
       v
AWS Service
       |
       v
Response
       |
       v
Query / Filter / Output
       |
       v
Automation / Administration
```

### Practical Steps

1. Install AWS CLI.
2. Verify the installation.
3. Configure AWS credentials securely.
4. Configure the default AWS Region.
5. Configure the output format.
6. Create profiles when required.
7. Verify the active configuration.
8. Run `aws sts get-caller-identity`.
9. Verify IAM permissions.
10. Run AWS service commands.
11. Use `--query` to filter results.
12. Use `--output` to format results.
13. Use scripts for repetitive tasks.
14. Monitor activity with CloudTrail.
15. Monitor resources with CloudWatch.
16. Follow least-privilege security practices.
17. Remove test resources after completing the lab.

### Final Result

**Successfully completed Lab 18 - AWS CLI and understood how to use the AWS Command Line Interface to authenticate with AWS, inspect and manage AWS resources, automate tasks, work with IAM, EC2, S3, VPC, RDS, Lambda, CloudWatch, CloudTrail, Auto Scaling, and Load Balancers, and troubleshoot AWS CLI operations securely.**
