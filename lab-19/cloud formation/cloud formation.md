# Lab 19 - AWS CloudFormation

## Objective

The objective of this lab is to understand **AWS CloudFormation** and practically learn how to create, configure, deploy, update, and delete AWS infrastructure using Infrastructure as Code (IaC).

This lab covers:

- AWS CloudFormation
- Infrastructure as Code (IaC)
- CloudFormation Templates
- YAML
- JSON
- Stacks
- Resources
- Parameters
- Mappings
- Conditions
- Outputs
- Intrinsic Functions
- References
- Dependencies
- Change Sets
- Stack Updates
- Stack Events
- Stack Resources
- Stack Outputs
- Rollback
- Drift Detection
- CloudFormation Designer
- IAM Permissions
- EC2
- S3
- VPC
- Security Groups
- CloudFormation CLI
- CloudFormation Security
- Practical CloudFormation Configuration
- Troubleshooting
- Best Practices

---

## 1. What is AWS CloudFormation?

### Explanation

**AWS CloudFormation** is an Infrastructure as Code service that allows you to define AWS infrastructure in a template and provision those resources automatically.

Instead of manually creating every resource through the AWS Management Console, CloudFormation allows you to describe the desired infrastructure in a template.

### Example

```text
CloudFormation Template
        |
        v
CloudFormation Stack
        |
        +---- VPC
        +---- Subnet
        +---- Security Group
        +---- EC2
        +---- S3
```

### Result

**Successfully understood that AWS CloudFormation can provision and manage AWS infrastructure using templates.**

---

## 2. What is Infrastructure as Code?

### Explanation

**Infrastructure as Code (IaC)** means defining infrastructure using configuration files or code instead of creating every resource manually.

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

### Infrastructure as Code

```text
CloudFormation Template
        |
        v
CloudFormation
        |
        v
AWS Resources
```

### Benefits

```text
Repeatable
Consistent
Automated
Version Controlled
Easier to Reuse
```

### Result

**Successfully understood the concept of Infrastructure as Code and how CloudFormation supports automated infrastructure deployment.**

---

## 3. CloudFormation Template

### Explanation

A **CloudFormation template** is a YAML or JSON document that describes the AWS resources and configuration that CloudFormation should create.

A basic template can contain sections such as:

```text
Parameters
Resources
Outputs
Mappings
Conditions
```

### Example

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

### Result

**Successfully understood that a CloudFormation template defines the infrastructure that CloudFormation should create.**

---

## 4. YAML

### Explanation

**YAML** is commonly used to write CloudFormation templates because it is easier to read and write than JSON for many infrastructure configurations.

### Example

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

### Result

**Successfully understood how YAML can be used to define CloudFormation resources.**

---

## 5. JSON

### Explanation

CloudFormation templates can also be written using JSON.

### Example

```json
{
  "Resources": {
    "MyBucket": {
      "Type": "AWS::S3::Bucket"
    }
  }
}
```

### Result

**Successfully understood that CloudFormation supports both YAML and JSON template formats.**

---

## 6. CloudFormation Stack

### Explanation

A **stack** is a collection of AWS resources that CloudFormation manages as a single unit.

For example, one stack can contain:

```text
VPC
Subnet
Route Table
Security Group
EC2 Instance
```

### Architecture

```text
CloudFormation Stack
        |
        +---- VPC
        |
        +---- Subnet
        |
        +---- Route Table
        |
        +---- Security Group
        |
        +---- EC2
```

### Result

**Successfully understood that a CloudFormation Stack groups and manages related AWS resources together.**

---

## 7. CloudFormation Resources

### Explanation

The **Resources** section is the main required section of a CloudFormation template.

It defines the AWS resources that CloudFormation should create.

### Example

```yaml
Resources:

  MyBucket:
    Type: AWS::S3::Bucket

  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
```

### Result

**Successfully understood how the Resources section defines AWS infrastructure components.**

---

## 8. CloudFormation Resource Type

### Explanation

The `Type` property specifies the AWS resource type.

Examples:

```text
AWS::S3::Bucket
AWS::EC2::Instance
AWS::EC2::VPC
AWS::EC2::Subnet
AWS::EC2::SecurityGroup
```

### Example

```yaml
MyBucket:
  Type: AWS::S3::Bucket
```

### Result

**Successfully understood how CloudFormation resource types identify the AWS resources to be created.**

---

## 9. CloudFormation Properties

### Explanation

**Properties** define the configuration of a resource.

### Example

```yaml
MyBucket:
  Type: AWS::S3::Bucket
  Properties:
    BucketEncryption:
      ServerSideEncryptionConfiguration:
        - ServerSideEncryptionByDefault:
            SSEAlgorithm: AES256
```

The exact properties depend on the resource type.

### Result

**Successfully understood how CloudFormation properties configure individual AWS resources.**

---

## 10. CloudFormation Parameters

### Explanation

**Parameters** allow values to be supplied when creating or updating a stack.

This makes templates reusable.

### Example

```yaml
Parameters:
  EnvironmentName:
    Type: String
    Default: Dev
```

The value can then be referenced by resources.

### Example

```yaml
!Ref EnvironmentName
```

### Result

**Successfully understood how Parameters make CloudFormation templates more reusable and configurable.**

---

## 11. CloudFormation Outputs

### Explanation

The **Outputs** section displays useful information after a stack is created.

Examples include:

```text
VPC ID
Subnet ID
Bucket Name
EC2 Instance ID
Load Balancer DNS Name
```

### Example

```yaml
Outputs:
  BucketName:
    Description: Name of the S3 bucket
    Value: !Ref MyBucket
```

### Result

**Successfully understood how CloudFormation Outputs can expose useful resource information after stack creation.**

---

## 12. CloudFormation Intrinsic Functions

### Explanation

CloudFormation provides intrinsic functions to reference and manipulate values inside templates.

Common functions include:

```text
Ref
Fn::GetAtt
Fn::Join
Fn::Sub
Fn::Select
Fn::Split
Fn::If
Fn::Equals
```

### Example

```yaml
BucketName:
  Value: !Ref MyBucket
```

### Result

**Successfully understood the purpose of CloudFormation intrinsic functions.**

---

## 13. Ref Function

### Explanation

The `Ref` function returns the value of a parameter or the appropriate reference value for a resource.

### Example

```yaml
Parameters:
  EnvironmentName:
    Type: String
    Default: Dev

Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Tags:
      - Key: Environment
        Value: !Ref EnvironmentName
```

### Result

**Successfully understood how `Ref` can reference parameters and resources inside a CloudFormation template.**

---

## 14. GetAtt Function

### Explanation

`Fn::GetAtt` retrieves an attribute from a resource.

### Example

```yaml
Outputs:
  BucketArn:
    Value: !GetAtt MyBucket.Arn
```

### Result

**Successfully understood how `Fn::GetAtt` can retrieve resource attributes such as an ARN.**

---

## 15. Sub Function

### Explanation

`Fn::Sub` can substitute variables into strings.

### Example

```yaml
Outputs:
  Message:
    Value: !Sub "Environment: ${EnvironmentName}"
```

### Result

**Successfully understood how `Fn::Sub` can construct strings using CloudFormation values.**

---

## 16. CloudFormation Dependencies

### Explanation

CloudFormation automatically determines many resource dependencies based on references between resources.

Explicit dependencies can also be specified using `DependsOn` when required.

### Example

```yaml
Resources:

  MyInstance:
    Type: AWS::EC2::Instance
    DependsOn: MySecurityGroup
```

### Result

**Successfully understood how CloudFormation manages resource creation order and dependencies.**

---

## 17. Creating a Simple S3 Bucket Using CloudFormation

### Explanation

In this practical lab, a simple S3 bucket is created using a CloudFormation template.

### Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - CloudFormation S3 Bucket

Resources:
  MyBucket:
    Type: AWS::S3::Bucket

Outputs:
  BucketName:
    Description: Name of the created S3 bucket
    Value: !Ref MyBucket
```

### Practical Steps

1. Open the AWS Management Console.
2. Search for **CloudFormation**.
3. Open the CloudFormation service.
4. Select **Create stack**.
5. Choose the template upload option.
6. Create the template file.

Example:

```text
lab19-s3.yaml
```

7. Paste the CloudFormation template into the file.
8. Upload the template.
9. Enter a stack name.

Example:

```text
Lab19-S3-Stack
```

10. Review the configuration.
11. Acknowledge any required capabilities or settings.
12. Create the stack.
13. Open the **Resources** section.
14. Verify that the S3 bucket was created.
15. Open **Outputs**.
16. Verify the bucket name.

### Result

**Successfully created an S3 bucket using an AWS CloudFormation template.**

---

## 18. CloudFormation Stack Creation

### Practical Steps

1. Open CloudFormation.
2. Click **Create stack**.
3. Select the appropriate template source.
4. Upload or specify the template.
5. Click **Next**.
6. Enter:

```text
Stack Name:
Lab19-CloudFormation
```

7. Configure Parameters when present.
8. Click **Next**.
9. Configure stack options when required.
10. Click **Next**.
11. Review the configuration.
12. Submit the stack creation.
13. Open the **Events** tab.
14. Monitor resource creation.
15. Open the **Resources** tab.
16. Verify created resources.
17. Open the **Outputs** tab.
18. Verify the output values.

### Result

**Successfully created and verified a CloudFormation stack.**

---

## 19. CloudFormation Stack Events

### Explanation

The **Events** section shows the progress and status of resources during stack operations.

Examples:

```text
CREATE_IN_PROGRESS
CREATE_COMPLETE
UPDATE_IN_PROGRESS
UPDATE_COMPLETE
DELETE_IN_PROGRESS
DELETE_COMPLETE
CREATE_FAILED
UPDATE_FAILED
```

### Example

```text
Stack Creation
      |
      v
CREATE_IN_PROGRESS
      |
      v
Resource Creation
      |
      v
CREATE_COMPLETE
```

### Result

**Successfully understood how CloudFormation Stack Events can be used to monitor stack operations.**

---

## 20. CloudFormation Stack Resources

### Explanation

The **Resources** section displays resources that are managed by the stack.

Example:

```text
CloudFormation Stack
       |
       +---- S3 Bucket
       +---- VPC
       +---- Subnet
       +---- Security Group
       +---- EC2 Instance
```

### Result

**Successfully understood how to view resources created and managed by a CloudFormation stack.**

---

## 21. CloudFormation Stack Outputs

### Explanation

The **Outputs** section displays values exposed by the template.

Example:

```yaml
Outputs:
  BucketName:
    Description: S3 Bucket Name
    Value: !Ref MyBucket
```

### Result

```text
BucketName:
<Generated Bucket Name>
```

### Result

**Successfully understood how stack outputs provide useful information about deployed resources.**

---

## 22. Updating a CloudFormation Stack

### Explanation

CloudFormation allows a stack to be updated by changing the template or parameter values.

### Practical Steps

1. Open CloudFormation.
2. Select the existing stack.
3. Select **Update**.
4. Choose the updated template.
5. Upload the new template.
6. Review the changes.
7. Submit the update.
8. Open **Events**.
9. Monitor the update.
10. Verify the resources.
11. Verify the Outputs.

### Example

```text
Original Template
      |
      v
Modify Template
      |
      v
Update Stack
      |
      v
CloudFormation
      |
      v
Updated Resources
```

### Result

**Successfully understood the process of updating resources managed by a CloudFormation stack.**

---

## 23. CloudFormation Change Sets

### Explanation

A **Change Set** allows you to preview how a proposed stack update may affect resources before executing the update.

### Practical Steps

1. Open CloudFormation.
2. Select the stack.
3. Create a Change Set.
4. Select the updated template.
5. Enter a Change Set name.
6. Review the proposed changes.
7. Check which resources will be:

```text
Added
Modified
Removed
```

8. Execute the Change Set when the changes are acceptable.

### Result

**Successfully understood how Change Sets can be used to review proposed CloudFormation stack changes before execution.**

---

## 24. CloudFormation Rollback

### Explanation

If a stack operation fails, CloudFormation can roll back resources depending on the operation and configured behavior.

### Example

```text
Stack Update
     |
     v
Resource Error
     |
     v
UPDATE_FAILED
     |
     v
Rollback
     |
     v
Previous State
```

### Result

**Successfully understood the purpose of CloudFormation rollback behavior when stack operations fail.**

---

## 25. CloudFormation Drift Detection

### Explanation

**Drift detection** helps identify differences between the configuration defined in a CloudFormation template and the current configuration of supported stack resources.

### Example

```text
CloudFormation Template
          |
          v
Expected Configuration
          |
          v
Compare
          |
          v
Actual AWS Resource
          |
          v
Drift Detected / No Drift
```

### Practical Steps

1. Open CloudFormation.
2. Select a stack.
3. Choose the drift detection option.
4. Start drift detection.
5. Wait for the operation to complete.
6. Review the drift status.
7. Open the affected resources if drift is detected.

### Result

**Successfully understood how CloudFormation drift detection can identify configuration differences between managed resources and their expected template configuration.**

---

## 26. CloudFormation with VPC

### Explanation

CloudFormation can create complete networking infrastructure using a template.

Example:

```text
CloudFormation
      |
      v
VPC
 |
 +---- Public Subnet
 |
 +---- Private Subnet
 |
 +---- Route Table
 |
 +---- Internet Gateway
 |
 +---- Security Group
```

### Result

**Successfully understood how CloudFormation can provision VPC networking infrastructure.**

---

## 27. CloudFormation VPC Template

### Example

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - Simple VPC

Resources:

  LabVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: Lab19-VPC

Outputs:

  VPCId:
    Description: VPC ID
    Value: !Ref LabVPC
```

### Result

**Successfully created a CloudFormation template that defines a VPC and outputs its VPC ID.**

---

## 28. CloudFormation with EC2

### Explanation

CloudFormation can create EC2 instances and their supporting resources.

### Architecture

```text
CloudFormation
      |
      +---- VPC
      |
      +---- Subnet
      |
      +---- Security Group
      |
      +---- EC2 Instance
```

### Result

**Successfully understood how CloudFormation can automate EC2 infrastructure deployment.**

---

## 29. CloudFormation EC2 Template Example

### Example

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - EC2 Example

Parameters:

  InstanceType:
    Type: String
    Default: t3.micro

  LatestAmiId:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64

Resources:

  LabSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group for Lab EC2 instance
      VpcId: !Ref LabVPC

  LabVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true

  LabSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref LabVPC
      CidrBlock: 10.0.1.0/24

  LabInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref LatestAmiId
      InstanceType: !Ref InstanceType
      SubnetId: !Ref LabSubnet
      SecurityGroupIds:
        - !Ref LabSecurityGroup

Outputs:

  InstanceId:
    Description: EC2 Instance ID
    Value: !Ref LabInstance

  VPCId:
    Description: VPC ID
    Value: !Ref LabVPC
```

### Result

**Successfully understood how a CloudFormation template can define an EC2 instance together with a VPC, subnet, and security group.**

---

## 30. CloudFormation IAM Permissions

### Explanation

CloudFormation requires appropriate permissions to create and manage resources.

The identity creating or updating a stack must have the required permissions, or CloudFormation can use a configured service role when appropriate.

### Example

```text
User / Role
     |
     v
CloudFormation
     |
     v
IAM Permissions
     |
     v
AWS Resources
```

### Result

**Successfully understood how IAM permissions control CloudFormation operations.**

---

## 31. CloudFormation Service Role

### Explanation

A **CloudFormation service role** is an IAM role that CloudFormation can assume to make calls to AWS services on behalf of the stack operation.

The role should follow least-privilege principles.

### Architecture

```text
User
 |
 v
CloudFormation
 |
 v
Service Role
 |
 v
AWS Services
```

### Result

**Successfully understood the purpose of a CloudFormation service role and its relationship with IAM permissions.**

---

## 32. CloudFormation Parameters Practical Lab

### Explanation

In this lab, a parameter is used to make a CloudFormation template configurable.

### Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - Parameters

Parameters:

  EnvironmentName:
    Type: String
    Default: Dev
    AllowedValues:
      - Dev
      - Test
      - Prod

Resources:

  LabBucket:
    Type: AWS::S3::Bucket
    Properties:
      Tags:
        - Key: Environment
          Value: !Ref EnvironmentName

Outputs:

  Environment:
    Description: Selected environment
    Value: !Ref EnvironmentName
```

### Practical Steps

1. Create the template.
2. Open CloudFormation.
3. Create a new stack.
4. Upload the template.
5. Enter a stack name.
6. Select:

```text
EnvironmentName:
Dev
```

7. Create the stack.
8. Open Resources.
9. Verify the S3 bucket.
10. Open Outputs.
11. Verify the selected environment.

### Result

**Successfully created a parameterized CloudFormation stack and supplied a parameter value during stack creation.**

---

## 33. CloudFormation Outputs Practical Lab

### Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Resources:

  LabBucket:
    Type: AWS::S3::Bucket

Outputs:

  BucketName:
    Description: Created S3 bucket name
    Value: !Ref LabBucket

  BucketArn:
    Description: Created S3 bucket ARN
    Value: !GetAtt LabBucket.Arn
```

### Practical Steps

1. Create the template.
2. Create a CloudFormation stack.
3. Upload the template.
4. Create the stack.
5. Open the **Outputs** section.
6. Verify:

```text
BucketName
BucketArn
```

### Result

**Successfully used CloudFormation Outputs and `GetAtt` to display resource information.**

---

## 34. CloudFormation with S3 and Parameters

### Complete Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - Parameterized S3 Bucket

Parameters:

  EnvironmentName:
    Type: String
    Default: Dev
    AllowedValues:
      - Dev
      - Test
      - Prod

Resources:

  LabBucket:
    Type: AWS::S3::Bucket
    Properties:
      Tags:
        - Key: Environment
          Value: !Ref EnvironmentName
        - Key: Project
          Value: AWS-CloudFormation-Lab

Outputs:

  BucketName:
    Description: Name of the S3 bucket
    Value: !Ref LabBucket

  BucketArn:
    Description: ARN of the S3 bucket
    Value: !GetAtt LabBucket.Arn

  Environment:
    Description: Selected environment
    Value: !Ref EnvironmentName
```

### Result

**Successfully created a reusable CloudFormation S3 template using Parameters, Resources, Tags, and Outputs.**

---

## 35. CloudFormation CLI

### Explanation

CloudFormation can also be managed from the AWS CLI.

### List Stacks

```bash
aws cloudformation list-stacks
```

### Describe Stack

```bash
aws cloudformation describe-stacks \
    --stack-name Lab19-CloudFormation
```

### Describe Stack Resources

```bash
aws cloudformation list-stack-resources \
    --stack-name Lab19-CloudFormation
```

### Describe Stack Events

```bash
aws cloudformation describe-stack-events \
    --stack-name Lab19-CloudFormation
```

### Result

**Successfully understood how AWS CLI can be used to inspect CloudFormation stacks, resources, and events.**

---

## 36. CloudFormation CLI - Create Stack

### Explanation

A CloudFormation stack can be created using the AWS CLI.

### Command

```bash
aws cloudformation create-stack \
    --stack-name Lab19-CLI-Stack \
    --template-body file://lab19-s3.yaml \
    --region ap-south-1
```

### Result

**Successfully understood how AWS CLI can initiate CloudFormation stack creation from a template file.**

---

## 37. CloudFormation CLI - Update Stack

### Command

```bash
aws cloudformation update-stack \
    --stack-name Lab19-CLI-Stack \
    --template-body file://lab19-s3.yaml \
    --region ap-south-1
```

### Result

**Successfully understood how AWS CLI can initiate a CloudFormation stack update.**

---

## 38. CloudFormation CLI - Delete Stack

### Explanation

A stack and its managed resources can be deleted using the AWS CLI when the resources and deletion behavior allow it.

### Command

```bash
aws cloudformation delete-stack \
    --stack-name Lab19-CLI-Stack \
    --region ap-south-1
```

### Result

**Successfully understood how AWS CLI can delete a CloudFormation stack.**

---

## 39. CloudFormation Practical Lab - Complete S3 Deployment

### Explanation

This practical lab demonstrates a complete CloudFormation deployment using a YAML template.

### Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - Complete CloudFormation S3 Deployment

Parameters:

  EnvironmentName:
    Type: String
    Default: Dev
    AllowedValues:
      - Dev
      - Test
      - Prod

Resources:

  LabBucket:
    Type: AWS::S3::Bucket
    Properties:
      Tags:
        - Key: Name
          Value: Lab19-Bucket
        - Key: Environment
          Value: !Ref EnvironmentName
        - Key: ManagedBy
          Value: CloudFormation

Outputs:

  BucketName:
    Description: Name of the CloudFormation S3 bucket
    Value: !Ref LabBucket

  BucketArn:
    Description: ARN of the CloudFormation S3 bucket
    Value: !GetAtt LabBucket.Arn

  Environment:
    Description: Environment selected for the stack
    Value: !Ref EnvironmentName
```

### Practical Steps

### Step 1 - Create Template

Create:

```text
lab19-s3.yaml
```

### Step 2 - Open CloudFormation

```text
AWS Console
      |
      v
CloudFormation
```

### Step 3 - Create Stack

Select:

```text
Create stack
```

### Step 4 - Upload Template

Upload:

```text
lab19-s3.yaml
```

### Step 5 - Enter Stack Name

```text
Lab19-S3-Stack
```

### Step 6 - Select Parameter

```text
EnvironmentName:
Dev
```

### Step 7 - Create Stack

Submit the stack.

### Step 8 - Monitor Events

Open:

```text
Events
```

Verify:

```text
CREATE_IN_PROGRESS
CREATE_COMPLETE
```

### Step 9 - Verify Resources

Open:

```text
Resources
```

Verify:

```text
LabBucket
```

### Step 10 - Verify Outputs

Open:

```text
Outputs
```

Verify:

```text
BucketName
BucketArn
Environment
```

### Result

**Successfully deployed an S3 resource using CloudFormation and verified the stack events, resources, and outputs.**

---

## 40. CloudFormation Practical Lab - Update

### Explanation

The existing stack can be updated by modifying the template.

### Practical Steps

1. Open the existing CloudFormation stack.
2. Modify the template.
3. Add or change a resource property.
4. Save the updated template.
5. Open CloudFormation.
6. Select the stack.
7. Select **Update**.
8. Upload the updated template.
9. Review the changes.
10. Create a Change Set when appropriate.
11. Execute the update.
12. Monitor Stack Events.
13. Verify the updated resource.

### Example

```text
Original Template
       |
       v
Modify
       |
       v
Change Set
       |
       v
Review
       |
       v
Execute
       |
       v
Updated Stack
```

### Result

**Successfully understood the practical CloudFormation stack update workflow.**

---

## 41. CloudFormation Practical Lab - Drift Detection

### Explanation

This lab demonstrates the purpose of detecting manual changes made outside CloudFormation.

### Practical Steps

1. Create a CloudFormation stack.
2. Verify the resource.
3. Manually modify a supported resource property outside CloudFormation when appropriate.
4. Return to CloudFormation.
5. Select the stack.
6. Start drift detection.
7. Wait for the drift detection operation to complete.
8. Review the drift status.
9. Identify the affected resource.
10. Compare the expected and actual configuration.

### Example

```text
CloudFormation Template
        |
        v
Expected Configuration
        |
        v
Compare
        |
        v
Actual Resource
        |
        v
DRIFTED
```

### Result

**Successfully understood how CloudFormation drift detection can identify configuration changes made outside CloudFormation.**

---

## 42. CloudFormation Stack Lifecycle

### Explanation

A CloudFormation stack goes through different lifecycle operations.

### Workflow

```text
Create
  |
  v
CREATE_IN_PROGRESS
  |
  v
CREATE_COMPLETE
  |
  v
Update
  |
  v
UPDATE_IN_PROGRESS
  |
  v
UPDATE_COMPLETE
  |
  v
Delete
  |
  v
DELETE_IN_PROGRESS
  |
  v
DELETE_COMPLETE
```

### Result

**Successfully understood the basic CloudFormation stack lifecycle.**

---

## 43. CloudFormation Troubleshooting

### Explanation

If CloudFormation fails to create or update a resource, check:

```text
Template Syntax
Resource Properties
IAM Permissions
Resource Dependencies
AWS Region
Resource Limits
Service Availability
Parameter Values
Stack Events
```

### Troubleshooting Flow

```text
CloudFormation Failure
        |
        v
Check Stack Events
        |
        v
Identify Failed Resource
        |
        v
Read Failure Reason
        |
        v
Check Template
        |
        v
Check IAM Permissions
        |
        v
Check Parameters
        |
        v
Check Dependencies
        |
        v
Correct Problem
        |
        v
Update / Retry
```

### Result

**Successfully understood how Stack Events can be used to troubleshoot CloudFormation deployment failures.**

---

## 44. CloudFormation Template Validation

### Explanation

Templates should be validated before deployment to identify syntax or template-structure problems.

### AWS CLI Command

```bash
aws cloudformation validate-template \
    --template-body file://lab19-s3.yaml
```

### Example

```text
Template
   |
   v
Validate
   |
   +---- Valid
   |
   +---- Error
```

### Result

**Successfully understood how to validate a CloudFormation template before deployment.**

---

## 45. CloudFormation Security

### Explanation

CloudFormation deployments should follow AWS security best practices.

Important practices include:

```text
Use least-privilege IAM permissions
Protect CloudFormation templates
Do not hard-code credentials
Do not place secret values directly in templates
Use secure parameter handling for sensitive values
Restrict stack access
Review IAM roles
Protect S3 template locations
Monitor CloudFormation activity with CloudTrail
```

### Example

```text
CloudFormation
      |
      v
IAM
      |
      v
Least Privilege
      |
      v
AWS Resources
```

### Result

**Successfully understood important security practices for CloudFormation deployments.**

---

## 46. CloudFormation and CloudTrail

### Explanation

CloudTrail can record CloudFormation API activity.

Examples include:

```text
CreateStack
UpdateStack
DeleteStack
ExecuteChangeSet
```

### Architecture

```text
CloudFormation
      |
      v
API Activity
      |
      v
CloudTrail
      |
      v
Audit / Investigation
```

### Result

**Successfully understood how CloudTrail can provide an audit trail for CloudFormation API activity.**

---

## 47. CloudFormation and CloudWatch

### Explanation

CloudWatch can be used to monitor supported AWS resources created by CloudFormation.

CloudFormation itself also exposes stack events and status information for deployment monitoring.

### Example

```text
CloudFormation
      |
      v
AWS Resources
      |
      v
CloudWatch
      |
      +---- Metrics
      +---- Logs
      +---- Alarms
```

### Result

**Successfully understood how CloudWatch and CloudFormation can work together for infrastructure deployment and resource monitoring.**

---

## 48. CloudFormation Complete Architecture

```text
                         Infrastructure as Code
                                  |
                                  v
                         CloudFormation Template
                                  |
                         +--------+--------+
                         |                 |
                         v                 v
                       YAML              JSON
                         |                 |
                         +--------+--------+
                                  |
                                  v
                         CloudFormation Stack
                                  |
             +--------------------+--------------------+
             |                    |                    |
             v                    v                    v
            VPC                  S3                   EC2
             |                    |                    |
             +--------------------+--------------------+
                                  |
                                  v
                           Stack Management
                                  |
              +------------------+------------------+
              |                  |                  |
              v                  v                  v
           Events            Resources           Outputs
              |
              v
          Monitoring
              |
              v
        CloudTrail / CloudWatch
```

---

## 49. CloudFormation Deployment Workflow

### Workflow

```text
Write Template
      |
      v
Validate Template
      |
      v
Create Stack
      |
      v
CloudFormation
      |
      v
Create Resources
      |
      v
Monitor Stack Events
      |
      v
CREATE_COMPLETE
      |
      v
Review Resources
      |
      v
Review Outputs
      |
      v
Create Change Set
      |
      v
Update Stack
      |
      v
Detect Drift
      |
      v
Delete Stack
```

### Result

**Successfully understood the complete CloudFormation infrastructure deployment workflow.**

---

## 50. CloudFormation Best Practices

### Explanation

Important CloudFormation best practices include:

```text
1. Store templates in version control.

2. Use reusable templates.

3. Use Parameters for environment-specific values.

4. Use Outputs for important resource information.

5. Use Change Sets before important updates.

6. Validate templates before deployment.

7. Follow least-privilege IAM permissions.

8. Avoid hard-coded credentials.

9. Protect sensitive configuration values.

10. Use meaningful resource names and descriptions.

11. Monitor Stack Events.

12. Use drift detection when appropriate.

13. Test templates in a development environment.

14. Remove unused test stacks and resources.

15. Keep templates organized and documented.
```

### Result

**Successfully understood important best practices for designing, deploying, updating, and securing CloudFormation infrastructure.**

---

## 51. Complete CloudFormation Practical Lab

### Explanation

This lab demonstrates the complete Infrastructure as Code workflow using AWS CloudFormation.

### Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Lab 19 - Complete CloudFormation Infrastructure

Parameters:

  EnvironmentName:
    Type: String
    Default: Dev
    AllowedValues:
      - Dev
      - Test
      - Prod

Resources:

  LabVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: !Sub "${EnvironmentName}-Lab-VPC"

  LabSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref LabVPC
      CidrBlock: 10.0.1.0/24
      Tags:
        - Key: Name
          Value: !Sub "${EnvironmentName}-Lab-Subnet"

  LabSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group for CloudFormation lab
      VpcId: !Ref LabVPC
      Tags:
        - Key: Name
          Value: !Sub "${EnvironmentName}-Lab-SG"

  LabBucket:
    Type: AWS::S3::Bucket
    Properties:
      Tags:
        - Key: Environment
          Value: !Ref EnvironmentName
        - Key: ManagedBy
          Value: CloudFormation

Outputs:

  VPCId:
    Description: CloudFormation Lab VPC ID
    Value: !Ref LabVPC

  SubnetId:
    Description: CloudFormation Lab Subnet ID
    Value: !Ref LabSubnet

  SecurityGroupId:
    Description: CloudFormation Lab Security Group ID
    Value: !Ref LabSecurityGroup

  BucketName:
    Description: CloudFormation Lab S3 Bucket Name
    Value: !Ref LabBucket

  BucketArn:
    Description: CloudFormation Lab S3 Bucket ARN
    Value: !GetAtt LabBucket.Arn
```

### Practical Steps

### Step 1 - Create Template

Create:

```text
lab19-cloudformation.yaml
```

### Step 2 - Validate Template

```bash
aws cloudformation validate-template \
    --template-body file://lab19-cloudformation.yaml
```

### Step 3 - Open CloudFormation

```text
AWS Console
      |
      v
CloudFormation
```

### Step 4 - Create Stack

Select:

```text
Create stack
```

Upload:

```text
lab19-cloudformation.yaml
```

### Step 5 - Enter Stack Name

```text
Lab19-Infrastructure
```

### Step 6 - Configure Parameter

```text
EnvironmentName:
Dev
```

### Step 7 - Review

Review:

```text
VPC
Subnet
Security Group
S3 Bucket
```

### Step 8 - Create Stack

Create the stack.

### Step 9 - Monitor Events

Open:

```text
Events
```

Check resource creation status.

### Step 10 - Check Resources

Open:

```text
Resources
```

Verify:

```text
LabVPC
LabSubnet
LabSecurityGroup
LabBucket
```

### Step 11 - Check Outputs

Open:

```text
Outputs
```

Verify:

```text
VPCId
SubnetId
SecurityGroupId
BucketName
BucketArn
```

### Step 12 - Create Change Set

Create a Change Set for a controlled template update.

### Step 13 - Review Changes

Check:

```text
Add
Modify
Remove
```

### Step 14 - Execute Update

Execute the Change Set when appropriate.

### Step 15 - Detect Drift

Run drift detection and review the result.

### Step 16 - Review CloudTrail

Use CloudTrail to inspect CloudFormation API activity when required.

### Step 17 - Delete Test Stack

After completing the lab:

```bash
aws cloudformation delete-stack \
    --stack-name Lab19-Infrastructure \
    --region ap-south-1
```

### Result

**Successfully completed a complete CloudFormation Infrastructure as Code workflow by creating a VPC, subnet, security group, and S3 bucket from a YAML template, validating the template, creating the stack, monitoring events, reviewing resources and outputs, understanding Change Sets and drift detection, and deleting the test stack using AWS CLI.**

---

## 52. Final CloudFormation Workflow

```text
                    CloudFormation
                          |
                          v
                  Infrastructure as Code
                          |
                          v
                  YAML / JSON Template
                          |
          +---------------+---------------+
          |               |               |
          v               v               v
      Parameters       Resources        Outputs
                          |
                          v
                  CloudFormation Stack
                          |
          +---------------+---------------+
          |               |               |
          v               v               v
         VPC             EC2              S3
          |               |               |
          +---------------+---------------+
                          |
                          v
                    Stack Events
                          |
             +------------+------------+
             |                         |
             v                         v
        CREATE_COMPLETE          UPDATE_COMPLETE
             |                         |
             +------------+------------+
                          |
                          v
                    Change Sets
                          |
                          v
                  Drift Detection
                          |
                          v
                     Monitoring
                          |
                          v
                  CloudTrail / IAM
                          |
                          v
                   Secure IaC
```

### Final Result

**Successfully completed Lab 19 - AWS CloudFormation and understood Infrastructure as Code, CloudFormation templates, YAML and JSON, stacks, resources, properties, parameters, outputs, intrinsic functions, dependencies, Change Sets, stack updates, rollback, drift detection, CloudFormation CLI, IAM permissions, VPC deployment, EC2 deployment, S3 deployment, CloudTrail integration, CloudWatch monitoring, troubleshooting, security, and CloudFormation best practices.**
