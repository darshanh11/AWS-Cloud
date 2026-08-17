# Lab 03 - Amazon EC2

## Objective

The objective of this lab is to understand **Amazon Elastic Compute Cloud (EC2)** and learn how to launch, configure, connect to, manage, monitor, and terminate virtual servers in the AWS Cloud.

---

## 1. What is Amazon EC2?

### Explanation

**Amazon Elastic Compute Cloud (EC2)** is an AWS service that provides resizable virtual servers in the cloud.

These virtual servers are called **EC2 Instances**.

EC2 allows users to run applications, websites, development environments, databases, and other workloads without purchasing and maintaining physical servers.

EC2 provides control over:

- Operating System
- CPU
- Memory
- Storage
- Networking
- Security
- Instance configuration

### Example

```text
                         AWS Cloud
                             |
                             v
                           Amazon EC2
                             |
              +--------------+--------------+
              |              |              |
             CPU            RAM          Storage
              |              |              |
              +--------------+--------------+
                             |
                             v
                      Operating System
                             |
                             v
                       Applications
```

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **EC2**.
3. Open the **EC2** service.
4. Open the **EC2 Dashboard**.
5. Explore the available EC2 features.
6. Review **Instances**, **AMIs**, **Instance Types**, **Key Pairs**, **Security Groups**, and **Elastic IPs**.

### Result

**Successfully opened Amazon EC2 and understood how EC2 provides virtual computing resources in the AWS Cloud.**

---

## 2. EC2 Instance

### Explanation

An **EC2 Instance** is a virtual server running in the AWS Cloud.

An EC2 instance provides computing resources such as:

- CPU
- Memory
- Storage
- Network connectivity
- Operating System

An instance can be launched with different configurations depending on the workload.

### Example

```text
                     EC2 Instance
                          |
          +---------------+---------------+
          |               |               |
         CPU             RAM           Storage
          |               |               |
          +---------------+---------------+
                          |
                          v
                   Operating System
                          |
                          v
                    Applications
```

### Practical Steps

1. Open the **EC2 Dashboard**.
2. Select **Instances**.
3. Click **Launch instances**.
4. Enter an instance name.
5. Select an operating system image.
6. Select an instance type.
7. Select or create a key pair.
8. Configure network settings.
9. Configure storage.
10. Review the configuration.
11. Click **Launch instance**.
12. Wait for the instance to start.
13. Verify that the instance appears in the **Instances** list.

### Result

**Successfully launched an EC2 instance and verified that the instance was available in the EC2 console.**

---

## 3. Amazon Machine Image (AMI)

### Explanation

An **Amazon Machine Image (AMI)** is a template used to create an EC2 instance.

An AMI contains the information required to launch an instance, such as the operating system and software configuration.

Common operating system choices include:

- Amazon Linux
- Ubuntu
- Windows Server
- Red Hat Enterprise Linux

### Example

```text
                    AMI
                     |
       +-------------+-------------+
       |             |             |
  Operating      Software     Configuration
    System
       |
       v
  EC2 Instance
```

### Practical Steps

1. Open **EC2**.
2. Click **Launch instance**.
3. Locate **Application and OS Images (AMI)**.
4. Review the available AMIs.
5. Select the required operating system.
6. Review the AMI details.
7. Continue with the EC2 configuration.

### Result

**Successfully explored AMIs and understood how AMIs are used as templates for launching EC2 instances.**

---

## 4. EC2 Instance Types

### Explanation

An **EC2 Instance Type** defines the computing resources available to an EC2 instance.

Different instance types provide different combinations of:

- vCPUs
- Memory
- Network performance
- Storage capabilities

Instance types are selected according to the workload requirements.

Common categories include:

- General purpose
- Compute optimized
- Memory optimized
- Storage optimized
- Accelerated computing

### Example

```text
Workload
   |
   +---- General Purpose
   |
   +---- Compute Optimized
   |
   +---- Memory Optimized
   |
   +---- Storage Optimized
   |
   +---- Accelerated Computing
```

### Practical Steps

1. Open the EC2 launch instance page.
2. Locate the **Instance type** section.
3. Review the available instance types.
4. Compare the CPU and memory specifications.
5. Review the pricing information.
6. Select an appropriate instance type.
7. Continue with the instance configuration.

### Result

**Successfully explored EC2 instance types and understood how instance types determine the computing capacity of an EC2 instance.**

---

## 5. EC2 Key Pair

### Explanation

An **EC2 Key Pair** is used to securely connect to an EC2 instance.

A key pair consists of:

- Public Key
- Private Key

The public key is associated with the EC2 instance, while the private key is kept securely by the user.

Key pairs are commonly used for secure access to Linux EC2 instances.

### Example

```text
                    Key Pair
                       |
              +--------+--------+
              |                 |
         Public Key        Private Key
              |                 |
              v                 v
        EC2 Instance       User Computer
              |                 |
              +--------+--------+
                       |
                       v
                Secure Connection
```

### Practical Steps

1. Open **EC2**.
2. Select **Key pairs**.
3. Click **Create key pair**.
4. Enter a key pair name.
5. Select the required private key format.
6. Click **Create key pair**.
7. Download the private key file.
8. Store the private key securely.
9. Select the key pair while launching an EC2 instance.
10. Use the private key when connecting to the instance.

### Security

**Never upload the private key to GitHub or share it publicly.**

### Result

**Successfully created an EC2 Key Pair and understood how it is used for secure access to EC2 instances.**

---

## 6. EC2 Security Groups

### Explanation

A **Security Group** acts as a virtual firewall for an EC2 instance.

Security Groups control network traffic going into and out of an EC2 instance.

Security Groups contain:

- Inbound Rules
- Outbound Rules

### Example

```text
                         Internet
                            |
                            v
                     Security Group
                            |
              +-------------+-------------+
              |                           |
        Inbound Rules                Outbound Rules
              |                           |
              v                           v
        EC2 Instance <--------------------+
```

### Practical Steps

1. Open **EC2**.
2. Select **Security Groups**.
3. Click **Create security group**.
4. Enter a security group name.
5. Enter a description.
6. Configure inbound rules.
7. Configure outbound rules.
8. Review the configuration.
9. Create the Security Group.
10. Attach the Security Group to the EC2 instance if required.
11. Verify the configured rules.

### Result

**Successfully created and configured a Security Group and understood how it controls network traffic for an EC2 instance.**

---

## 7. Inbound Rules

### Explanation

**Inbound Rules** control traffic coming into an EC2 instance.

Common inbound ports include:

| Protocol | Port | Purpose |
|---|---:|---|
| SSH | 22 | Linux remote access |
| RDP | 3389 | Windows remote access |
| HTTP | 80 | Web traffic |
| HTTPS | 443 | Secure web traffic |

Inbound rules determine which traffic is allowed to reach the EC2 instance.

### Example

```text
Internet
   |
   v
Security Group
   |
   +---- SSH : 22
   +---- HTTP : 80
   +---- HTTPS : 443
   |
   v
EC2 Instance
```

### Practical Steps

1. Open the required Security Group.
2. Select **Inbound rules**.
3. Click **Edit inbound rules**.
4. Select the required protocol.
5. Select the required port.
6. Specify the allowed source.
7. Review the rule.
8. Save the inbound rules.
9. Verify the configured rules.

### Result

**Successfully configured inbound rules and understood how incoming network traffic is controlled for an EC2 instance.**

---

## 8. Outbound Rules

### Explanation

**Outbound Rules** control traffic leaving an EC2 instance.

These rules determine where the EC2 instance can send network traffic.

### Example

```text
EC2 Instance
      |
      v
Security Group
      |
      v
Outbound Rules
      |
      v
Internet / AWS Resources
```

### Practical Steps

1. Open the required Security Group.
2. Select **Outbound rules**.
3. Click **Edit outbound rules**.
4. Review the configured protocols.
5. Review the configured ports.
6. Review the destinations.
7. Modify the rules if required.
8. Save the outbound rules.
9. Verify the configuration.

### Result

**Successfully reviewed outbound rules and understood how outgoing network traffic from an EC2 instance is controlled.**

---

## 9. VPC and Subnet

### Explanation

An EC2 instance runs inside an **Amazon Virtual Private Cloud (VPC)**.

A VPC provides an isolated network environment for AWS resources.

A **Subnet** is a range of IP addresses inside a VPC where AWS resources such as EC2 instances can be placed.

### Example

```text
                         VPC
                          |
             +------------+------------+
             |                         |
        Public Subnet             Private Subnet
             |                         |
             v                         v
        EC2 Instance              AWS Resources
```

### Practical Steps

1. Open the **EC2** launch instance page.
2. Locate the **Network settings** section.
3. Select the required VPC.
4. Select the required subnet.
5. Configure the public IP setting if required.
6. Select or create a Security Group.
7. Review the network configuration.
8. Continue with the EC2 launch.

### Result

**Successfully understood how VPCs and subnets provide the network environment for EC2 instances.**

---

## 10. Public and Private IP Addresses

### Explanation

An EC2 instance can have private and public network addressing depending on its network configuration.

A **Private IP address** is used for communication within the VPC.

A **Public IP address** can provide internet connectivity when the network configuration supports it.

### Example

```text
                    Internet
                       |
                       v
                  Public IP
                       |
                       v
                 EC2 Instance
                       |
                       v
                  Private IP
                       |
                       v
                     VPC
```

### Practical Steps

1. Launch or select an EC2 instance.
2. Open the instance details.
3. Locate the **Networking** section.
4. Review the Private IPv4 address.
5. Review the Public IPv4 address if assigned.
6. Understand how the addresses are used.
7. Verify the network configuration.

### Result

**Successfully understood the difference between public and private IP addresses associated with EC2 networking.**

---

## 11. Elastic IP Address

### Explanation

An **Elastic IP address** is a static public IPv4 address that can be associated with an EC2 instance.

It can be useful when an application requires a consistent public IP address.

### Example

```text
Internet
    |
    v
Elastic IP
    |
    v
EC2 Instance
```

### Practical Steps

1. Open **EC2**.
2. Select **Elastic IPs**.
3. Click **Allocate Elastic IP address**.
4. Review the allocation settings.
5. Allocate the Elastic IP.
6. Select the allocated IP address.
7. Choose **Associate Elastic IP address**.
8. Select the EC2 instance.
9. Associate the Elastic IP.
10. Verify the public IP configuration.

### Result

**Successfully allocated and understood how an Elastic IP address can provide a consistent public IPv4 address for an EC2 instance.**

---

## 12. EC2 Storage

### Explanation

EC2 instances use storage to store:

- Operating system files
- Applications
- Configuration files
- User data
- Application data

The primary persistent block storage service used with EC2 is **Amazon Elastic Block Store (EBS)**.

### Example

```text
                  EC2 Instance
                       |
                       v
                    EBS Volume
                       |
            +----------+----------+
            |          |          |
           OS      Applications   Data
```

### Practical Steps

1. Open **EC2**.
2. Select the required instance.
3. Open the **Storage** section.
4. Review the attached EBS volumes.
5. Review the volume size.
6. Review the volume type.
7. Add or modify storage when required.
8. Verify the attached storage.

### Result

**Successfully explored EC2 storage and understood how EBS provides persistent block storage for EC2 instances.**

---

## 13. Amazon EBS

### Explanation

**Amazon Elastic Block Store (EBS)** provides persistent block storage for EC2 instances.

EBS volumes can be used to store operating systems, applications, and data.

EBS volumes remain separate from the compute instance and can be managed independently.

### Example

```text
EC2 Instance
     |
     v
EBS Volume
     |
     +---- Operating System
     +---- Applications
     +---- Data
```

### Practical Steps

1. Open **EC2**.
2. Select **Volumes** under Elastic Block Store.
3. Click **Create volume**.
4. Select the required volume type.
5. Specify the required volume size.
6. Select the Availability Zone.
7. Create the volume.
8. Select the volume.
9. Choose **Attach volume**.
10. Select the EC2 instance.
11. Attach the volume.
12. Verify that the volume is attached.

### Result

**Successfully created and understood how an EBS volume provides persistent storage for an EC2 instance.**

---

## 14. EC2 Instance Connect

### Explanation

**EC2 Instance Connect** provides a way to connect to supported EC2 instances through the AWS Management Console or other supported methods.

It can be used to access a Linux instance without manually managing a persistent SSH key in some configurations.

### Practical Steps

1. Open **EC2**.
2. Select a supported Linux EC2 instance.
3. Click **Connect**.
4. Select **EC2 Instance Connect**.
5. Select the required connection options.
6. Click **Connect**.
7. Wait for the terminal session to open.
8. Verify that the EC2 instance can be accessed.

### Result

**Successfully understood how EC2 Instance Connect can be used to access a supported EC2 instance.**

---

## 15. Connect to a Linux EC2 Instance Using SSH

### Explanation

**SSH (Secure Shell)** is commonly used to remotely connect to Linux EC2 instances.

SSH commonly uses **port 22**.

A private key is normally used for authentication.

### Example

```text
Local Computer
      |
      | SSH
      v
Port 22
      |
      v
Linux EC2 Instance
```

### Practical Steps

1. Launch a Linux EC2 instance.
2. Ensure the instance is in the **Running** state.
3. Verify that the Security Group allows SSH traffic on port **22** from the appropriate source.
4. Open the EC2 instance.
5. Click **Connect**.
6. Select the appropriate connection method.
7. Follow the connection instructions provided by AWS.
8. Use the required private key.
9. Establish the SSH connection.
10. Verify that the Linux terminal is accessible.

### Result

**Successfully understood how SSH can be used to securely connect to a Linux EC2 instance.**

---

## 16. Connect to a Windows EC2 Instance Using RDP

### Explanation

**Remote Desktop Protocol (RDP)** is commonly used to remotely connect to Windows EC2 instances.

RDP commonly uses **port 3389**.

### Example

```text
Local Computer
      |
      | RDP
      v
Port 3389
      |
      v
Windows EC2 Instance
```

### Practical Steps

1. Launch a Windows EC2 instance.
2. Ensure the instance is in the **Running** state.
3. Verify that the Security Group allows RDP traffic on port **3389** from the appropriate source.
4. Select the Windows EC2 instance.
5. Click **Connect**.
6. Select **RDP client**.
7. Obtain the required connection information.
8. Retrieve the Windows administrator credentials using the appropriate AWS process.
9. Open the Remote Desktop client.
10. Enter the required connection details.
11. Enter the required credentials.
12. Connect to the Windows instance.
13. Verify that the Windows desktop is accessible.

### Result

**Successfully understood how RDP can be used to remotely connect to a Windows EC2 instance.**

---

## 17. EC2 Instance States

### Explanation

An EC2 instance can have different states during its lifecycle.

Common instance states include:

- Pending
- Running
- Stopping
- Stopped
- Shutting-down
- Terminated

### Example

```text
Pending
   |
   v
Running
   |
   +----> Stopping ----> Stopped
   |
   +----> Shutting-down ----> Terminated
```

### Practical Steps

1. Open **EC2**.
2. Select **Instances**.
3. Select an EC2 instance.
4. Review the current instance state.
5. Start the instance if it is stopped.
6. Stop the instance if it is running and no longer required.
7. Review the state changes.
8. Terminate the instance only when it is no longer required.

### Result

**Successfully understood the different EC2 instance states and the basic EC2 instance lifecycle.**

---

## 18. Start an EC2 Instance

### Explanation

Starting an EC2 instance changes its state from **Stopped** to **Running**.

A running instance can process workloads and accept network connections according to its configuration.

### Practical Steps

1. Open **EC2**.
2. Select **Instances**.
3. Select the stopped EC2 instance.
4. Choose **Instance state**.
5. Select **Start instance**.
6. Wait for the instance to start.
7. Monitor the instance state.
8. Verify that the instance state changes to **Running**.

### Result

**Successfully started an EC2 instance and verified that it reached the Running state.**

---

## 19. Stop an EC2 Instance

### Explanation

Stopping an EC2 instance shuts down the compute instance while preserving the instance configuration and attached EBS storage, subject to the applicable configuration and AWS charges.

Stopping an instance can help reduce compute costs when the instance is not required.

### Practical Steps

1. Open **EC2**.
2. Select **Instances**.
3. Select the running EC2 instance.
4. Choose **Instance state**.
5. Select **Stop instance**.
6. Confirm the operation.
7. Wait for the instance to stop.
8. Verify that the instance state changes to **Stopped**.

### Result

**Successfully stopped an EC2 instance and verified that it reached the Stopped state.**

---

## 20. Reboot an EC2 Instance

### Explanation

Rebooting an EC2 instance restarts the operating system while keeping the instance available as the same EC2 resource.

A reboot can be useful when troubleshooting operating system or application issues.

### Practical Steps

1. Open **EC2**.
2. Select **Instances**.
3. Select the required running instance.
4. Choose **Instance state**.
5. Select **Reboot instance**.
6. Confirm the operation.
7. Wait for the instance to become available again.
8. Verify that the instance returns to the **Running** state.

### Result

**Successfully understood and performed an EC2 instance reboot operation.**

---

## 21. Terminate an EC2 Instance

### Explanation

**Termination** permanently removes an EC2 instance.

Termination should only be performed when the instance is no longer required.

Important data should be backed up before termination.

### Practical Steps

1. Open **EC2**.
2. Select **Instances**.
3. Select the EC2 instance that is no longer required.
4. Review the instance details.
5. Confirm that important data has been backed up.
6. Choose **Instance state**.
7. Select **Terminate instance**.
8. Confirm the termination.
9. Wait for the instance state to change to **Terminated**.
10. Verify the instance status.

### Result

**Successfully understood the EC2 termination process and the importance of confirming that an instance and its required data are no longer needed before termination.**

---

## 22. EC2 User Data

### Explanation

**EC2 User Data** allows commands or scripts to run automatically when an EC2 instance is launched.

It can be used for:

- Initial configuration
- Software installation
- Service configuration
- Automation

### Example

```bash
#!/bin/bash
apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
```

### Practical Steps

1. Open **EC2**.
2. Click **Launch instance**.
3. Select the required AMI.
4. Select the instance type.
5. Configure the key pair.
6. Configure the network settings.
7. Open **Advanced details**.
8. Locate **User data**.
9. Enter the required startup script.
10. Complete the EC2 configuration.
11. Launch the instance.
12. Wait for the instance to start.
13. Verify that the User Data script was executed.

### Result

**Successfully understood how EC2 User Data can automate initial instance configuration and software installation.**

---

## 23. EC2 Monitoring

### Explanation

EC2 provides monitoring information that can be used to observe instance performance and health.

Common monitoring information includes:

- CPU utilization
- Network traffic
- Disk activity
- Instance status
- System status

**Amazon CloudWatch** can be used for detailed monitoring, metrics, alarms, and operational visibility.

### Example

```text
EC2 Instance
      |
      v
CloudWatch
      |
      +---- CPU Utilization
      +---- Network Traffic
      +---- Status
      +---- Metrics
      +---- Alarms
```

### Practical Steps

1. Open **EC2**.
2. Select an EC2 instance.
3. Open the **Monitoring** section.
4. Review the available metrics.
5. Check CPU utilization.
6. Review network-related metrics.
7. Review instance status information.
8. Open CloudWatch when detailed monitoring is required.
9. Review the available EC2 metrics.

### Result

**Successfully explored EC2 monitoring and understood how instance performance and health can be monitored using AWS monitoring services.**

---

## 24. EC2 Instance Metadata

### Explanation

**EC2 Instance Metadata** provides information about a running EC2 instance.

It can provide information such as:

- Instance ID
- Private IP address
- Instance type
- Network information
- IAM role information when configured

Instance metadata is available from within the EC2 instance.

### Example

```text
EC2 Instance
      |
      v
Instance Metadata
      |
      +---- Instance ID
      +---- Instance Type
      +---- Private IP
      +---- Network Information
```

### Practical Steps

1. Launch an EC2 instance.
2. Connect to the instance.
3. Access the supported instance metadata endpoint from inside the instance.
4. Request the required metadata.
5. Review the returned instance information.
6. Use metadata only when required by the application or administration task.

### Result

**Successfully understood the purpose of EC2 Instance Metadata and the type of information it can provide about an EC2 instance.**

---

## 25. EC2 Auto Recovery and Status Checks

### Explanation

EC2 performs status checks to monitor the health of an instance and its underlying infrastructure.

Common status checks include:

- System status checks
- Instance status checks

Status checks help identify problems that may affect an EC2 instance.

### Practical Steps

1. Open **EC2**.
2. Select the required instance.
3. Review the **Status checks** section.
4. Check the system status.
5. Check the instance status.
6. Investigate any failed status checks.
7. Follow AWS recommended recovery or troubleshooting procedures when required.

### Result

**Successfully understood EC2 status checks and how they can help identify instance and infrastructure problems.**

---

## 26. EC2 Pricing and Cost Awareness

### Explanation

EC2 costs can depend on several factors, including:

- Instance type
- Running time
- Operating system
- Storage
- Data transfer
- Additional AWS services

Unused resources should be stopped or terminated when they are no longer required, depending on the resource and workload requirements.

### Practical Steps

1. Select an appropriate EC2 instance type.
2. Review the pricing information before launching.
3. Use only the resources required for the lab.
4. Monitor the running resources.
5. Stop instances when they are not required.
6. Terminate resources that are no longer needed.
7. Review **AWS Billing and Cost Management**.
8. Monitor the estimated or actual usage where applicable.

### Result

**Successfully understood the basic cost factors associated with EC2 and learned the importance of managing unused resources.**

---

## 27. EC2 Architecture

### Explanation

An EC2 environment consists of several AWS components that work together to provide secure and scalable computing.

These components can include:

- VPC
- Subnet
- Security Group
- AMI
- EC2 Instance
- EBS
- Key Pair
- Public or Private IP
- CloudWatch

### Architecture

```text
                         AWS Cloud
                             |
                             v
                           VPC
                             |
                    +--------+--------+
                    |                 |
                Public Subnet      Private Subnet
                    |                 |
                    v                 v
              Security Group     AWS Resources
                    |
                    v
              EC2 Instance
                    |
        +-----------+-----------+
        |           |           |
       AMI         EBS       Key Pair
        |           |           |
        v           v           v
   Operating     Storage    Secure Access
    System
                    |
                    v
                CloudWatch
                 Monitoring
```

### Practical Steps

1. Create or select a VPC.
2. Select a subnet.
3. Configure the Security Group.
4. Select an AMI.
5. Select an instance type.
6. Configure the key pair.
7. Configure storage.
8. Configure networking.
9. Launch the EC2 instance.
10. Connect to the instance.
11. Monitor the instance.
12. Stop or terminate the instance when the lab is complete.

### Result

**Successfully understood the basic architecture of an EC2 environment and how compute, networking, security, storage, access, and monitoring components work together.**

---

## 28. EC2 Security Best Practices

### Explanation

EC2 instances should be configured securely to reduce the risk of unauthorized access.

Important security practices include:

- Use Security Groups carefully.
- Allow only required ports.
- Restrict SSH access.
- Restrict RDP access.
- Use strong authentication.
- Protect private keys.
- Use IAM Roles where appropriate.
- Keep operating systems updated.
- Monitor EC2 instances.
- Stop or terminate unused resources.

### Practical Steps

1. Review the Security Group.
2. Remove unnecessary inbound ports.
3. Restrict SSH access to trusted sources.
4. Restrict RDP access to trusted sources.
5. Protect the EC2 private key.
6. Use IAM Roles instead of storing long-term AWS credentials on instances when appropriate.
7. Keep the operating system updated.
8. Monitor instance activity.
9. Review EC2 permissions and network configuration.
10. Remove unused resources.

### Result

**Successfully reviewed EC2 security best practices and understood how to improve the security of EC2 instances.**

---

## 29. Complete EC2 Workflow

### Explanation

The complete EC2 workflow includes selecting an AMI, choosing an instance type, configuring security and networking, configuring storage and authentication, launching the instance, connecting to it, monitoring it, and managing its lifecycle.

### Workflow

```text
                    Select AMI
                        |
                        v
                 Select Instance Type
                        |
                        v
                  Create Key Pair
                        |
                        v
               Configure Network
                        |
                        v
              Configure Security Group
                        |
                        v
                Configure Storage
                        |
                        v
                 Launch Instance
                        |
                        v
                  EC2 Running
                        |
             +----------+----------+
             |                     |
             v                     v
         Connect                 Monitor
             |                     |
             +----------+----------+
                        |
                        v
                 Stop / Reboot
                        |
                        v
                    Terminate
```

### Practical Steps

1. Open the **EC2 Dashboard**.
2. Select **Launch instance**.
3. Choose an **AMI**.
4. Select an **Instance Type**.
5. Configure the **Key Pair**.
6. Configure the **VPC and Subnet**.
7. Configure the **Security Group**.
8. Configure **Storage**.
9. Review the configuration.
10. Launch the EC2 instance.
11. Verify the instance state.
12. Connect to the instance.
13. Perform the required workload or configuration.
14. Monitor the instance.
15. Stop the instance when it is temporarily not required.
16. Terminate the instance when the lab resources are no longer required.

### Result

**Successfully understood the complete EC2 workflow from instance creation and configuration to connection, monitoring, lifecycle management, and termination.**
