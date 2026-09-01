# Lab 09 - Security Groups

## Objective

The objective of this lab is to understand **Amazon EC2 Security Groups** and practically learn how to create, configure, modify, and use Security Groups to control inbound and outbound network traffic.

This lab covers:

- Security Groups
- Inbound Rules
- Outbound Rules
- Ports
- Protocols
- Source and Destination
- Security Group Association
- EC2 and Security Groups
- SSH
- HTTP
- HTTPS
- Security Group vs Network ACL
- Stateful Nature
- Practical Security Group Configuration
- Security Best Practices
- Troubleshooting

---

## 1. What is a Security Group?

### Explanation

A **Security Group** acts as a virtual firewall for AWS resources such as EC2 instances.

Security Groups control network traffic based on rules.

A Security Group controls:

- Inbound traffic
- Outbound traffic

Security Groups are associated with network interfaces and can be attached to supported AWS resources.

### Example

```text
                    Internet
                        |
                        v
                 Security Group
                  /           \
                 /             \
        Inbound Rules      Outbound Rules
                 \             /
                  \           /
                        |
                        v
                   EC2 Instance
```

### Result

**Successfully understood that a Security Group acts as a virtual firewall to control network traffic to and from AWS resources.**

---

## 2. Security Group Components

### Explanation

A Security Group rule generally contains:

- Type
- Protocol
- Port
- Source for inbound rules
- Destination for outbound rules

Example:

```text
Type:
SSH

Protocol:
TCP

Port:
22

Source:
My IP
```

### Example

```text
Security Group
      |
      +---- Protocol
      |
      +---- Port
      |
      +---- Source / Destination
      |
      +---- Allow Rule
```

### Result

**Successfully understood the basic components used when configuring Security Group rules.**

---

## 3. Inbound Rules

### Explanation

**Inbound Rules** control traffic coming into a resource.

For an EC2 instance, inbound rules determine which incoming connections are allowed by the Security Group.

Common examples include:

```text
SSH     - Port 22
HTTP    - Port 80
HTTPS   - Port 443
RDP     - Port 3389
```

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

1. Open the **AWS Management Console**.
2. Search for **EC2**.
3. Open the **EC2** service.
4. Select **Security Groups** under **Network & Security**.
5. Select the required Security Group.
6. Open the **Inbound rules** tab.
7. Click **Edit inbound rules**.
8. Click **Add rule**.
9. Select the required rule type.
10. Select the required protocol and port.
11. Specify the source.
12. Review the rule.
13. Click **Save rules**.
14. Verify the inbound rule.

### Result

**Successfully configured an inbound Security Group rule and understood how incoming traffic is controlled.**

---

## 4. Outbound Rules

### Explanation

**Outbound Rules** control traffic leaving a resource.

They determine which destinations a resource can communicate with through the Security Group.

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
2. Select the **Outbound rules** tab.
3. Click **Edit outbound rules**.
4. Review the existing rules.
5. Add or modify a rule when required.
6. Select the protocol.
7. Select the port.
8. Specify the destination.
9. Click **Save rules**.
10. Verify the outbound configuration.

### Result

**Successfully reviewed and configured outbound Security Group rules.**

---

## 5. SSH Port 22

### Explanation

**SSH (Secure Shell)** commonly uses TCP port **22**.

SSH is used to remotely connect to Linux-based systems.

Example:

```text
SSH
Protocol:
TCP

Port:
22
```

### Security Recommendation

SSH access should normally be restricted to trusted source IP addresses rather than allowing access from everywhere.

### Practical Steps

1. Open the required Security Group.
2. Open **Inbound rules**.
3. Click **Edit inbound rules**.
4. Add a rule.
5. Select **SSH**.
6. Verify port:

```text
22
```

7. Select an appropriate source.
8. Save the rule.
9. Verify the rule.

### Result

**Successfully understood how Security Groups control SSH access to an EC2 instance.**

---

## 6. HTTP Port 80

### Explanation

**HTTP** commonly uses TCP port **80**.

It is used for normal web traffic.

Example:

```text
HTTP
Protocol:
TCP

Port:
80
```

### Practical Steps

1. Open the required Security Group.
2. Open **Inbound rules**.
3. Click **Edit inbound rules**.
4. Add a new rule.
5. Select **HTTP**.
6. Verify port:

```text
80
```

7. Select the appropriate source.
8. Save the rule.
9. Verify the rule.

### Result

**Successfully configured an HTTP Security Group rule and understood how web traffic can be allowed to an EC2 instance.**

---

## 7. HTTPS Port 443

### Explanation

**HTTPS** commonly uses TCP port **443**.

It is used for encrypted web traffic.

Example:

```text
HTTPS
Protocol:
TCP

Port:
443
```

### Practical Steps

1. Open the required Security Group.
2. Open **Inbound rules**.
3. Click **Edit inbound rules**.
4. Add a new rule.
5. Select **HTTPS**.
6. Verify port:

```text
443
```

7. Select the appropriate source.
8. Save the rule.
9. Verify the rule.

### Result

**Successfully configured an HTTPS Security Group rule and understood how secure web traffic can be allowed to an EC2 instance.**

---

## 8. RDP Port 3389

### Explanation

**RDP (Remote Desktop Protocol)** commonly uses TCP port **3389**.

It is commonly used to remotely access Windows instances.

Example:

```text
RDP
Protocol:
TCP

Port:
3389
```

### Security Recommendation

RDP access should be restricted to trusted source IP addresses whenever possible.

### Result

**Successfully understood how Security Groups can control RDP access to Windows EC2 instances.**

---

## 9. Source and Destination

### Explanation

For an **Inbound Rule**, the Security Group specifies where the incoming traffic is allowed from.

For an **Outbound Rule**, the Security Group specifies where the outgoing traffic is allowed to.

### Inbound Example

```text
Source:
My IP

Protocol:
TCP

Port:
22
```

### Outbound Example

```text
Destination:
0.0.0.0/0

Protocol:
All

Ports:
All
```

### Result

**Successfully understood the difference between the source of inbound traffic and the destination of outbound traffic.**

---

## 10. Security Group and EC2

### Explanation

A Security Group can be associated with an EC2 instance through its network interface.

When traffic reaches the instance, the Security Group rules determine whether the traffic is allowed.

### Architecture

```text
Internet
    |
    v
Security Group
    |
    v
EC2 Instance
```

### Practical Steps

1. Open the **EC2 Dashboard**.
2. Select **Instances**.
3. Select an EC2 instance.
4. Open the **Security** tab.
5. Locate the associated Security Group.
6. Click the Security Group.
7. Review the inbound rules.
8. Review the outbound rules.
9. Modify the rules if required.
10. Verify the Security Group association.

### Result

**Successfully verified the Security Group associated with an EC2 instance and reviewed its traffic rules.**

---

## 11. Creating a Security Group

### Explanation

A Security Group can be created for a specific application or group of resources.

Example:

```text
Security Group Name:
AWS-Lab-SG

Description:
Security Group for AWS Lab EC2
```

### Practical Steps

1. Open the **EC2** service.
2. Select **Security Groups**.
3. Click **Create security group**.
4. Enter the Security Group name.

```text
AWS-Lab-SG
```

5. Enter a description.

```text
Security Group for AWS Lab EC2
```

6. Select the required VPC.
7. Configure inbound rules.
8. Review outbound rules.
9. Click **Create security group**.
10. Verify that the Security Group has been created.

### Result

**Successfully created a Security Group for the AWS lab environment.**

---

## 12. Associating a Security Group with EC2

### Explanation

A Security Group can be associated with an EC2 instance during instance launch or after the instance has been created.

### Practical Steps

1. Open the **EC2 Dashboard**.
2. Select **Instances**.
3. Select the required EC2 instance.
4. Choose **Actions**.
5. Select the option to manage or change Security Groups.
6. Select the required Security Group.
7. Save the configuration.
8. Verify the Security Group association.

### Result

**Successfully associated a Security Group with an EC2 instance.**

---

## 13. Multiple Security Groups

### Explanation

An EC2 instance can have multiple Security Groups associated with it.

The effective permissions are based on the combined rules of the associated Security Groups.

Example:

```text
                    EC2 Instance
                         |
             +-----------+-----------+
             |                       |
             v                       v
       Web Security Group      Admin Security Group
             |                       |
             v                       v
         HTTP/HTTPS                  SSH
```

### Example

```text
Web-SG:
HTTP 80
HTTPS 443

Admin-SG:
SSH 22
```

### Result

**Successfully understood how multiple Security Groups can be associated with an EC2 instance for different access requirements.**

---

## 14. Security Group Stateful Nature

### Explanation

Security Groups are **stateful**.

When an inbound connection is allowed, the response traffic for that connection is automatically allowed back, regardless of outbound rules.

Similarly, allowed outbound connections can receive response traffic.

### Example

```text
Client
  |
  | Request
  v
Security Group
  |
  v
EC2
  |
  | Response
  v
Client
```

The response traffic is automatically permitted for the established connection.

### Result

**Successfully understood that Security Groups are stateful and automatically allow response traffic for permitted connections.**

---

## 15. Security Group vs Network ACL

### Explanation

Security Groups and Network ACLs are both used for network security, but they operate differently.

### Comparison

| Feature | Security Group | Network ACL |
|---|---|---|
| Level | Resource / Network Interface | Subnet |
| Stateful | Yes | No |
| Rules | Allow rules | Allow and Deny rules |
| Applied To | Network interfaces/resources | Subnets |
| Main Purpose | Resource-level traffic control | Subnet-level traffic control |

### Example

```text
VPC
 |
 v
Network ACL
 |
 v
Subnet
 |
 v
Security Group
 |
 v
EC2 Instance
```

### Result

**Successfully understood the difference between Security Groups and Network ACLs.**

---

## 16. Security Group Rule Example

### Example

Suppose an EC2 web server requires HTTP and HTTPS access.

```text
Security Group:
AWS-Web-SG

Inbound Rules:

HTTP
Protocol: TCP
Port: 80
Source: Appropriate Internet Source

HTTPS
Protocol: TCP
Port: 443
Source: Appropriate Internet Source
```

For administrative access:

```text
SSH
Protocol: TCP
Port: 22
Source: Trusted IP Address
```

### Result

**Successfully understood how to create Security Group rules according to application requirements.**

---

## 17. Principle of Least Privilege

### Explanation

The **Principle of Least Privilege** means allowing only the network traffic that is required.

For example, if a server only needs HTTPS:

```text
Allow:
HTTPS - 443
```

There is no need to open unnecessary ports.

### Example

```text
Required:
HTTPS 443

Not Required:
FTP 21
Telnet 23
Unused Application Ports
```

### Result

**Successfully understood how the Principle of Least Privilege can be applied to Security Group rules.**

---

## 18. Practical Lab - Configure Security Group

### Explanation

In this practical lab, a Security Group is created and configured for an EC2 web server.

### Practical Steps

### Step 1 - Open EC2

1. Sign in to AWS.
2. Search for **EC2**.
3. Open the EC2 service.
4. Select **Security Groups**.

### Step 2 - Create Security Group

Create:

```text
Security Group Name:
AWS-Web-SG

Description:
Security Group for Web Server
```

Select the required VPC.

### Step 3 - Configure SSH

Add:

```text
Type:
SSH

Protocol:
TCP

Port:
22

Source:
Trusted IP Address
```

Restrict SSH access to the required source.

### Step 4 - Configure HTTP

Add:

```text
Type:
HTTP

Protocol:
TCP

Port:
80

Source:
Required Source
```

### Step 5 - Configure HTTPS

Add:

```text
Type:
HTTPS

Protocol:
TCP

Port:
443

Source:
Required Source
```

### Step 6 - Review Outbound Rules

Review the outbound rules.

Configure them according to the application's requirements.

### Step 7 - Create Security Group

Click:

```text
Create security group
```

### Step 8 - Launch EC2

Launch an EC2 instance inside the required VPC and subnet.

Select:

```text
Security Group:
AWS-Web-SG
```

### Step 9 - Verify

Open the EC2 instance details.

Check:

```text
Security
   |
   v
Security Groups
   |
   v
AWS-Web-SG
```

### Result

**Successfully created and associated a Security Group with an EC2 instance and configured the required inbound and outbound traffic rules.**

---

## 19. Security Group Troubleshooting

### Explanation

If an EC2 instance cannot be accessed, the Security Group should be checked.

Important items include:

- Correct Security Group
- Correct inbound rule
- Correct port
- Correct protocol
- Correct source
- Correct outbound rule
- Correct EC2 instance
- Correct subnet
- Correct Route Table
- Internet Gateway
- Public IPv4 address

### Troubleshooting Flow

```text
Cannot Access EC2
       |
       v
Check Security Group
       |
       v
Check Inbound Rule
       |
       v
Check Port
       |
       v
Check Protocol
       |
       v
Check Source
       |
       v
Check Route Table
       |
       v
Check Internet Gateway
       |
       v
Check Public IP
       |
       v
Test Again
```

### Result

**Successfully understood the basic troubleshooting process for Security Group connectivity problems.**

---

## 20. Security Group Security Best Practices

### Explanation

Security Groups should be configured according to the minimum network access required.

Important practices include:

- Allow only required ports.
- Restrict SSH access.
- Restrict RDP access.
- Avoid unnecessary open ports.
- Use trusted IP addresses where possible.
- Use separate Security Groups for different application roles.
- Review Security Group rules regularly.
- Follow the Principle of Least Privilege.
- Remove unused rules.
- Remove unused Security Groups when they are no longer required.

### Example

```text
Internet
   |
   v
Security Group
   |
   +---- HTTPS 443
   |
   v
Web Server
   |
   v
Application Server
   |
   v
Database
```

### Result

**Successfully understood Security Group security best practices and the importance of restricting unnecessary network access.**

---

## 21. Complete Security Group Architecture

```text
                              Internet
                                  |
                                  v
                         Internet Gateway
                                  |
                                  v
                            Public Subnet
                                  |
                                  v
                         Security Group
                       +----------------+
                       | HTTP : 80      |
                       | HTTPS : 443    |
                       | SSH : 22       |
                       +----------------+
                                  |
                                  v
                            EC2 Web Server
```

---

## 22. Security Group Traffic Flow

### Inbound Traffic

```text
Client
   |
   v
Internet Gateway
   |
   v
Public Subnet
   |
   v
Security Group
   |
   | Allowed by inbound rule
   v
EC2 Instance
```

### Outbound Traffic

```text
EC2 Instance
   |
   v
Security Group
   |
   | Allowed by outbound rule
   v
Route Table
   |
   v
Internet Gateway
   |
   v
Internet
```

### Result

**Successfully understood how inbound and outbound traffic flows through a Security Group.**

---

## 23. Complete Security Group Workflow

### Workflow

```text
Create VPC
    |
    v
Create Subnet
    |
    v
Create Security Group
    |
    v
Configure Inbound Rules
    |
    v
Configure Outbound Rules
    |
    v
Launch EC2
    |
    v
Associate Security Group
    |
    v
Verify Ports
    |
    v
Test Connectivity
    |
    v
Monitor and Review
```

### Practical Steps

1. Create or select a VPC.
2. Create or select a subnet.
3. Create a Security Group.
4. Select the VPC.
5. Configure inbound rules.
6. Configure outbound rules.
7. Launch an EC2 instance.
8. Associate the Security Group.
9. Verify the Security Group rules.
10. Verify the Route Table.
11. Verify the Internet Gateway when internet access is required.
12. Verify the public IP when public access is required.
13. Test the required connectivity.
14. Review the Security Group configuration.
15. Remove unnecessary rules after completing the lab.

### Final Result

**Successfully completed Lab 09 - Security Groups and understood how Security Groups act as virtual firewalls for AWS resources. Learned how to create Security Groups, configure inbound and outbound rules, manage ports and protocols, control SSH, HTTP, HTTPS, and RDP access, associate Security Groups with EC2 instances, understand stateful behavior, compare Security Groups with Network ACLs, troubleshoot connectivity, and apply the Principle of Least Privilege and Security Group security best practices.**
