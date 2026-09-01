# Lab 17 - AWS Lambda

## Objective

The objective of this lab is to understand **AWS Lambda** and practically learn how to create, configure, execute, monitor, and secure a serverless function.

This lab covers:

- AWS Lambda
- Serverless Computing
- Lambda Function
- Function Code
- Runtime
- Handler
- Event
- Trigger
- Execution Role
- IAM Role
- Environment Variables
- Lambda Layers
- Memory
- Timeout
- Concurrency
- Versions
- Aliases
- CloudWatch Logs
- CloudWatch Monitoring
- Invocation
- Synchronous Invocation
- Asynchronous Invocation
- Event-Driven Architecture
- Lambda with S3
- Lambda with API Gateway
- Lambda with CloudWatch
- Lambda Security
- Practical Lambda Configuration
- Troubleshooting
- Best Practices

---

## 1. What is AWS Lambda?

### Explanation

**AWS Lambda** is a serverless compute service that allows you to run code without managing servers.

You upload your function code and AWS manages the underlying compute infrastructure.

Lambda automatically runs the function when it is invoked by an event or request.

### Example

```text
Event
  |
  v
AWS Lambda
  |
  v
Lambda Function
  |
  v
Result
```

### Result

**Successfully understood that AWS Lambda runs code without requiring the user to manage servers.**

---

## 2. What is Serverless Computing?

### Explanation

**Serverless computing** means the cloud provider manages the underlying server infrastructure while the user focuses mainly on application code.

Serverless does not mean that servers do not exist.

AWS manages:

- Servers
- Infrastructure
- Capacity
- Operating system maintenance
- Scaling infrastructure

The user manages:

- Function code
- Configuration
- Permissions
- Application logic

### Example

```text
Traditional EC2:

User
 |
 v
EC2
 |
 +---- OS
 +---- Server
 +---- Runtime
 +---- Application
 |
 v
Management


Serverless Lambda:

User
 |
 v
Lambda Function
 |
 v
AWS Managed Infrastructure
```

### Result

**Successfully understood the concept of serverless computing and how Lambda reduces infrastructure management.**

---

## 3. Why is AWS Lambda Used?

### Explanation

Lambda is useful for applications that need code to run in response to events without maintaining continuously running servers.

Common use cases include:

- API backends
- File processing
- Automation
- Scheduled tasks
- Event processing
- Data processing
- AWS resource automation

### Example

```text
S3 Upload
    |
    v
Lambda
    |
    v
Process File
```

### Result

**Successfully understood common use cases for AWS Lambda.**

---

## 4. Lambda Function

### Explanation

A **Lambda function** contains the code that AWS executes.

A function includes:

```text
Function Name
Runtime
Handler
Code
Execution Role
Configuration
```

### Example

```text
Lambda Function
     |
     +---- Runtime
     |
     +---- Handler
     |
     +---- Code
     |
     +---- Execution Role
     |
     +---- Configuration
```

### Result

**Successfully understood the main components of an AWS Lambda function.**

---

## 5. Lambda Runtime

### Explanation

The **runtime** provides the environment required to execute Lambda function code.

Examples of supported runtimes can include:

```text
Python
Node.js
Java
.NET
Ruby
Go
```

The exact runtime versions available depend on AWS's current Lambda support.

### Example

```text
Lambda Function
      |
      v
Runtime
      |
      v
Execute Code
```

### Result

**Successfully understood the purpose of a Lambda runtime.**

---

## 6. Lambda Handler

### Explanation

The **handler** identifies the function in your code that Lambda should invoke.

For Python, an example handler can be:

```text
lambda_function.lambda_handler
```

This means:

```text
lambda_function
       |
       v
lambda_handler()
```

### Example Code

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Hello from AWS Lambda!"
    }
```

### Result

**Successfully understood how the Lambda handler identifies the function that Lambda executes.**

---

## 7. Lambda Event

### Explanation

An **event** is input data provided to a Lambda function when it is invoked.

The event can contain information about what triggered the function.

### Example

```text
Event
 |
 v
Lambda
 |
 v
Function
 |
 v
Response
```

A Python Lambda function can access the event using:

```python
def lambda_handler(event, context):
    print(event)
```

### Result

**Successfully understood that an event provides input information to a Lambda function.**

---

## 8. Lambda Context

### Explanation

The **context** object provides information about the current Lambda invocation and execution environment.

Python example:

```python
def lambda_handler(event, context):
    print(context)
```

It can provide information such as:

```text
Function Name
Request ID
Remaining Execution Time
Memory Limit
```

### Result

**Successfully understood the purpose of the Lambda context object.**

---

## 9. Creating a Lambda Function

### Practical Steps

1. Sign in to the AWS Management Console.
2. Search for **Lambda**.
3. Open the Lambda service.
4. Select **Functions**.
5. Click **Create function**.
6. Select:

```text
Author from scratch
```

7. Enter the function name.

Example:

```text
AWS-Lab-Lambda
```

8. Select the required runtime.

Example:

```text
Python
```

9. Configure the execution role.
10. Select the option to create a new role with basic Lambda permissions when appropriate.
11. Review the configuration.
12. Click **Create function**.
13. Wait for the function to be created.
14. Open the function.

### Result

**Successfully created an AWS Lambda function using the AWS Management Console.**

---

## 10. Lambda Function Code

### Explanation

Lambda allows function code to be written or uploaded depending on the deployment method.

For a basic Python Lambda function:

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Hello from AWS Lambda!"
    }
```

### Code Explanation

```text
def lambda_handler(event, context):
```

Defines the function that Lambda invokes.

```text
event
```

Contains input event data.

```text
context
```

Contains information about the current invocation.

```text
return
```

Returns the function response.

### Result

**Successfully created basic Lambda function code and understood the purpose of the handler, event, context, and response.**

---

## 11. Testing a Lambda Function

### Practical Steps

1. Open the Lambda function.
2. Select the **Test** option.
3. Create a new test event when required.
4. Enter an event name.

Example:

```text
LambdaTest
```

5. Use a basic JSON event.

```json
{
  "message": "Hello Lambda"
}
```

6. Save the test event.
7. Click **Test**.
8. Review the execution result.
9. Review the function response.
10. Review the execution logs.

### Example Result

```text
Status:
Succeeded

Response:
{
    "statusCode": 200,
    "body": "Hello from AWS Lambda!"
}
```

### Result

**Successfully invoked the Lambda function manually and verified the execution result.**

---

## 12. Lambda Invocation

### Explanation

**Invocation** means executing a Lambda function.

A Lambda function can be invoked by:

```text
AWS Console
AWS CLI
AWS SDK
API Gateway
S3
EventBridge
Other AWS Services
```

### Example

```text
Event Source
     |
     v
Lambda Invocation
     |
     v
Lambda Function
     |
     v
Response
```

### Result

**Successfully understood how Lambda functions can be invoked from different sources.**

---

## 13. Synchronous Invocation

### Explanation

With **synchronous invocation**, the caller waits for the Lambda function to complete and receives the response.

### Example

```text
Client
  |
  | Request
  v
Lambda
  |
  | Response
  v
Client
```

Examples can include request-response applications and API integrations.

### Result

**Successfully understood the basic concept of synchronous Lambda invocation.**

---

## 14. Asynchronous Invocation

### Explanation

With **asynchronous invocation**, the event source sends the event to Lambda without waiting for the function's response.

Lambda processes the event asynchronously.

### Example

```text
Event Source
     |
     v
Lambda
     |
     v
Process Event
```

This model is useful for event-driven workloads where an immediate response to the caller is not required.

### Result

**Successfully understood the basic concept of asynchronous Lambda invocation.**

---

## 15. Lambda Execution Role

### Explanation

A Lambda function uses an **IAM execution role** to obtain permission to access AWS resources.

For example, a Lambda function that needs to write logs to CloudWatch Logs requires appropriate permissions through its execution role.

### Architecture

```text
Lambda Function
      |
      v
IAM Execution Role
      |
      v
AWS Permissions
      |
      +---- CloudWatch Logs
      +---- S3
      +---- DynamoDB
      +---- Other AWS Services
```

### Result

**Successfully understood that a Lambda execution role provides the permissions required by a Lambda function.**

---

## 16. Lambda IAM Execution Role Practical Steps

### Practical Steps

1. Open **IAM**.
2. Select **Roles**.
3. Locate the Lambda execution role.
4. Open the role.
5. Review the attached policies.
6. Verify that the role has the required permissions.
7. Return to Lambda.
8. Open the Lambda function.
9. Open **Configuration**.
10. Select **Permissions**.
11. Review the execution role.

### Example

```text
Lambda
 |
 v
Execution Role
 |
 v
IAM Policy
 |
 v
CloudWatch Logs
```

### Result

**Successfully reviewed the IAM execution role associated with the Lambda function.**

---

## 17. Lambda Environment Variables

### Explanation

**Environment variables** allow configuration values to be passed to the Lambda function without placing them directly in the source code.

Example:

```text
DATABASE_HOST
APPLICATION_ENV
LOG_LEVEL
```

### Python Example

```python
import os

def lambda_handler(event, context):
    environment = os.environ.get("APPLICATION_ENV")

    return {
        "statusCode": 200,
        "body": f"Environment: {environment}"
    }
```

### Practical Steps

1. Open the Lambda function.
2. Select **Configuration**.
3. Select **Environment variables**.
4. Click **Edit**.
5. Add a variable.

Example:

```text
Key:
APPLICATION_ENV

Value:
lab
```

6. Save the configuration.
7. Update the function code if required.
8. Test the function.

### Result

**Successfully configured and used Lambda environment variables.**

---

## 18. Lambda Layers

### Explanation

A **Lambda Layer** is a reusable package containing additional code or dependencies that can be shared across Lambda functions.

### Example

```text
Lambda Function 1
       |
       +---- Layer
       |
Lambda Function 2
       |
       +---- Layer
```

Layers can help avoid packaging the same dependencies separately with every function.

### Result

**Successfully understood how Lambda Layers provide reusable dependencies for Lambda functions.**

---

## 19. Lambda Memory

### Explanation

Lambda functions can be configured with a memory allocation.

The memory configuration also affects the amount of CPU available to the function.

Example:

```text
Memory:
128 MB
```

The appropriate memory setting depends on the workload.

### Result

**Successfully understood how Lambda memory configuration affects function execution resources.**

---

## 20. Lambda Timeout

### Explanation

The **timeout** specifies the maximum amount of time a Lambda function can run before AWS terminates the invocation.

Example:

```text
Timeout:
10 seconds
```

The timeout should be configured according to the application's expected execution time.

### Result

**Successfully understood the purpose of the Lambda timeout configuration.**

---

## 21. Lambda Concurrency

### Explanation

**Concurrency** represents the number of Lambda function invocations being processed at the same time.

Lambda can process multiple invocations concurrently depending on available capacity and configured limits.

### Example

```text
Requests
 |   |   |   |
 v   v   v   v
Lambda Lambda Lambda Lambda
```

Concurrency settings can be used to control function execution behavior.

### Result

**Successfully understood the basic concept of Lambda concurrency.**

---

## 22. Lambda Versions

### Explanation

Lambda supports publishing versions of a function.

A published version is an immutable snapshot of the function code and configuration that is associated with that version.

Example:

```text
Lambda Function
      |
      +---- Version 1
      |
      +---- Version 2
      |
      +---- Version 3
```

### Result

**Successfully understood how Lambda versions can be used to manage different published versions of a function.**

---

## 23. Lambda Aliases

### Explanation

A **Lambda alias** is a named pointer to a specific function version.

Examples:

```text
dev
test
production
```

### Example

```text
Alias: production
        |
        v
Version 3
```

If the production alias is updated to point to another version, applications can use the alias without changing the function reference.

### Result

**Successfully understood how Lambda aliases can provide stable names for specific published function versions.**

---

## 24. CloudWatch Logs for Lambda

### Explanation

Lambda integrates with **CloudWatch Logs** to provide execution logs.

Python example:

```python
def lambda_handler(event, context):
    print("Lambda function executed")

    return {
        "statusCode": 200,
        "body": "Success"
    }
```

The `print()` output can appear in the Lambda function's CloudWatch log stream when the execution role has the required logging permissions.

### Architecture

```text
Lambda Function
      |
      v
Execution Logs
      |
      v
CloudWatch Logs
      |
      +---- Log Group
      |
      +---- Log Stream
      |
      +---- Log Events
```

### Result

**Successfully understood how Lambda execution logs can be monitored using CloudWatch Logs.**

---

## 25. Viewing Lambda Logs

### Practical Steps

1. Open **Lambda**.
2. Select the function.
3. Invoke the function.
4. Open the **Monitor** section.
5. Select **View CloudWatch logs**.
6. Open the relevant Log Group.
7. Select the Log Stream.
8. Review the log events.

### Example

```text
START RequestId: example

Lambda function executed

END RequestId: example

REPORT RequestId: example
```

### Result

**Successfully viewed Lambda execution logs in CloudWatch Logs.**

---

## 26. Lambda with S3

### Explanation

Lambda can be triggered by events from Amazon S3.

For example, a Lambda function can run when an object is uploaded to an S3 bucket.

### Architecture

```text
User
 |
 v
S3 Bucket
 |
 | Object Upload
 v
Lambda
 |
 v
Process Object
```

### Result

**Successfully understood how S3 events can trigger Lambda functions.**

---

## 27. Lambda with S3 Practical Lab

### Explanation

In this practical lab, an S3 object upload is used to trigger a Lambda function.

### Practical Steps

### Step 1 - Create S3 Bucket

Create a bucket with a unique name.

Example:

```text
aws-lab-lambda-s3-unique
```

### Step 2 - Create Lambda Function

Create:

```text
AWS-Lab-S3-Lambda
```

Use:

```text
Python
```

### Step 3 - Add Lambda Code

```python
def lambda_handler(event, context):
    print("S3 event received")

    return {
        "statusCode": 200,
        "body": "S3 event processed successfully"
    }
```

### Step 4 - Configure S3 Trigger

1. Open the Lambda function.
2. Select **Add trigger**.
3. Select **S3**.
4. Select the S3 bucket.
5. Select the required event type.
6. Configure the trigger.
7. Save the trigger.

### Step 5 - Upload Object

Upload a test file to the S3 bucket.

Example:

```text
test.txt
```

### Step 6 - Check Lambda

Open CloudWatch Logs.

Verify that the Lambda function was invoked.

### Result

**Successfully configured an S3 event trigger and understood how an S3 object event can invoke a Lambda function.**

---

## 28. Lambda with API Gateway

### Explanation

Amazon API Gateway can provide an HTTP API endpoint that invokes a Lambda function.

### Architecture

```text
Client
  |
  v
API Gateway
  |
  v
Lambda
  |
  v
Application Logic
  |
  v
Response
```

### Result

**Successfully understood how API Gateway can provide an HTTP interface for invoking Lambda functions.**

---

## 29. Lambda with API Gateway Practical Steps

### Practical Steps

1. Create a Lambda function.
2. Open the Lambda function.
3. Select **Add trigger**.
4. Select **API Gateway**.
5. Select the required API configuration.
6. Configure the API endpoint.
7. Add the trigger.
8. Deploy the API when required.
9. Obtain the API endpoint.
10. Send a test HTTP request.
11. Verify the Lambda invocation.
12. Review the Lambda response.
13. Check CloudWatch Logs.

### Example

```text
HTTP Request
     |
     v
API Gateway
     |
     v
Lambda
     |
     v
Response
```

### Result

**Successfully understood the practical workflow for connecting API Gateway with Lambda.**

---

## 30. Lambda Event-Driven Architecture

### Explanation

Lambda is commonly used in event-driven architectures.

An AWS service generates an event and Lambda processes that event.

### Example

```text
S3
 |
 | Event
 v
Lambda
 |
 v
Process Data
 |
 v
Another AWS Service
```

Other event sources can include:

```text
Amazon EventBridge
Amazon SQS
Amazon SNS
Amazon API Gateway
Amazon DynamoDB
Amazon S3
```

### Result

**Successfully understood how Lambda can be used to build event-driven architectures.**

---

## 31. Lambda with EventBridge

### Explanation

Amazon EventBridge can invoke Lambda functions in response to matching events or on a schedule.

### Example

```text
EventBridge
     |
     | Event / Schedule
     v
Lambda
     |
     v
Execute Task
```

### Result

**Successfully understood how EventBridge can invoke Lambda functions using events or schedules.**

---

## 32. Lambda Monitoring

### Explanation

Lambda monitoring can be performed using CloudWatch metrics and logs.

Important information can include:

```text
Invocations
Errors
Duration
Throttles
Concurrent Executions
```

### Example

```text
Lambda
 |
 v
CloudWatch
 |
 +---- Invocations
 +---- Errors
 +---- Duration
 +---- Throttles
 +---- Concurrency
```

### Result

**Successfully understood how CloudWatch can monitor Lambda performance and execution behavior.**

---

## 33. Lambda Error Monitoring

### Explanation

CloudWatch metrics and logs can help identify Lambda execution errors.

### Example

```text
Lambda Execution
      |
      v
Error
      |
      v
CloudWatch
      |
      +---- Error Metric
      |
      +---- Error Logs
      |
      v
Troubleshooting
```

### Practical Steps

1. Open the Lambda function.
2. Invoke the function.
3. Review the execution result.
4. Open CloudWatch Logs.
5. Review the error message.
6. Identify the cause.
7. Correct the function or configuration.
8. Invoke the function again.
9. Verify successful execution.

### Result

**Successfully understood how CloudWatch Logs and metrics can be used to troubleshoot Lambda execution errors.**

---

## 34. Lambda Practical Lab - Complete Configuration

### Explanation

In this practical lab, a Python Lambda function is created, tested, monitored, and configured with an execution role.

### Architecture

```text
                         AWS Lambda
                              |
              +---------------+---------------+
              |               |               |
              v               v               v
            Code          IAM Role        Configuration
              |               |               |
              v               v               v
           Runtime       Permissions      Memory/Timeout
                              |
                              v
                       CloudWatch Logs
```

### Practical Steps

### Step 1 - Open Lambda

Open:

```text
AWS Console
   |
   v
Lambda
```

### Step 2 - Create Function

Select:

```text
Create function
```

Choose:

```text
Author from scratch
```

Enter:

```text
Function Name:
AWS-Lab-Lambda
```

Select:

```text
Runtime:
Python
```

### Step 3 - Configure Execution Role

Create or select the appropriate IAM execution role.

For basic logging, use the AWS-managed permissions or an equivalent least-privilege custom policy appropriate to the lab.

### Step 4 - Add Function Code

```python
def lambda_handler(event, context):
    print("AWS Lambda Lab 17 executed successfully")

    return {
        "statusCode": 200,
        "body": "Hello from AWS Lambda"
    }
```

### Step 5 - Deploy Code

Save or deploy the function code using the Lambda console.

### Step 6 - Create Test Event

Use:

```json
{
    "message": "Lambda Lab Test"
}
```

### Step 7 - Invoke Function

Click:

```text
Test
```

### Step 8 - Verify Response

Expected response:

```json
{
    "statusCode": 200,
    "body": "Hello from AWS Lambda"
}
```

### Step 9 - Check Logs

Open:

```text
Monitor
   |
   v
CloudWatch Logs
```

Verify:

```text
AWS Lambda Lab 17 executed successfully
```

### Step 10 - Review Configuration

Check:

```text
Runtime
Handler
Memory
Timeout
Environment Variables
Execution Role
```

### Result

**Successfully created, deployed, invoked, tested, and monitored a Python AWS Lambda function.**

---

## 35. Lambda Security

### Explanation

Lambda functions should follow the Principle of Least Privilege.

Important security practices include:

- Use a dedicated IAM execution role.
- Grant only required permissions.
- Do not hard-code credentials in Lambda code.
- Protect environment variables.
- Avoid exposing sensitive information in logs.
- Use encryption where required.
- Restrict access to the Lambda function.
- Monitor Lambda activity.
- Keep dependencies updated.
- Use private networking when required.
- Review function permissions regularly.

### Example

```text
Lambda
 |
 v
IAM Execution Role
 |
 v
Least Privilege Permissions
 |
 +---- Required AWS Service
 |
 X---- Unnecessary Permissions
```

### Result

**Successfully understood important security practices for protecting Lambda functions and their AWS permissions.**

---

## 36. Lambda Networking with VPC

### Explanation

A Lambda function can be configured to access resources in a VPC.

This can be useful when Lambda needs to communicate with resources such as private databases or internal services.

### Example

```text
Lambda
   |
   v
VPC
   |
   v
Private Subnet
   |
   v
RDS
```

VPC configuration must be planned carefully because it affects networking, routing, and access to other resources.

### Result

**Successfully understood how Lambda can be configured to communicate with resources inside a VPC.**

---

## 37. Lambda and RDS Architecture

### Explanation

Lambda can be used as an application layer that communicates with an RDS database.

### Example

```text
Client
  |
  v
API Gateway
  |
  v
Lambda
  |
  v
RDS
  |
  v
Database
```

The Lambda execution role and network configuration must provide only the required access.

### Result

**Successfully understood the basic architecture of Lambda communicating with an RDS database.**

---

## 38. Lambda Versions and Aliases Practical Steps

### Practical Steps

1. Open the Lambda function.
2. Create or update the function code.
3. Deploy the code.
4. Publish a new function version.
5. Verify the version number.
6. Create an alias.
7. Enter:

```text
Alias:
production
```

8. Point the alias to the required published version.
9. Save the alias.
10. Verify the alias configuration.

### Example

```text
AWS-Lab-Lambda
      |
      +---- Version 1
      |
      +---- Version 2
      |
      +---- Version 3
                ^
                |
          production
```

### Result

**Successfully understood how Lambda versions and aliases can be used to manage function deployments.**

---

## 39. Lambda Troubleshooting

### Explanation

If a Lambda function does not execute correctly, check:

- Function code
- Runtime
- Handler
- Execution role
- IAM permissions
- Event format
- Trigger configuration
- Timeout
- Memory
- Environment variables
- CloudWatch Logs
- VPC configuration
- Network connectivity
- Resource permissions

### Troubleshooting Flow

```text
Lambda Error
     |
     v
Check Function Code
     |
     v
Check Runtime
     |
     v
Check Handler
     |
     v
Check Execution Role
     |
     v
Check IAM Permissions
     |
     v
Check Trigger
     |
     v
Check Event
     |
     v
Check CloudWatch Logs
     |
     v
Check Timeout / Memory
     |
     v
Check VPC / Network
     |
     v
Test Again
```

### Result

**Successfully understood the basic troubleshooting process for Lambda execution and configuration problems.**

---

## 40. Lambda Common Errors

### Explanation

Common Lambda problems include:

```text
Handler Error
Permission Denied
Timeout
Invalid Event
Missing Dependency
Resource Access Denied
VPC Connectivity Problem
Throttling
```

### Example

```text
Handler Error
     |
     v
Check Handler Name
     |
     v
Check File Name
     |
     v
Check Function Name
     |
     v
Deploy Again
```

### Result

**Successfully understood common Lambda errors and the basic areas to investigate.**

---

## 41. Lambda and CloudWatch Workflow

```text
Lambda Function
      |
      v
Invocation
      |
      v
Execution
      |
      +---- Success
      |
      +---- Error
      |
      v
CloudWatch
      |
      +---- Metrics
      |
      +---- Logs
      |
      +---- Alarms
      |
      v
Monitoring
```

### Result

**Successfully understood how Lambda integrates with CloudWatch for monitoring and troubleshooting.**

---

## 42. Lambda Complete Architecture

```text
                              Client
                                |
                                v
                           API Gateway
                                |
                                v
                         Lambda Function
                                |
              +-----------------+-----------------+
              |                 |                 |
              v                 v                 v
           IAM Role           CloudWatch         S3
              |                 |                 |
              v                 v                 v
         Permissions          Logs/Metric       Objects
                                |
                                v
                             Alarms
```

---

## 43. Lambda Event-Driven Architecture

```text
       +---------+
       |   S3    |
       +----+----+
            |
            v
       +---------+
       | Lambda  |
       +----+----+
            |
            v
       +---------+
       | Process |
       |  Data   |
       +---------+

       +------------+
       | EventBridge|
       +-----+------+
             |
             v
         +-------+
         |Lambda |
         +-------+

       +------------+
       | API Gateway|
       +-----+------+
             |
             v
         +-------+
         |Lambda |
         +-------+
```

### Result

**Successfully understood how Lambda can act as a serverless processing layer for multiple AWS event sources.**

---

## 44. Lambda Complete Workflow

### Workflow

```text
Create Lambda Function
        |
        v
Select Runtime
        |
        v
Configure Handler
        |
        v
Write Function Code
        |
        v
Configure Execution Role
        |
        v
Configure Memory / Timeout
        |
        v
Configure Environment Variables
        |
        v
Deploy Function
        |
        v
Create Test Event
        |
        v
Invoke Function
        |
        v
Check Response
        |
        v
Check CloudWatch Logs
        |
        v
Configure Trigger
        |
        v
Monitor Metrics
        |
        v
Secure Function
        |
        v
Troubleshoot / Optimize
```

### Practical Steps

1. Open AWS Lambda.
2. Create a Lambda function.
3. Select the required runtime.
4. Configure the function name.
5. Configure the handler.
6. Configure the IAM execution role.
7. Write the Lambda function code.
8. Deploy the function.
9. Create a test event.
10. Invoke the function.
11. Verify the response.
12. Review CloudWatch Logs.
13. Configure environment variables when required.
14. Configure memory and timeout.
15. Configure a trigger.
16. Integrate with S3, API Gateway, EventBridge, or another supported event source when required.
17. Monitor Lambda metrics using CloudWatch.
18. Review errors and logs.
19. Configure versions and aliases when required.
20. Follow least-privilege security practices.
21. Remove unused triggers and resources after completing the lab.

### Final Result

**Successfully completed Lab 17 - AWS Lambda and understood serverless computing and event-driven execution. Learned about Lambda functions, runtimes, handlers, events, context, invocation types, execution roles, IAM permissions, environment variables, Layers, memory, timeout, concurrency, versions, aliases, CloudWatch Logs, monitoring, S3 triggers, API Gateway integration, EventBridge integration, VPC networking, RDS integration, troubleshooting, and Lambda security best practices.**
