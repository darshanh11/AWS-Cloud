# Lab 14 - Amazon RDS

## Objective

The objective of this lab is to understand **Amazon Relational Database Service (RDS)** and practically learn how to create, configure, connect to, monitor, back up, and manage a relational database in AWS.

This lab covers:

- Amazon RDS
- Relational Database
- Database Engine
- DB Instance
- Database Endpoint
- Database Port
- VPC
- Subnet Group
- Security Group
- Public and Private Database
- Multi-AZ
- Read Replicas
- Automated Backups
- Manual Snapshots
- Encryption
- Monitoring
- Database Connectivity
- RDS Architecture
- Practical RDS Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is Amazon RDS?

### Explanation

**Amazon Relational Database Service (RDS)** is a managed AWS service used to run relational databases.

AWS manages many infrastructure and administrative tasks such as:

- Database provisioning
- Hardware management
- Operating system maintenance
- Automated backups
- Software patching
- Monitoring
- High availability options

RDS supports multiple database engines.

Common examples include:

```text
Amazon Aurora
MySQL
PostgreSQL
MariaDB
Oracle
Microsoft SQL Server
```

### Example

```text
                    AWS Cloud
                        |
                        v
                       RDS
                        |
            +-----------+-----------+
            |           |           |
            v           v           v
          MySQL    PostgreSQL    Oracle
```

### Result

**Successfully understood that Amazon RDS is a managed AWS service for running relational databases.**

---

## 2. What is a Relational Database?

### Explanation

A **relational database** stores data in tables consisting of rows and columns.

Example:

```text
Users Table

+----+----------+-------------------+
| ID | Name     | Email             |
+----+----------+-------------------+
| 1  | Darshan  | user@example.com  |
| 2  | User2    | user2@example.com |
+----+----------+-------------------+
```

Relational databases use SQL to create, read, update, and delete data.

### Common SQL Operations

```text
CREATE
SELECT
INSERT
UPDATE
DELETE
```

### Result

**Successfully understood how relational databases organize data using tables, rows, and columns.**

---

## 3. RDS Database Engines

### Explanation

RDS supports several relational database engines.

Common options include:

```text
MySQL
PostgreSQL
MariaDB
Oracle
Microsoft SQL Server
Amazon Aurora
```

The database engine should be selected according to the application's requirements.

### Example

```text
Application
     |
     v
Amazon RDS
     |
     +---- MySQL
     |
     +---- PostgreSQL
     |
     +---- MariaDB
     |
     +---- Oracle
     |
     +---- SQL Server
     |
     +---- Aurora
```

### Result

**Successfully understood the major database engines available through Amazon RDS.**

---

## 4. What is an RDS DB Instance?

### Explanation

An RDS **DB instance** is the database environment that runs the selected database engine.

It provides the compute, memory, storage, and networking required by the database.

### Example

```text
Amazon RDS
     |
     v
DB Instance
     |
     +---- Database Engine
     |
     +---- CPU
     |
     +---- Memory
     |
     +---- Storage
     |
     +---- Network
```

### Result

**Successfully understood that an RDS DB instance provides the environment in which the selected relational database engine runs.**

---

## 5. RDS VPC

### Explanation

An RDS DB instance runs inside a VPC.

The VPC provides the network environment for the database.

Example:

```text
VPC
10.0.0.0/16
      |
      v
RDS
      |
      v
DB Instance
```

The RDS database can communicate with other AWS resources according to the configured network and security rules.

### Result

**Successfully understood the relationship between Amazon RDS and a VPC.**

---

## 6. RDS Subnet Group

### Explanation

A **DB subnet group** is a collection of subnets that you can designate for your RDS database instances.

For production architectures, subnets in multiple Availability Zones are commonly used.

### Example

```text
                    VPC
                     |
              DB Subnet Group
                 /       \
                v         v
          Subnet A     Subnet B
             |            |
             v            v
          AZ-A           AZ-B
```

### Practical Steps

1. Open the **RDS** service.
2. Select **Subnet groups**.
3. Click **Create DB subnet group**.
4. Enter the subnet group name.

Example:

```text
AWS-RDS-Subnet-Group
```

5. Enter the description.
6. Select the required VPC.
7. Select Availability Zones.
8. Select the required subnets.
9. Create the subnet group.
10. Verify the subnet group.

### Result

**Successfully created an RDS DB subnet group using the selected VPC subnets.**

---

## 7. RDS Security Group

### Explanation

A Security Group controls network traffic to and from the RDS DB instance.

The database should normally allow access only from the application resources that need it.

### Example

```text
Application Server
       |
       v
Security Group
       |
       v
RDS Security Group
       |
       v
Database
```

### Common Database Ports

```text
MySQL:
3306

PostgreSQL:
5432

Microsoft SQL Server:
1433

Oracle:
1521
```

### Result

**Successfully understood how Security Groups control network access to an RDS database.**

---

## 8. Creating an RDS Security Group

### Explanation

A dedicated Security Group can be created for the database.

Example:

```text
Security Group:
AWS-RDS-SG

Description:
Security Group for RDS Database
```

The inbound database port should preferably allow traffic from the application's Security Group rather than from the entire internet.

### Practical Steps

1. Open **EC2 > Security Groups**.
2. Click **Create security group**.
3. Enter:

```text
Name:
AWS-RDS-SG
```

4. Select the RDS VPC.
5. Configure the inbound rule.
6. Select the database engine port.

Example for MySQL:

```text
Type:
MySQL/Aurora

Port:
3306

Source:
Application Security Group
```

7. Configure outbound rules according to requirements.
8. Create the Security Group.
9. Verify the configuration.

### Result

**Successfully created a dedicated Security Group for the RDS database.**

---

## 9. RDS Database Endpoint

### Explanation

An RDS database has an **endpoint** that applications use to connect to the database.

Example:

```text
RDS Endpoint
     |
     v
database.xxxxxxxxx.region.rds.amazonaws.com
     |
     v
Database
```

The endpoint is used instead of manually connecting to an instance's IP address.

### Result

**Successfully understood that the RDS endpoint provides the connection address for applications and database clients.**

---

## 10. RDS Database Port

### Explanation

Each database engine commonly uses a default port.

Examples:

```text
MySQL:
3306

PostgreSQL:
5432

SQL Server:
1433

Oracle:
1521
```

The port must be permitted by the applicable Security Group and network configuration.

### Result

**Successfully understood the relationship between the database engine, database port, and Security Group configuration.**

---

## 11. Creating an RDS Database

### Explanation

An RDS database can be created from the AWS RDS console.

### Practical Steps

1. Sign in to AWS.
2. Search for **RDS**.
3. Open the **Amazon RDS** service.
4. Select **Databases**.
5. Click **Create database**.
6. Select the database creation method.
7. Select the database engine.

Example:

```text
MySQL
```

8. Select the required engine version.
9. Choose the appropriate template.
10. Configure the DB instance identifier.

Example:

```text
aws-lab-rds
```

11. Configure master credentials.
12. Select the required DB instance class.
13. Configure storage.
14. Select the VPC.
15. Select the DB subnet group.
16. Select the RDS Security Group.
17. Configure database port.
18. Configure backups.
19. Configure monitoring when required.
20. Review the configuration.
21. Click **Create database**.
22. Wait until the database becomes available.

### Result

**Successfully created an Amazon RDS database instance using the selected database engine and VPC configuration.**

---

## 12. RDS Database Identifier

### Explanation

A **DB instance identifier** is the name used to identify the RDS database instance within AWS.

Example:

```text
DB Instance Identifier:

aws-lab-rds
```

It helps identify the database when managing multiple RDS instances.

### Result

**Successfully understood the purpose of the RDS DB instance identifier.**

---

## 13. RDS Master Credentials

### Explanation

During database creation, administrative database credentials are configured.

Example:

```text
Master Username:
admin

Master Password:
Strong Password
```

Credentials should be stored securely and should not be hard-coded into applications or GitHub repositories.

### Security Practice

```text
Do NOT store:

Username + Password

inside:

GitHub Repository
Public README
Source Code
```

Use appropriate secrets-management mechanisms for applications.

### Result

**Successfully understood how database credentials are configured and why database passwords must be protected.**

---

## 14. RDS Public Access

### Explanation

RDS can be configured with public connectivity, but databases should generally not be exposed directly to the internet unless there is a specific requirement and appropriate security controls.

A safer architecture is commonly:

```text
Internet
    |
    v
Load Balancer
    |
    v
Application
    |
    v
Private RDS
```

### Result

**Successfully understood the difference between public and private database connectivity and the importance of keeping databases protected from unnecessary internet exposure.**

---

## 15. RDS Private Architecture

### Explanation

A common production architecture places the RDS database in private subnets.

### Example

```text
                         Internet
                             |
                             v
                       Load Balancer
                             |
                             v
                     Application Servers
                             |
                             v
                       Private Subnet
                             |
                             v
                            RDS
```

The database is not directly accessible from the public internet.

### Result

**Successfully understood why RDS databases are commonly placed in private network segments.**

---

## 16. RDS and EC2 Connectivity

### Explanation

An EC2 application server can connect to an RDS database when the VPC, subnet routing, Security Groups, database port, and database configuration allow the connection.

### Example

```text
EC2 Application
       |
       v
EC2 Security Group
       |
       v
VPC Network
       |
       v
RDS Security Group
       |
       v
RDS Database
```

### Practical Steps

1. Launch an EC2 instance in the same VPC or a connected network.
2. Configure the EC2 Security Group.
3. Configure the RDS Security Group.
4. Allow the database port from the application Security Group.
5. Obtain the RDS endpoint.
6. Use the appropriate database client.
7. Connect using the database endpoint.
8. Verify database connectivity.

### Result

**Successfully understood how an EC2 application can connect to an RDS database using VPC networking and Security Groups.**

---

## 17. RDS Multi-AZ

### Explanation

**Multi-AZ deployment** provides a high-availability configuration for supported RDS engines.

RDS maintains a standby database in another Availability Zone.

The standby is not normally used to serve read traffic.

If the primary database becomes unavailable, RDS can fail over to the standby.

### Architecture

```text
                         RDS
                          |
             +------------+------------+
             |                         |
             v                         v
       Availability Zone A      Availability Zone B
             |                         |
             v                         v
          Primary                  Standby
          Database                Database
```

### Result

**Successfully understood how Multi-AZ improves RDS availability through a standby database in another Availability Zone.**

---

## 18. RDS Read Replica

### Explanation

A **Read Replica** is a separate database instance that can be used to handle read traffic.

It can help scale read-heavy workloads.

### Architecture

```text
                    Primary RDS
                        |
                        v
                  Read Replica
                        |
                        v
                  Read Requests
```

Multiple read replicas can be used depending on the database engine and configuration.

### Multi-AZ vs Read Replica

| Feature | Multi-AZ | Read Replica |
|---|---|---|
| Main Purpose | High Availability | Read Scaling |
| Primary Use | Failover | Read Traffic |
| Standby/Replica | Standby | Readable Replica |
| Read Traffic | Not normally served by standby | Yes |

### Result

**Successfully understood the difference between Multi-AZ deployments and Read Replicas.**

---

## 19. RDS Automated Backups

### Explanation

RDS provides automated backup capabilities.

Automated backups can be used to support point-in-time recovery within the configured backup retention period.

### Practical Steps

1. Open the RDS database.
2. Select the database instance.
3. Open the **Maintenance and backups** section.
4. Review the backup configuration.
5. Verify the backup retention settings.
6. Review the available automated backups.

### Result

**Successfully understood how automated backups help protect RDS databases and support recovery.**

---

## 20. RDS Manual Snapshot

### Explanation

An RDS **DB snapshot** is a user-initiated backup of a DB instance.

Snapshots can be retained for longer-term recovery requirements.

### Practical Steps

1. Open **RDS**.
2. Select **Databases**.
3. Select the RDS database.
4. Choose **Actions**.
5. Select **Take snapshot**.
6. Enter the snapshot identifier.

Example:

```text
aws-lab-rds-snapshot
```

7. Create the snapshot.
8. Wait for the snapshot to complete.
9. Verify the snapshot.

### Result

**Successfully created a manual RDS DB snapshot for backup and recovery purposes.**

---

## 21. Restoring an RDS Snapshot

### Explanation

An RDS snapshot can be used to create a new database instance.

### Practical Steps

1. Open **RDS > Snapshots**.
2. Select the required snapshot.
3. Choose **Actions**.
4. Select **Restore snapshot**.
5. Configure the new DB instance.
6. Select the VPC.
7. Select the DB subnet group.
8. Select the Security Group.
9. Review the configuration.
10. Restore the database.
11. Wait until the new database becomes available.
12. Verify the new RDS endpoint.

### Result

**Successfully understood how an RDS snapshot can be restored to create a new database instance.**

---

## 22. RDS Encryption

### Explanation

RDS supports encryption at rest using AWS Key Management Service (AWS KMS).

Encryption can protect database storage, automated backups, read replicas, and snapshots according to the supported configuration.

### Example

```text
RDS Database
     |
     v
Encrypted Storage
     |
     v
AWS KMS
```

### Result

**Successfully understood how encryption can protect RDS data at rest.**

---

## 23. RDS Monitoring

### Explanation

Amazon RDS integrates with **Amazon CloudWatch** for monitoring database metrics.

Examples include:

```text
CPU Utilization
Database Connections
Free Storage Space
Read IOPS
Write IOPS
Network Traffic
```

The exact metrics available depend on the database engine and configuration.

### Example

```text
RDS
 |
 v
CloudWatch
 |
 +---- CPU
 |
 +---- Connections
 |
 +---- Storage
 |
 +---- IOPS
```

### Result

**Successfully understood how CloudWatch can be used to monitor RDS database performance and resource utilization.**

---

## 24. RDS Maintenance

### Explanation

RDS provides managed maintenance capabilities such as database software patching according to the configured maintenance settings.

Maintenance can be configured with a preferred maintenance window.

### Practical Steps

1. Open the RDS database.
2. Select the database instance.
3. Open the **Maintenance** section.
4. Review the maintenance settings.
5. Review the preferred maintenance window.
6. Configure the settings according to requirements.

### Result

**Successfully understood how RDS provides managed database maintenance and configurable maintenance windows.**

---

## 25. RDS Scaling

### Explanation

RDS resources can be adjusted according to application requirements.

Scaling can involve:

```text
Compute Capacity
Storage
Read Capacity
```

The exact scaling options depend on the RDS engine and configuration.

### Example

```text
Low Database Demand
       |
       v
Smaller Resources


High Database Demand
       |
       v
Larger Resources
```

Read-heavy applications can also use Read Replicas when supported.

### Result

**Successfully understood the basic approaches to scaling an RDS database.**

---

## 26. RDS Storage

### Explanation

RDS databases use managed storage.

When creating an RDS database, storage type and allocated storage can be configured according to the selected database engine and requirements.

### Example

```text
RDS DB Instance
      |
      v
Managed Storage
      |
      +---- Database Data
      |
      +---- Database Files
```

### Result

**Successfully understood that RDS provides managed database storage as part of the DB instance configuration.**

---

## 27. RDS Practical Lab

### Explanation

In this practical lab, a MySQL RDS database is created inside a VPC and connected to an EC2 application server.

### Architecture

```text
                         Internet
                             |
                             v
                          EC2
                     Application Server
                             |
                             v
                      VPC Networking
                             |
                             v
                        RDS Security
                             |
                             v
                        MySQL RDS
```

### Practical Steps

### Step 1 - Create VPC

Use:

```text
VPC:
AWS-Lab-VPC

CIDR:
10.0.0.0/16
```

### Step 2 - Create Database Subnets

Create appropriate subnets in multiple Availability Zones.

Example:

```text
DB-Subnet-A
10.0.10.0/24

DB-Subnet-B
10.0.11.0/24
```

### Step 3 - Create DB Subnet Group

Create:

```text
Name:
AWS-RDS-Subnet-Group
```

Select:

```text
VPC:
AWS-Lab-VPC
```

Add the database subnets.

### Step 4 - Create RDS Security Group

Create:

```text
Security Group:
AWS-RDS-SG
```

For MySQL, configure the required inbound rule:

```text
Type:
MySQL/Aurora

Protocol:
TCP

Port:
3306

Source:
Application Security Group
```

Do not expose the database unnecessarily to the internet.

### Step 5 - Create RDS Database

Open:

```text
RDS
   |
   v
Databases
   |
   v
Create database
```

Select:

```text
Engine:
MySQL
```

Configure:

```text
DB Identifier:
aws-lab-rds
```

Configure the required credentials.

### Step 6 - Configure Networking

Select:

```text
VPC:
AWS-Lab-VPC

DB Subnet Group:
AWS-RDS-Subnet-Group

Security Group:
AWS-RDS-SG
```

Keep public access disabled when the database should remain private.

### Step 7 - Configure Database Port

For MySQL:

```text
Port:
3306
```

### Step 8 - Create Database

Review the configuration.

Click:

```text
Create database
```

Wait until:

```text
Status:
Available
```

### Step 9 - Obtain RDS Endpoint

Open the database details.

Find:

```text
Endpoint
```

Example:

```text
aws-lab-rds.xxxxxxxxx.region.rds.amazonaws.com
```

### Step 10 - Connect from EC2

From the application server, use an appropriate MySQL client.

Example:

```bash
mysql -h <RDS-ENDPOINT> -P 3306 -u <USERNAME> -p
```

Enter the database password when prompted.

### Step 11 - Verify Connection

After successful authentication:

```sql
SHOW DATABASES;
```

Create a test database if required:

```sql
CREATE DATABASE aws_lab;
```

Select it:

```sql
USE aws_lab;
```

Create a test table:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Insert test data:

```sql
INSERT INTO users VALUES (1, 'AWS-Lab-User');
```

Check the data:

```sql
SELECT * FROM users;
```

### Result

**Successfully created a MySQL RDS database, configured its VPC and Security Group, obtained the RDS endpoint, connected from an EC2 application server, and performed basic SQL operations.**

---

## 28. RDS Connection Troubleshooting

### Explanation

If an EC2 instance cannot connect to RDS, check the complete network and database configuration.

Important items include:

- RDS status
- RDS endpoint
- Database port
- VPC
- DB subnet group
- Security Group
- EC2 Security Group
- Network ACL
- Route configuration
- Database credentials
- Database engine
- Database client

### Troubleshooting Flow

```text
EC2 Cannot Connect to RDS
          |
          v
Check RDS Status
          |
          v
Check RDS Endpoint
          |
          v
Check Database Port
          |
          v
Check VPC
          |
          v
Check DB Subnet Group
          |
          v
Check RDS Security Group
          |
          v
Check EC2 Security Group
          |
          v
Check Network ACL
          |
          v
Check Credentials
          |
          v
Test Connection Again
```

### Result

**Successfully understood the basic troubleshooting process for EC2-to-RDS connectivity problems.**

---

## 29. RDS Security Best Practices

### Explanation

RDS databases contain potentially sensitive application data and should be protected using appropriate security controls.

Important practices include:

- Keep databases private when public access is not required.
- Do not allow database ports from the entire internet unnecessarily.
- Allow database access from trusted application Security Groups.
- Use strong database credentials.
- Protect database credentials using appropriate secrets-management solutions.
- Enable encryption when required.
- Enable automated backups.
- Take manual snapshots when required.
- Use Multi-AZ for high availability requirements.
- Monitor database activity and performance.
- Apply appropriate maintenance and patching configurations.
- Follow the Principle of Least Privilege.
- Delete unused databases and snapshots when no longer required.

### Example

```text
Internet
    |
    v
Load Balancer
    |
    v
Application
    |
    v
Private RDS
    |
    v
Database
```

### Result

**Successfully understood important security practices for protecting Amazon RDS databases.**

---

## 30. RDS Architecture

```text
                              Internet
                                  |
                                  v
                           Load Balancer
                                  |
                                  v
                        Application Servers
                                  |
                                  v
                              VPC
                                  |
                    +-------------+-------------+
                    |                           |
                    v                           v
             Availability Zone A        Availability Zone B
                    |                           |
                    v                           v
             Private Subnet A            Private Subnet B
                    |                           |
                    +-------------+-------------+
                                  |
                                  v
                           DB Subnet Group
                                  |
                                  v
                               RDS
                                  |
                       +----------+----------+
                       |                     |
                       v                     v
                    Primary              Standby
                    Database             Database
```

---

## 31. RDS High Availability Architecture

```text
                         Application
                              |
                              v
                         RDS Primary
                              |
                    Automatic Failover
                              |
                              v
                         RDS Standby
```

Multi-AZ deployments are designed for high availability and failover.

### Result

**Successfully understood the basic architecture of a highly available RDS deployment.**

---

## 32. RDS Backup and Recovery Workflow

```text
RDS Database
     |
     +---- Automated Backup
     |
     +---- Manual Snapshot
     |
     v
Recovery
     |
     v
Restore Database
     |
     v
New RDS Instance
```

### Practical Steps

1. Create an RDS database.
2. Configure automated backups.
3. Verify the backup retention configuration.
4. Create a manual snapshot.
5. Verify the snapshot.
6. Restore the snapshot when required.
7. Verify the restored database.
8. Test application connectivity.

### Result

**Successfully understood the basic RDS backup and recovery workflow.**

---

## 33. RDS vs EC2 Database

### Explanation

A database can be installed manually on an EC2 instance, but RDS provides a managed database service.

### EC2 Database

```text
EC2
 |
 +---- OS Management
 |
 +---- Database Installation
 |
 +---- Patching
 |
 +---- Backups
 |
 +---- Monitoring
 |
 +---- Maintenance
```

### RDS

```text
RDS
 |
 +---- Managed Database
 |
 +---- Automated Backups
 |
 +---- Maintenance
 |
 +---- Monitoring
 |
 +---- High Availability Options
```

### Comparison

| Feature | Database on EC2 | Amazon RDS |
|---|---|---|
| Database Management | User Managed | AWS Managed Service |
| OS Management | User Managed | AWS Managed |
| Backups | User Configured | Managed Options |
| Patching | User Managed | Managed Options |
| Scaling | User Managed | Managed Options |
| High Availability | User Designed | Managed Options |

### Result

**Successfully understood the difference between managing a database manually on EC2 and using Amazon RDS as a managed database service.**

---

## 34. Complete RDS Workflow

### Workflow

```text
Create VPC
    |
    v
Create Database Subnets
    |
    v
Create DB Subnet Group
    |
    v
Create RDS Security Group
    |
    v
Create RDS Database
    |
    v
Select Database Engine
    |
    v
Configure Storage
    |
    v
Configure Networking
    |
    v
Configure Backups
    |
    v
Configure Monitoring
    |
    v
Database Available
    |
    v
Obtain RDS Endpoint
    |
    v
Connect Application
    |
    v
Monitor Database
    |
    v
Backup / Snapshot
    |
    v
Maintain / Scale
```

### Practical Steps

1. Create or select a VPC.
2. Create database subnets.
3. Create a DB subnet group.
4. Create an RDS Security Group.
5. Allow database traffic only from trusted sources.
6. Create the RDS database.
7. Select the database engine.
8. Configure the DB instance.
9. Configure storage.
10. Configure networking.
11. Configure database credentials.
12. Configure backups.
13. Configure monitoring.
14. Create the database.
15. Wait for the database status to become available.
16. Obtain the RDS endpoint.
17. Connect from the application server.
18. Test database operations.
19. Monitor database performance.
20. Create snapshots when required.
21. Test backup and recovery procedures.
22. Configure Multi-AZ when high availability is required.
23. Use Read Replicas when read scaling is required.
24. Review Security Group and network configuration.
25. Delete unused resources after completing the lab.

### Final Result

**Successfully completed Lab 14 - Amazon RDS and understood how to create and manage a managed relational database in AWS. Learned about database engines, DB instances, VPCs, DB subnet groups, Security Groups, database endpoints, database ports, public and private database architecture, EC2-to-RDS connectivity, Multi-AZ deployments, Read Replicas, automated backups, manual snapshots, encryption, monitoring, maintenance, scaling, troubleshooting, and RDS security best practices.**
