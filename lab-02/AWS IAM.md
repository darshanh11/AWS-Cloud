# Lab 02 - AWS Identity and Access Management (IAM)

## Objective

The objective of this lab is to understand **AWS Identity and Access Management (IAM)** and practically explore **IAM Users, IAM Groups, IAM Policies, IAM Roles, Multi-Factor Authentication (MFA), Access Keys, Authentication, Authorization, and the Principle of Least Privilege**.

---

## 1. What is IAM?

### Explanation

**AWS Identity and Access Management (IAM)** is an AWS service used to securely control access to AWS resources.

IAM allows administrators to control:

- Who can access AWS resources
- Which AWS resources they can access
- What actions they can perform
- What permissions they have

IAM helps protect AWS resources from unauthorized access.

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **IAM** in the AWS services search bar.
3. Open the **IAM** service.
4. Open the **IAM Dashboard**.
5. Explore the available IAM features.
6. Review **Users**, **User groups**, **Policies**, **Roles**, and **Security credentials**.

### Result

**Successfully opened the IAM service and understood how IAM is used to securely manage access to AWS resources.**

---

## 2. IAM Components

### Explanation

The main components of AWS IAM are:

- **IAM Users** - Represents individual identities.
- **IAM Groups** - A collection of IAM users.
- **IAM Policies** - Define permissions.
- **IAM Roles** - Provide permissions to trusted entities.
- **MFA** - Provides an additional layer of security.
- **Access Keys** - Provide programmatic access.
- **Permissions** - Define which actions an identity can perform.

### IAM Structure

```text
                         AWS IAM
                            |
          +-----------------+------------------+
          |                 |                  |
        Users             Groups             Roles
          |                 |                  |
          +-----------------+------------------+
                            |
                            v
                         Policies
                            |
                            v
                       Permissions
                            |
                            v
                     AWS Resources
```

### Practical Steps

1. Open the **IAM Dashboard**.
2. Open **Users**.
3. Open **User groups**.
4. Open **Policies**.
5. Open **Roles**.
6. Review **Security credentials**.
7. Review **MFA** options.
8. Understand how these components work together to control access.

### Result

**Successfully identified and explored the major components of AWS IAM.**

---

## 3. IAM Users

### Explanation

An **IAM User** represents an individual person or application that requires access to AWS resources.

An IAM user can have:

- Username
- Password
- Permissions
- Access Keys
- MFA

IAM users are useful when individual identities need specific access to AWS resources.

### Example

```text
IAM User
   |
   +-- Username
   +-- Password
   +-- Permissions
   +-- Access Keys
   +-- MFA
```

### Practical Steps

1. Open the **AWS Management Console**.
2. Search for **IAM**.
3. Open **IAM**.
4. Select **Users**.
5. Click **Create user**.
6. Enter the required username.
7. Configure the required access.
8. Assign the required permissions.
9. Review the configuration.
10. Create the user.
11. Verify that the user appears in the **Users** list.
12. Open the user and review the available permissions and security settings.

### Result

**Successfully created and verified an IAM User and understood how individual AWS identities are managed.**

---

## 4. IAM Groups

### Explanation

An **IAM Group** is a collection of IAM users.

Groups are useful when multiple users require similar permissions.

Instead of assigning the same policy individually to every user, policies can be attached to a group.

### Example

```text
Developers Group
       |
       +-- User 1
       +-- User 2
       +-- User 3
```

If a policy is attached to the **Developers** group, users in the group can receive the permissions provided by that policy.

### Practical Steps

1. Open **IAM**.
2. Select **User groups**.
3. Click **Create group**.
4. Enter a group name.
5. Select the users to add to the group.
6. Select the required permission policies.
7. Review the configuration.
8. Create the group.
9. Open the created group.
10. Verify the users in the group.
11. Verify the policies attached to the group.

### Result

**Successfully created and configured an IAM Group and understood how groups simplify permission management for multiple users.**

---

## 5. IAM Policies

### Explanation

An **IAM Policy** is a JSON document that defines permissions.

Policies determine which AWS actions are **Allowed** or **Denied** for specific AWS resources.

### Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    }
  ]
}
```

### Policy Elements

| Element | Description |
|---|---|
| **Version** | Defines the policy language version |
| **Effect** | Specifies `Allow` or `Deny` |
| **Action** | Defines the AWS operation |
| **Resource** | Defines the AWS resource |
| **Condition** | Defines optional conditions |

### Practical Steps

1. Open **IAM**.
2. Select **Policies**.
3. Click **Create policy**.
4. Select the required AWS service.
5. Select the required actions.
6. Select the required resources.
7. Configure conditions if required.
8. Review the permissions.
9. Create the policy.
10. Open the created policy.
11. Review the **JSON policy document**.
12. Verify the permissions.
13. Attach the policy to the appropriate user, group, or role if required.

### Result

**Successfully created or explored an IAM Policy and understood how policies define permissions for AWS resources.**

---

## 6. IAM Roles

### Explanation

An **IAM Role** is an identity that provides permissions to trusted entities such as AWS services, applications, and users.

Roles are commonly used when one AWS service needs permission to access another AWS service.

For example, an EC2 instance can use an IAM Role to access an S3 bucket without storing long-term access keys on the instance.

### Example

```text
EC2 Instance
      |
      v
  IAM Role
      |
      v
S3 Permissions
      |
      v
  S3 Bucket
```

### Practical Steps

1. Open **IAM**.
2. Select **Roles**.
3. Click **Create role**.
4. Select the trusted entity.
5. Select the required permissions.
6. Enter a role name.
7. Review the trust relationship and permission configuration.
8. Create the role.
9. Open the created role.
10. Review the attached policies.
11. Verify the role configuration.

### Result

**Successfully created and explored an IAM Role and understood how roles provide permissions to trusted entities.**

---

## 7. Multi-Factor Authentication (MFA)

### Explanation

**Multi-Factor Authentication (MFA)** provides an additional layer of security for an AWS identity.

MFA requires an additional authentication factor along with the normal login credentials.

### Example

```text
Username + Password
        |
        v
       MFA
        |
        v
    AWS Access
```

### Practical Steps

1. Open **IAM**.
2. Select the required IAM user.
3. Open **Security credentials**.
4. Locate the **Multi-factor authentication (MFA)** section.
5. Select the option to assign MFA.
6. Select the appropriate MFA device.
7. Configure the authenticator application or device.
8. Enter the required verification codes.
9. Complete the MFA setup.
10. Verify that MFA is enabled.

### Result

**Successfully configured and verified MFA and understood how it provides an additional layer of security for AWS identities.**

---

## 8. Access Keys

### Explanation

**Access Keys** are credentials used for programmatic access to AWS services.

They are commonly used with:

- AWS CLI
- AWS SDK
- Applications
- Automation tools

An access key consists of:

```text
Access Key ID
Secret Access Key
```

### Example

```text
Application
     |
     v
Access Keys
     |
     v
AWS API
     |
     v
AWS Resource
```

### Practical Steps

1. Open **IAM**.
2. Select the required IAM user.
3. Open **Security credentials**.
4. Locate **Access keys**.
5. Review the available access key options.
6. Create an access key only when programmatic access is required.
7. Select the appropriate use case.
8. Store the credentials securely.
9. Configure the credentials securely in the required AWS CLI or application environment.

### Security

**Never upload AWS Access Keys or Secret Access Keys to GitHub.**

Do not:

- Put credentials inside source code.
- Commit credentials to Git.
- Share secret keys publicly.
- Store credentials inside README files.

### Result

**Successfully understood Access Keys, their purpose, and the importance of securely protecting AWS credentials.**

---

## 9. Authentication

### Explanation

**Authentication** is the process of verifying the identity of a user or application.

It answers:

> **Who are you?**

AWS can verify an identity using credentials and MFA.

### Example

```text
Username
   +
Password
   +
MFA
   |
   v
Authentication
```

### Practical Steps

1. Open the **AWS Management Console**.
2. Enter valid login credentials.
3. Enter the MFA verification code if MFA is enabled.
4. AWS verifies the identity.
5. After successful authentication, AWS provides access according to the identity and its permissions.

### Result

**Successfully understood how AWS authentication verifies the identity of a user before providing access.**

---

## 10. Authorization

### Explanation

**Authorization** determines what an authenticated identity is allowed to do.

It answers:

> **What are you allowed to do?**

Authorization is controlled using IAM policies and permissions.

### Example

```text
Authenticated User
        |
        v
    IAM Policy
        |
        v
   Allow / Deny
```

For example, a user may be allowed to read an S3 object but may not be allowed to delete it.

### Practical Steps

1. Authenticate into AWS.
2. Request access to an AWS resource.
3. AWS identifies the IAM user, group, or role.
4. AWS evaluates the applicable policies.
5. AWS checks the requested action.
6. AWS determines whether the action is allowed or denied.
7. Verify the access result.

### Result

**Successfully understood how AWS authorization determines whether an authenticated identity can perform a requested action.**

---

## 11. Authentication vs Authorization

### Explanation

**Authentication** verifies the identity of a user, while **Authorization** determines what that authenticated user is allowed to do.

### Comparison

| Authentication | Authorization |
|---|---|
| Verifies identity | Determines permissions |
| Answers "Who are you?" | Answers "What can you do?" |
| Uses credentials | Uses IAM policies |
| Verifies the identity | Determines resource access |

### Example

```text
Authentication
      |
      v
Who are you?
      |
      v
User Identity
      |
      v
Authorization
      |
      v
What can you do?
      |
      v
IAM Permissions
```

### Practical Steps

1. Sign in using valid AWS credentials.
2. Complete MFA if enabled.
3. Confirm successful authentication.
4. Attempt to access an AWS resource.
5. AWS evaluates the assigned permissions.
6. Observe whether access is allowed or denied.

### Result

**Successfully understood the difference between authentication and authorization in AWS IAM.**

---

## 12. Principle of Least Privilege

### Explanation

The **Principle of Least Privilege** means providing only the permissions required to perform a specific task.

For example, if a developer only needs to read an S3 bucket, the developer should receive only the required S3 read permissions instead of full administrator access.

### Example

```text
Developer
    |
    v
Required Permissions
    |
    v
S3 Read Access
```

### Practical Steps

1. Identify what the user needs to do.
2. Identify the AWS resources required.
3. Identify the minimum actions required.
4. Create or select a policy containing only those permissions.
5. Assign the policy to the appropriate user, group, or role.
6. Test the required access.
7. Remove unnecessary permissions.
8. Verify that the user can perform only the required actions.

### Result

**Successfully understood and applied the Principle of Least Privilege to provide only the required AWS permissions.**

---

## 13. IAM Permission Flow

### Explanation

IAM permissions determine whether an identity can perform a specific action on an AWS resource.

### Permission Flow

```text
User / Role
     |
     v
IAM Policy
     |
     v
Requested Action
     |
     v
AWS Resource
     |
     v
Allow / Deny
```

### Example

A user attempts to read an S3 object:

```text
IAM User
    |
    v
Read S3 Object
    |
    v
IAM Policy Evaluation
    |
    +---- Allow ----> Access Granted
    |
    +---- Deny -----> Access Denied
```

An explicit **Deny** takes precedence over an **Allow**.

### Practical Steps

1. Select an IAM user, group, or role.
2. Assign an IAM policy.
3. Request access to an AWS resource.
4. AWS evaluates the applicable policies.
5. AWS checks the requested action.
6. AWS determines whether the action is allowed or denied.
7. Verify the result.

### Result

**Successfully understood how IAM policies are evaluated to control access to AWS resources.**
