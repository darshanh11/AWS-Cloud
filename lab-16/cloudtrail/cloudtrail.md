# Lab 16 - AWS CloudTrail

## Objective

The objective of this lab is to understand **AWS CloudTrail** and practically learn how to record, view, search, and monitor activity and API actions performed in an AWS account.

This lab covers:

- AWS CloudTrail
- CloudTrail Events
- Management Events
- Data Events
- Event History
- Trails
- S3 Bucket
- CloudWatch Logs
- Event Selectors
- Read Events
- Write Events
- User Identity
- Event Source
- Event Name
- Source IP Address
- Event Time
- AWS Console Activity
- AWS CLI Activity
- IAM Activity
- EC2 Activity
- Security Monitoring
- Auditing
- Compliance
- Practical CloudTrail Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is AWS CloudTrail?

### Explanation

**AWS CloudTrail** is an AWS service that records actions and API activity performed in an AWS account.

CloudTrail helps answer questions such as:

```text
Who performed the action?
What action was performed?
When was it performed?
Where did it come from?
Which AWS resource was affected?
```

### Example

```text
AWS Account
     |
     +---- IAM Activity
     |
     +---- EC2 Activity
     |
     +---- S3 Activity
     |
     +---- VPC Activity
     |
     v
AWS CloudTrail
     |
     v
Event Records
```

### Result

**Successfully understood that AWS CloudTrail records AWS account activity and API actions for auditing and security investigation.**

---

## 2. Why is CloudTrail Used?

### Explanation

CloudTrail is commonly used for:

- Auditing
- Security monitoring
- Troubleshooting
- Compliance
- Investigating account activity
- Tracking changes to AWS resources
- Identifying who performed an action

### Example

```text
AWS Resource
     |
     v
API Activity
     |
     v
CloudTrail
     |
     v
Event Record
     |
     v
Security Investigation
```

### Result

**Successfully understood why CloudTrail is important for auditing, monitoring, and investigating AWS activity.**

---

## 3. CloudTrail Event

### Explanation

A **CloudTrail event** is a record of an activity or API action that occurred in an AWS account.

An event can contain information such as:

```text
Event Time
User Identity
Event Name
Event Source
AWS Region
Source IP Address
Resource Information
```

### Example

```text
Event:
CreateBucket

Event Source:
s3.amazonaws.com

Region:
ap-south-1

Source IP:
Example IP

User Identity:
IAM User / Role
```

### Result

**Successfully understood that CloudTrail events contain information about AWS API activity.**

---

## 4. CloudTrail Event History

### Explanation

The **CloudTrail Event History** provides a searchable record of recent management events in an AWS account.

It can be used to investigate actions performed through:

```text
AWS Management Console
AWS CLI
AWS SDKs
AWS APIs
```

### Practical Steps

1. Sign in to the AWS Management Console.
2. Search for **CloudTrail**.
3. Open the CloudTrail service.
4. Select **Event history**.
5. Review the available events.
6. Select an event.
7. Open the event details.
8. Review the event information.

### Result

**Successfully viewed CloudTrail Event History and examined recorded AWS activity.**

---

## 5. Management Events

### Explanation

**Management events** provide information about management operations performed on AWS resources.

Examples include:

```text
Create
Delete
Modify
Update
Describe
```

Examples of AWS actions include:

```text
CreateUser
RunInstances
CreateBucket
CreateSecurityGroup
DeleteSecurityGroup
```

### Example

```text
AWS Management Action
        |
        v
CloudTrail
        |
        v
Management Event
```

### Result

**Successfully understood how CloudTrail records management activity involving AWS resources.**

---

## 6. Read Events and Write Events

### Explanation

Management events can be categorized into read and write operations.

### Read Event

A read event generally retrieves information without changing a resource.

Example:

```text
DescribeInstances
GetUser
ListBuckets
```

### Write Event

A write event generally creates, modifies, or deletes a resource.

Example:

```text
RunInstances
CreateUser
DeleteBucket
```

### Example

```text
CloudTrail
    |
    +---- Read Events
    |       |
    |       +---- Describe
    |       +---- Get
    |       +---- List
    |
    +---- Write Events
            |
            +---- Create
            +---- Update
            +---- Delete
```

### Result

**Successfully understood the difference between read and write CloudTrail events.**

---

## 7. Data Events

### Explanation

**Data events** provide visibility into resource-level data operations for supported AWS resources.

Examples can include object-level operations in Amazon S3.

Data events can generate a large number of events, so they should be enabled according to monitoring requirements.

### Example

```text
S3 Bucket
    |
    +---- Object Access
    |
    +---- Object Operations
    |
    v
CloudTrail Data Events
```

### Result

**Successfully understood that CloudTrail Data Events provide detailed visibility into supported resource-level operations.**

---

## 8. CloudTrail Trail

### Explanation

A **Trail** is a CloudTrail configuration that delivers events to a destination such as an Amazon S3 bucket.

A trail can be configured to record selected event types and deliver the event logs for longer-term storage and analysis.

### Example

```text
AWS Account
     |
     v
CloudTrail Trail
     |
     v
S3 Bucket
     |
     v
CloudTrail Logs
```

### Result

**Successfully understood that a CloudTrail Trail can deliver recorded events to an S3 bucket for storage and analysis.**

---

## 9. CloudTrail and S3

### Explanation

CloudTrail can deliver trail logs to an **Amazon S3 bucket**.

S3 provides durable storage for CloudTrail log files.

### Example

```text
AWS Activity
     |
     v
CloudTrail
     |
     v
Trail
     |
     v
Amazon S3
     |
     v
CloudTrail Log Files
```

### Result

**Successfully understood how CloudTrail can deliver trail logs to Amazon S3 for storage.**

---

## 10. Creating an S3 Bucket for CloudTrail

### Explanation

An S3 bucket can be used as the destination for CloudTrail logs.

### Practical Steps

1. Open the **Amazon S3** service.
2. Select **Create bucket**.
3. Enter a globally unique bucket name.

Example:

```text
aws-lab-cloudtrail-logs-unique
```

4. Select the required AWS Region.
5. Keep the bucket private.
6. Keep appropriate security settings enabled.
7. Create the bucket.
8. Verify that the bucket was created.

### Result

**Successfully created a private S3 bucket to store CloudTrail logs.**

---

## 11. Creating a CloudTrail Trail

### Explanation

A CloudTrail Trail can be configured to deliver events to an S3 bucket.

### Practical Steps

1. Open **CloudTrail**.
2. Select **Trails**.
3. Click **Create trail**.
4. Enter the trail name.

Example:

```text
AWS-Lab-Trail
```

5. Configure the management events.
6. Select the required read and write events.
7. Select the S3 destination.
8. Select the previously created S3 bucket.
9. Configure additional event types when required.
10. Review the configuration.
11. Create the trail.
12. Verify that the trail is enabled.

### Result

**Successfully created a CloudTrail Trail and configured an S3 bucket as the log destination.**

---

## 12. CloudTrail Event Selectors

### Explanation

Event selectors determine which types of events a trail records.

A trail can be configured for:

```text
Management Events
Data Events
Network Activity Events
```

The exact available options depend on the CloudTrail configuration and AWS service.

### Example

```text
CloudTrail Trail
       |
       +---- Management Events
       |
       +---- Data Events
       |
       +---- Network Activity Events
```

### Result

**Successfully understood how event selectors control the types of activity recorded by a CloudTrail Trail.**

---

## 13. CloudTrail User Identity

### Explanation

CloudTrail records information about the identity associated with an API action.

The identity can be associated with:

```text
IAM User
IAM Role
AWS Account
AWS Service
Root User
```

depending on the event.

### Example

```text
User
 |
 v
AWS API
 |
 v
CloudTrail
 |
 v
User Identity
```

### Result

**Successfully understood how CloudTrail records identity information associated with AWS activity.**

---

## 14. Event Name

### Explanation

The **Event Name** identifies the API operation that was performed.

Examples:

```text
RunInstances
CreateUser
CreateBucket
DeleteBucket
StopInstances
StartInstances
```

### Example

```text
Event Name:
RunInstances

Meaning:
An EC2 instance launch API operation was performed.
```

### Result

**Successfully understood how the Event Name identifies the AWS API operation recorded by CloudTrail.**

---

## 15. Event Source

### Explanation

The **Event Source** identifies the AWS service that generated the API event.

Examples:

```text
ec2.amazonaws.com
s3.amazonaws.com
iam.amazonaws.com
cloudtrail.amazonaws.com
```

### Example

```text
Event Name:
RunInstances

Event Source:
ec2.amazonaws.com
```

### Result

**Successfully understood how Event Source identifies the AWS service associated with a CloudTrail event.**

---

## 16. Source IP Address

### Explanation

CloudTrail events can contain the **source IP address** associated with the request when available.

This information can be useful during security investigations.

### Example

```text
User
  |
  | Request
  | Source IP
  v
AWS API
  |
  v
CloudTrail
```

### Result

**Successfully understood how source IP information can help identify where an AWS API request originated.**

---

## 17. AWS Region

### Explanation

CloudTrail events contain information about the AWS Region associated with the event.

Example:

```text
Region:
ap-south-1
```

This helps identify where an AWS resource or API operation was associated with the activity.

### Result

**Successfully understood how the AWS Region information helps identify the regional context of CloudTrail events.**

---

## 18. CloudTrail Event Details

### Explanation

Opening an individual CloudTrail event provides detailed information about the API activity.

Example:

```text
Event Time:
2026-09-01 15:00:00

Event Source:
ec2.amazonaws.com

Event Name:
RunInstances

AWS Region:
ap-south-1

Source IP Address:
Example IP

User Identity:
IAM Role
```

### Practical Steps

1. Open **CloudTrail**.
2. Select **Event history**.
3. Select an event.
4. Open the event details.
5. Review the event source.
6. Review the event name.
7. Review the user identity.
8. Review the event time.
9. Review the source IP address.
10. Review the AWS Region.
11. Review the resource information.

### Result

**Successfully examined the detailed information contained in a CloudTrail event.**

---

## 19. CloudTrail and IAM

### Explanation

CloudTrail can record IAM API activity.

Examples include:

```text
CreateUser
DeleteUser
CreateRole
AttachRolePolicy
CreateAccessKey
DeleteAccessKey
```

### Example

```text
IAM Activity
     |
     v
CloudTrail
     |
     v
Event History
```

### Result

**Successfully understood how CloudTrail can be used to audit IAM-related API activity.**

---

## 20. CloudTrail and EC2

### Explanation

CloudTrail can record EC2 management actions.

Examples include:

```text
RunInstances
StartInstances
StopInstances
TerminateInstances
CreateSecurityGroup
AuthorizeSecurityGroupIngress
```

### Example

```text
EC2 Action
    |
    v
CloudTrail
    |
    v
Event
```

### Result

**Successfully understood how CloudTrail can be used to track EC2 management activity.**

---

## 21. CloudTrail and S3

### Explanation

CloudTrail can record management activity related to S3.

For supported S3 data operations, Data Events can provide more detailed object-level visibility when configured.

### Example

```text
S3
 |
 +---- Create Bucket
 |
 +---- Delete Bucket
 |
 +---- Object Operations
 |
 v
CloudTrail
```

### Result

**Successfully understood how CloudTrail can provide visibility into S3 activity through management and, when configured, data events.**

---

## 22. CloudTrail and CloudWatch Logs

### Explanation

CloudTrail events can also be delivered to **CloudWatch Logs** for monitoring and analysis.

### Architecture

```text
AWS Activity
     |
     v
CloudTrail
     |
     +------------+
     |            |
     v            v
     S3       CloudWatch Logs
                  |
                  v
              Monitoring
```

### Result

**Successfully understood how CloudTrail can integrate with CloudWatch Logs for monitoring and analysis.**

---

## 23. Creating CloudTrail CloudWatch Logs Integration

### Practical Steps

1. Open **CloudTrail**.
2. Select **Trails**.
3. Select the required trail.
4. Edit the trail configuration.
5. Locate the CloudWatch Logs configuration.
6. Specify the required Log Group.
7. Configure the required IAM role according to AWS requirements.
8. Save the trail configuration.
9. Perform a test AWS activity.
10. Open **CloudWatch**.
11. Open **Log Groups**.
12. Select the configured Log Group.
13. Review the CloudTrail events.

### Result

**Successfully understood the practical workflow for delivering CloudTrail events to CloudWatch Logs.**

---

## 24. CloudTrail Practical Lab - Record EC2 Activity

### Explanation

In this practical lab, CloudTrail is used to record an EC2 API action.

### Practical Steps

### Step 1 - Open CloudTrail

Open:

```text
AWS Console
   |
   v
CloudTrail
```

### Step 2 - Open Event History

Select:

```text
Event history
```

### Step 3 - Perform EC2 Action

Open:

```text
EC2
```

Perform a test action such as:

```text
Start Instance
```

or:

```text
Stop Instance
```

### Step 4 - Return to CloudTrail

Open:

```text
CloudTrail
   |
   v
Event history
```

### Step 5 - Search the Event

Search for the relevant EC2 event.

Example:

```text
Event Name:
StartInstances
```

### Step 6 - Open Event

Select the event and inspect:

```text
Event Time
Event Name
Event Source
User Identity
Source IP Address
AWS Region
```

### Result

**Successfully performed an EC2 action and used CloudTrail Event History to identify and inspect the corresponding API event.**

---

## 25. Practical Lab - Record IAM Activity

### Explanation

CloudTrail can be used to audit IAM API actions.

### Practical Steps

1. Open **IAM**.
2. Perform an appropriate test activity.
3. Example:

```text
Create IAM User
```

4. Open **CloudTrail**.
5. Select **Event history**.
6. Search for the IAM event.
7. Open the event details.
8. Review:

```text
Event Name
Event Source
User Identity
Event Time
Source IP Address
```

### Example

```text
IAM
 |
 v
CreateUser
 |
 v
CloudTrail
 |
 v
Event History
```

### Result

**Successfully understood how CloudTrail can be used to identify and audit IAM API activity.**

---

## 26. Practical Lab - Record S3 Activity

### Explanation

In this practical lab, CloudTrail is used to observe S3-related activity.

### Practical Steps

1. Open **S3**.
2. Perform an appropriate test action.
3. Example:

```text
Create Bucket
```

4. Open **CloudTrail**.
5. Select **Event history**.
6. Search for the S3 event.
7. Open the event.
8. Review:

```text
Event Source:
s3.amazonaws.com

Event Name:
CreateBucket
```

9. Review the identity and request details.

### Result

**Successfully used CloudTrail Event History to identify an S3 management event.**

---

## 27. CloudTrail Security Investigation

### Explanation

CloudTrail can help investigate suspicious or unexpected AWS activity.

Important information to review includes:

```text
Who?
What?
When?
Where?
Which Resource?
```

### Investigation Flow

```text
Suspicious Activity
       |
       v
CloudTrail Event History
       |
       v
Event Name
       |
       v
User Identity
       |
       v
Source IP
       |
       v
Event Time
       |
       v
Affected Resource
       |
       v
Security Investigation
```

### Result

**Successfully understood how CloudTrail event information can support AWS security investigations.**

---

## 28. CloudTrail Event History Filtering

### Explanation

CloudTrail Event History can be filtered to locate specific activity.

Filters can include information such as:

```text
Event Name
Event Source
Resource Type
Resource Name
User Name
Read Only
Event Time
```

The exact filters available can vary with the CloudTrail console experience.

### Practical Steps

1. Open CloudTrail.
2. Select **Event history**.
3. Select the appropriate filter.
4. Enter the required value.
5. Apply the filter.
6. Review the matching events.
7. Open an event for detailed investigation.

### Result

**Successfully understood how filtering can be used to locate relevant CloudTrail events efficiently.**

---

## 29. CloudTrail Log File Validation

### Explanation

CloudTrail supports log file integrity validation for trails when configured.

This feature can help determine whether CloudTrail log files have been modified or deleted after delivery.

### Example

```text
CloudTrail
    |
    v
Log Files
    |
    v
Integrity Validation
    |
    v
Security Verification
```

### Result

**Successfully understood the purpose of CloudTrail log file integrity validation.**

---

## 30. CloudTrail Practical Lab - Complete Configuration

### Explanation

In this practical lab, a CloudTrail Trail is created to record AWS management activity and deliver logs to an S3 bucket.

### Architecture

```text
                         AWS Account
                              |
              +---------------+---------------+
              |               |               |
              v               v               v
             EC2             IAM             S3
              |               |               |
              +---------------+---------------+
                              |
                              v
                         CloudTrail
                              |
                              v
                           Trail
                              |
                 +------------+------------+
                 |                         |
                 v                         v
                S3                  CloudWatch Logs
                 |                         |
                 v                         v
          Log File Storage            Monitoring
```

### Practical Steps

### Step 1 - Create S3 Bucket

Create:

```text
Bucket:
aws-lab-cloudtrail-logs-unique
```

Keep the bucket private.

### Step 2 - Open CloudTrail

Go to:

```text
AWS Console
   |
   v
CloudTrail
```

### Step 3 - Create Trail

Select:

```text
Trails
   |
   v
Create trail
```

Enter:

```text
Trail Name:
AWS-Lab-Trail
```

### Step 4 - Configure Management Events

Configure:

```text
Management Events:
Enabled
```

Select the required event types.

Example:

```text
Read:
Enabled

Write:
Enabled
```

### Step 5 - Configure S3 Destination

Select:

```text
S3 Bucket:
aws-lab-cloudtrail-logs-unique
```

### Step 6 - Configure Additional Monitoring

Configure CloudWatch Logs or other supported event types when required.

### Step 7 - Create Trail

Review the configuration.

Click:

```text
Create trail
```

### Step 8 - Perform Test Activity

Perform an AWS action.

Example:

```text
Start EC2 Instance
```

### Step 9 - Check Event History

Open:

```text
CloudTrail
   |
   v
Event history
```

Search for the activity.

### Step 10 - Review Event

Check:

```text
Event Name
Event Source
Event Time
User Identity
Source IP Address
AWS Region
```

### Step 11 - Check S3

Open:

```text
S3
   |
   v
aws-lab-cloudtrail-logs-unique
```

Verify that CloudTrail log files are being delivered.

### Result

**Successfully created a CloudTrail Trail, configured management events, delivered CloudTrail logs to an S3 bucket, performed test AWS activity, and verified the corresponding CloudTrail events.**

---

## 31. CloudTrail Troubleshooting

### Explanation

If CloudTrail events or logs are not appearing as expected, check:

- Trail status
- Event selectors
- AWS Region
- S3 bucket configuration
- S3 bucket permissions
- CloudWatch Logs configuration
- IAM permissions
- Event type
- Event history time range
- Trail configuration

### Troubleshooting Flow

```text
CloudTrail Event Not Found
          |
          v
Check Event History
          |
          v
Check Time Range
          |
          v
Check Region
          |
          v
Check Event Type
          |
          v
Check Trail
          |
          v
Check Event Selectors
          |
          v
Check S3 Destination
          |
          v
Check CloudWatch Logs
          |
          v
Check IAM Permissions
          |
          v
Test Again
```

### Result

**Successfully understood the basic troubleshooting process for CloudTrail event and log-delivery problems.**

---

## 32. CloudTrail Security Best Practices

### Explanation

CloudTrail should be configured carefully because its logs can contain important security and operational information.

Important practices include:

- Enable CloudTrail for required AWS environments.
- Protect CloudTrail logs.
- Keep the S3 log bucket private.
- Restrict access to CloudTrail logs.
- Use appropriate IAM permissions.
- Enable log file integrity validation when required.
- Send logs to centralized storage when appropriate.
- Monitor important CloudTrail events.
- Configure CloudWatch alarms for important security events when required.
- Protect sensitive information from being unnecessarily written to logs.
- Review CloudTrail configuration regularly.
- Retain logs according to organizational and compliance requirements.

### Example

```text
AWS Account
     |
     v
CloudTrail
     |
     v
Protected S3 Bucket
     |
     v
Security Monitoring
     |
     v
Investigation / Compliance
```

### Result

**Successfully understood important security best practices for protecting and monitoring CloudTrail logs.**

---

## 33. CloudTrail vs CloudWatch

### Explanation

CloudTrail and CloudWatch have different primary purposes.

### CloudTrail

Used mainly for:

```text
API Activity
Auditing
Account Activity
Security Investigation
```

### CloudWatch

Used mainly for:

```text
Metrics
Logs
Monitoring
Alarms
Dashboards
```

### Comparison

| Feature | CloudTrail | CloudWatch |
|---|---|---|
| Main Purpose | API Activity and Auditing | Monitoring and Observability |
| Records API Actions | Yes | Not its primary purpose |
| Metrics | Limited event-related metrics | Yes |
| Logs | CloudTrail Event Logs | Application/System/AWS Logs |
| Alarms | Can integrate with monitoring workflows | Yes |
| Dashboards | No primary dashboard function | Yes |
| Security Investigation | Strong Use Case | Supporting Use Case |

### Example

```text
AWS API Activity
       |
       v
CloudTrail
       |
       v
Who / What / When / Where


Resource Performance
       |
       v
CloudWatch
       |
       v
Metrics / Logs / Alarms
```

### Result

**Successfully understood the difference between CloudTrail and CloudWatch and how they can complement each other.**

---

## 34. CloudTrail Complete Security Monitoring Architecture

```text
                              AWS Account
                                  |
             +--------------------+--------------------+
             |                    |                    |
             v                    v                    v
            IAM                  EC2                   S3
             |                    |                    |
             +--------------------+--------------------+
                                  |
                                  v
                             CloudTrail
                                  |
                     +------------+------------+
                     |                         |
                     v                         v
                    S3                  CloudWatch Logs
                     |                         |
                     v                         v
               Log Storage               Monitoring
                                               |
                                               v
                                           CloudWatch
                                               |
                                               v
                                             Alarm
                                               |
                                               v
                                           SNS / Alert
```

---

## 35. CloudTrail Investigation Workflow

### Workflow

```text
AWS Activity
     |
     v
CloudTrail
     |
     v
Event History
     |
     v
Filter Event
     |
     v
Identify User
     |
     v
Identify Action
     |
     v
Identify Source IP
     |
     v
Identify Resource
     |
     v
Check Event Time
     |
     v
Investigate
     |
     v
Take Security Action
```

### Result

**Successfully understood the complete workflow for investigating AWS activity using CloudTrail.**

---

## 36. Complete CloudTrail Workflow

### Workflow

```text
AWS Account
     |
     v
AWS API Activity
     |
     v
CloudTrail
     |
     +---- Event History
     |
     +---- Management Events
     |
     +---- Data Events
     |
     v
CloudTrail Trail
     |
     +---- S3
     |
     +---- CloudWatch Logs
     |
     v
Monitoring / Auditing
     |
     v
Security Investigation
     |
     v
Compliance / Response
```

### Practical Steps

1. Create or select an AWS account environment.
2. Open CloudTrail.
3. Review Event History.
4. Perform a controlled AWS test action.
5. Locate the event.
6. Review the event details.
7. Identify the user identity.
8. Identify the event name.
9. Identify the event source.
10. Identify the event time.
11. Identify the source IP address.
12. Identify the AWS Region.
13. Create a CloudTrail Trail.
14. Configure management events.
15. Configure data events when required.
16. Create or select a secure S3 bucket.
17. Configure S3 log delivery.
18. Configure CloudWatch Logs when required.
19. Enable log file integrity validation when required.
20. Test the Trail.
21. Verify logs in S3.
22. Verify events in CloudWatch Logs when configured.
23. Create monitoring and alerting workflows when required.
24. Review CloudTrail regularly.
25. Protect and retain CloudTrail logs according to requirements.

### Final Result

**Successfully completed Lab 16 - AWS CloudTrail and understood how CloudTrail records AWS account activity and API actions for auditing, security monitoring, troubleshooting, and compliance. Learned about CloudTrail Events, Event History, Management Events, Data Events, Read and Write Events, Trails, Event Selectors, User Identity, Event Name, Event Source, Source IP Address, AWS Region, S3 log storage, CloudWatch Logs integration, IAM and EC2 activity auditing, security investigations, troubleshooting, and CloudTrail security best practices.**
