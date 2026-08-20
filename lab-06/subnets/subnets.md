# Lab 06 - Amazon VPC Subnets

## Objective

The objective of this lab is to understand **Amazon VPC Subnets** and practically learn how to create, configure, and manage public and private subnets inside an AWS VPC.

This lab covers:

- What is a Subnet
- Subnet CIDR
- Public Subnet
- Private Subnet
- Availability Zone
- Route Table Association
- Public IPv4 Address
- Internet Gateway
- NAT Gateway
- Subnet Communication
- Subnet Security
- Subnet Architecture
- Practical Subnet Configuration

---

## 1. What is a Subnet?

### Explanation

A **Subnet** is a smaller network range created inside an Amazon VPC.

A VPC can be divided into multiple subnets to organize AWS resources and control network traffic.

Each subnet belongs to one Availability Zone.

Example:

```text
                         VPC
                    10.0.0.0/16
                         |
             +-----------+-----------+
             |                       |
             v                       v
       Public Subnet            Private Subnet
       10.0.1.0/24              10.0.2.0/24
             |                       |
             v                       v
        Web Server              Application Server
```

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **VPC**.
3. Open the **Amazon VPC** service.
4. Select **Subnets**.
5. Review the existing subnets.
6. Check the VPC associated with each subnet.
7. Check the Availability Zone.
8. Check the IPv4 CIDR block.

### Result

**Successfully opened the Subnets section and understood that a subnet is a smaller IP network range inside a VPC.**

---

## 2. Subnet CIDR Block

### Explanation

A **Subnet CIDR Block** defines the IP address range available inside a subnet.

For example, if the VPC has:

```text
10.0.0.0/16
```

It can contain smaller subnet ranges such as:

```text
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24
```

### Example

```text
VPC
10.0.0.0/16
      |
      +---- 10.0.1.0/24
      |
      +---- 10.0.2.0/24
      |
      +---- 10.0.3.0/24
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Subnets**.
3. Click **Create subnet**.
4. Select the required VPC.
5. Enter the subnet name.
6. Select an Availability Zone.
7. Enter the IPv4 CIDR block.

Example:

```text
10.0.1.0/24
```

8. Review the CIDR configuration.
9. Click **Create subnet**.
10. Verify the subnet.

### Result

**Successfully created a subnet with a CIDR block and understood how the subnet receives a specific IP address range from the VPC.**

---

## 3. Public Subnet

### Explanation

A **Public Subnet** is a subnet whose route table has a route to an **Internet Gateway**.

Resources inside the subnet can have internet connectivity when the required public IP addressing, routing, and security configuration are present.

A public subnet is commonly used for:

- Web servers
- Public-facing applications
- Load balancers
- Bastion hosts

### Example

```text
                         Internet
                             |
                             v
                     Internet Gateway
                             |
                             v
                        Route Table
                             |
                             v
                       Public Subnet
                             |
                             v
                        EC2 Instance
```

### Practical Steps

1. Create a subnet inside the VPC.
2. Select the required Availability Zone.
3. Assign a CIDR block.
4. Create or select a Route Table.
5. Add a route to the Internet Gateway.

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

6. Associate the Route Table with the subnet.
7. Enable public IPv4 addressing for the EC2 instance when required.
8. Configure the Security Group.
9. Launch an EC2 instance in the subnet.
10. Verify the network configuration.

### Result

**Successfully configured a public subnet and understood how routing through an Internet Gateway provides a path to the internet.**

---

## 4. Private Subnet

### Explanation

A **Private Subnet** is a subnet that does not have a direct route to an Internet Gateway for internet access.

Private subnets are commonly used for resources that should not be directly accessible from the public internet.

Examples:

- Database servers
- Application servers
- Backend servers
- Internal services

### Example

```text
                         VPC
                          |
                          v
                   Private Subnet
                          |
              +-----------+-----------+
              |                       |
              v                       v
        Application Server       Database Server
```

A private subnet can use a NAT Gateway for outbound internet access when required.

### Practical Steps

1. Create a subnet inside the VPC.
2. Select the required Availability Zone.
3. Enter the private subnet CIDR block.
4. Create or select a private Route Table.
5. Do not add a direct default route to the Internet Gateway.
6. Create a NAT Gateway when outbound internet access is required.
7. Add the NAT Gateway route to the private Route Table.
8. Associate the Route Table with the private subnet.
9. Verify the configuration.

### Result

**Successfully configured a private subnet and understood how private resources can be protected from direct internet access.**

---

## 5. Public Subnet vs Private Subnet

### Explanation

Public and private subnets are mainly differentiated by their routing configuration.

### Public Subnet

```text
Public Subnet
     |
     v
Route Table
     |
     v
Internet Gateway
     |
     v
Internet
```

### Private Subnet

```text
Private Subnet
     |
     v
Route Table
     |
     v
NAT Gateway
     |
     v
Internet Gateway
     |
     v
Internet
```

### Comparison

| Feature | Public Subnet | Private Subnet |
|---|---|---|
| Internet Gateway Route | Yes | No direct route |
| Direct Internet Access | Possible with proper configuration | Not directly |
| Common Usage | Web Servers | Application/Database Servers |
| Public IP | Can be assigned | Usually not assigned |
| NAT Gateway | Not required for inbound internet access | Used for outbound internet access when required |

### Result

**Successfully understood the difference between public and private subnets and their common use cases.**

---

## 6. Availability Zone and Subnet

### Explanation

Each subnet is associated with **one Availability Zone**.

An AWS Region contains multiple Availability Zones.

You can create subnets across different Availability Zones to distribute resources.

### Example

```text
                    AWS Region
                        |
          +-------------+-------------+
          |                           |
          v                           v
 Availability Zone A          Availability Zone B
          |                           |
          v                           v
 Public Subnet                Private Subnet
 10.0.1.0/24                  10.0.2.0/24
```

Using multiple Availability Zones can help improve application availability and resilience.

### Practical Steps

1. Open **VPC > Subnets**.
2. Click **Create subnet**.
3. Select the VPC.
4. Select Availability Zone A.
5. Create the first subnet.
6. Create another subnet.
7. Select Availability Zone B.
8. Assign a different CIDR block.
9. Create the second subnet.
10. Verify the Availability Zone of each subnet.

### Result

**Successfully created subnets in different Availability Zones and understood their relationship with AWS Regions.**

---

## 7. Route Table Association

### Explanation

A subnet uses a Route Table to determine where network traffic should be sent.

A Route Table can be associated with one or more subnets.

Example:

```text
Route Table
     |
     +---- Public Subnet 1
     |
     +---- Public Subnet 2
```

A subnet can have only one route table associated with it at a time, either explicitly or through the VPC's main route table.

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Route Tables**.
3. Select the required Route Table.
4. Open **Subnet associations**.
5. Click **Edit subnet associations**.
6. Select the required subnet.
7. Save the association.
8. Verify that the subnet is associated with the correct Route Table.

### Result

**Successfully associated a subnet with a Route Table and understood how routing is applied to subnet traffic.**

---

## 8. Internet Gateway and Public Subnet

### Explanation

A public subnet requires a routing path to an Internet Gateway for internet connectivity.

The Internet Gateway itself does not automatically make a subnet public.

The subnet's Route Table must contain an appropriate route.

### Example

```text
EC2 Instance
     |
     v
Public Subnet
     |
     v
Route Table
     |
     v
0.0.0.0/0
     |
     v
Internet Gateway
     |
     v
Internet
```

### Practical Steps

1. Create or select an Internet Gateway.
2. Attach it to the VPC.
3. Open **Route Tables**.
4. Select the public Route Table.
5. Open **Routes**.
6. Click **Edit routes**.
7. Add:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

8. Save the route.
9. Associate the Route Table with the public subnet.
10. Verify the configuration.

### Result

**Successfully configured the routing required for a public subnet to communicate with the internet.**

---

## 9. NAT Gateway and Private Subnet

### Explanation

A **NAT Gateway** allows resources in a private subnet to initiate outbound connections to the internet.

The private resources are not directly exposed through an Internet Gateway.

### Example

```text
Private EC2
     |
     v
Private Subnet
     |
     v
Private Route Table
     |
     v
NAT Gateway
     |
     v
Internet Gateway
     |
     v
Internet
```

### Practical Steps

1. Create a public subnet.
2. Create a NAT Gateway in the public subnet.
3. Allocate an Elastic IP address.
4. Create the NAT Gateway.
5. Open the private subnet Route Table.
6. Add the default route.

```text
Destination:
0.0.0.0/0

Target:
NAT Gateway
```

7. Associate the Route Table with the private subnet.
8. Verify the configuration.

### Result

**Successfully understood how a NAT Gateway provides outbound internet connectivity to resources in a private subnet.**

---

## 10. Public IPv4 Address in a Subnet

### Explanation

An EC2 instance in a public subnet can receive a public IPv4 address when public IPv4 addressing is enabled and the instance is configured appropriately.

A public IP allows communication with the internet when routing and security rules permit it.

### Example

```text
Internet
    |
    v
Public IPv4 Address
    |
    v
EC2 Instance
    |
    v
Public Subnet
```

### Practical Steps

1. Open the **EC2** service.
2. Click **Launch instance**.
3. Select the required VPC.
4. Select the public subnet.
5. Review the public IP setting.
6. Enable public IPv4 addressing when required.
7. Configure the Security Group.
8. Launch the instance.
9. Open the instance details.
10. Verify the Public IPv4 address.

### Result

**Successfully understood how public IPv4 addressing can be used with resources in a public subnet.**

---

## 11. Subnet IP Addresses

### Explanation

A subnet receives its IP address range from the VPC CIDR block.

For example:

```text
VPC:
10.0.0.0/16
```

A subnet can use:

```text
10.0.1.0/24
```

The subnet then provides IP addresses for resources placed inside it.

### Example

```text
VPC
10.0.0.0/16
       |
       v
Subnet
10.0.1.0/24
       |
       +---- EC2: 10.0.1.10
       |
       +---- EC2: 10.0.1.20
       |
       +---- EC2: 10.0.1.30
```

### Result

**Successfully understood how subnet CIDR blocks provide IP addresses to resources inside the subnet.**

---

## 12. Subnet and Security Group

### Explanation

A subnet provides the network location for a resource, while a Security Group controls network traffic to and from resources such as EC2 instances.

They work together.

### Example

```text
VPC
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

### Practical Steps

1. Create a subnet.
2. Create a Security Group.
3. Configure the required inbound rules.
4. Configure the required outbound rules.
5. Launch an EC2 instance.
6. Select the VPC.
7. Select the subnet.
8. Select the Security Group.
9. Verify the instance networking configuration.

### Result

**Successfully understood how Subnets and Security Groups work together to provide network placement and traffic control.**

---

## 13. Subnet and Network ACL

### Explanation

A **Network ACL** provides security at the subnet level.

A Security Group works with resources such as EC2 network interfaces, while a Network ACL controls traffic entering and leaving the subnet.

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
EC2 Instance
 |
 v
Security Group
```

### Practical Steps

1. Open the VPC Dashboard.
2. Select **Network ACLs**.
3. Create or select a Network ACL.
4. Configure inbound rules.
5. Configure outbound rules.
6. Associate the Network ACL with the required subnet.
7. Verify the association.
8. Review the Security Group of the resources inside the subnet.

### Result

**Successfully understood how Network ACLs provide subnet-level traffic control.**

---

## 14. Subnet Communication

### Explanation

Resources inside different subnets of the same VPC can communicate using the VPC's local routing, provided that the applicable security controls allow the traffic.

Example:

```text
VPC
10.0.0.0/16
       |
       +----------------------+
       |                      |
       v                      v
Public Subnet            Private Subnet
10.0.1.0/24              10.0.2.0/24
       |                      |
       v                      v
EC2 Web Server           EC2 App Server
```

The local VPC route provides the routing path between the subnet IP ranges.

### Result

**Successfully understood how resources in different subnets can communicate through VPC local routing when security rules permit the traffic.**

---

## 15. Subnet Route Table Example

### Public Subnet Route Table

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

### Private Subnet Route Table

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         NAT Gateway
```

### Explanation

The **Public Subnet Route Table** sends internet-bound traffic to the Internet Gateway.

The **Private Subnet Route Table** sends internet-bound traffic to the NAT Gateway.

### Result

**Successfully understood how different Route Tables can be used for public and private subnet networking.**

---

## 16. Creating Multiple Subnets

### Explanation

Multiple subnets can be created inside a VPC to separate different types of resources.

Example:

```text
                         VPC
                    10.0.0.0/16
                         |
        +----------------+----------------+
        |                |                |
        v                v                v
 Public Subnet      Private Subnet    Database Subnet
 10.0.1.0/24        10.0.2.0/24       10.0.3.0/24
        |                |                |
        v                v                v
   Web Server      App Server        Database
```

### Practical Steps

1. Open **VPC > Subnets**.
2. Click **Create subnet**.
3. Select the VPC.
4. Create the first subnet.

```text
Name:
Public-Subnet

CIDR:
10.0.1.0/24
```

5. Create the second subnet.

```text
Name:
Private-Subnet

CIDR:
10.0.2.0/24
```

6. Create the third subnet if required.

```text
Name:
Database-Subnet

CIDR:
10.0.3.0/24
```

7. Select appropriate Availability Zones.
8. Verify all subnet configurations.

### Result

**Successfully created multiple subnets and understood how subnets can be used to separate different types of AWS resources.**

---

## 17. Subnet Architecture

### Explanation

A typical AWS architecture can use public and private subnets to separate internet-facing resources from internal resources.

### Architecture

```text
                              Internet
                                  |
                                  v
                          Internet Gateway
                                  |
                                  v
                         +----------------+
                         | Public Subnet  |
                         | 10.0.1.0/24    |
                         +----------------+
                                  |
                                  v
                           EC2 Web Server
                                  |
                                  v
                              VPC Local
                                  |
                                  v
                         +----------------+
                         | Private Subnet|
                         | 10.0.2.0/24   |
                         +----------------+
                                  |
                                  v
                         EC2 Application
                                  |
                                  v
                         +----------------+
                         | Database Subnet|
                         | 10.0.3.0/24    |
                         +----------------+
                                  |
                                  v
                              Database
```

### Result

**Successfully understood how public, private, and database subnets can be arranged inside a VPC to create a structured and secure AWS network.**

---

## 18. Subnet Security Best Practices

### Explanation

Subnets should be designed according to the security and networking requirements of the application.

Important practices include:

- Use public subnets only for resources that require public access.
- Keep databases in private subnets.
- Use Security Groups to control resource traffic.
- Use Network ACLs when subnet-level filtering is required.
- Avoid unnecessary public IP addresses.
- Use NAT Gateway for required outbound access from private subnets.
- Use separate Route Tables for different network requirements.
- Use multiple Availability Zones for improved resilience.
- Follow the Principle of Least Privilege.
- Monitor network traffic when required.

### Example

```text
Internet
   |
   v
Public Subnet
   |
   v
Web Server
   |
   v
Private Subnet
   |
   v
Application Server
   |
   v
Private Database Subnet
   |
   v
Database
```

### Result

**Successfully understood important subnet security practices and how subnet design can improve the security of AWS resources.**

---

## 19. Complete Subnet Practical Lab

### Explanation

This practical lab creates a basic VPC network containing a public subnet and a private subnet.

### Practical Steps

### Step 1 - Create VPC

Create a VPC with:

```text
VPC Name:
AWS-Lab-VPC

CIDR:
10.0.0.0/16
```

### Step 2 - Create Public Subnet

Create:

```text
Subnet Name:
Public-Subnet

CIDR:
10.0.1.0/24
```

Select the required Availability Zone.

### Step 3 - Create Private Subnet

Create:

```text
Subnet Name:
Private-Subnet

CIDR:
10.0.2.0/24
```

Select the required Availability Zone.

### Step 4 - Create Internet Gateway

Create:

```text
Name:
AWS-Lab-IGW
```

Attach it to:

```text
AWS-Lab-VPC
```

### Step 5 - Create Public Route Table

Create:

```text
Name:
Public-Route-Table
```

Add:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

Associate the Route Table with:

```text
Public-Subnet
```

### Step 6 - Create NAT Gateway

Create a NAT Gateway in the public subnet.

Allocate an Elastic IP address.

Example:

```text
NAT Gateway:
AWS-Lab-NAT
```

### Step 7 - Configure Private Route Table

Create:

```text
Name:
Private-Route-Table
```

Add:

```text
Destination:
0.0.0.0/0

Target:
NAT Gateway
```

Associate the Route Table with:

```text
Private-Subnet
```

### Step 8 - Configure Security Group

Create:

```text
Name:
AWS-Lab-SG
```

Allow only the required inbound traffic.

Example:

```text
SSH:
Port 22

HTTP:
Port 80

HTTPS:
Port 443
```

Restrict the source appropriately.

### Step 9 - Launch EC2 in Public Subnet

Launch an EC2 instance.

Select:

```text
VPC:
AWS-Lab-VPC

Subnet:
Public-Subnet

Security Group:
AWS-Lab-SG
```

Enable public IPv4 addressing when required.

### Step 10 - Verify Public Connectivity

Check:

```text
EC2 Instance
      |
      v
Public Subnet
      |
      v
Public Route Table
      |
      v
Internet Gateway
      |
      v
Internet
```

### Step 11 - Verify Private Subnet

Place an appropriate resource in the private subnet.

Check:

```text
Private Resource
      |
      v
Private Subnet
      |
      v
Private Route Table
      |
      v
NAT Gateway
      |
      v
Internet Gateway
      |
      v
Internet
```

### Result

**Successfully created and configured public and private subnets inside an Amazon VPC and understood how CIDR blocks, Availability Zones, Route Tables, Internet Gateway, NAT Gateway, Security Groups, and Network ACLs work together to provide secure network connectivity.**

---

## 20. Complete Subnet Workflow

### Workflow

```text
Create VPC
    |
    v
Define VPC CIDR
    |
    v
Create Subnets
    |
    +---------------------+
    |                     |
    v                     v
Public Subnet        Private Subnet
    |                     |
    v                     v
Public Route Table   Private Route Table
    |                     |
    v                     v
Internet Gateway     NAT Gateway
    |                     |
    v                     v
Internet             Internet
```

### Practical Steps

1. Create a VPC.
2. Define the VPC CIDR block.
3. Create a public subnet.
4. Create a private subnet.
5. Select Availability Zones.
6. Create an Internet Gateway.
7. Attach the Internet Gateway to the VPC.
8. Create a public Route Table.
9. Add an Internet Gateway route.
10. Associate the public subnet.
11. Create a NAT Gateway if required.
12. Create a private Route Table.
13. Add a NAT Gateway route.
14. Associate the private subnet.
15. Configure Security Groups.
16. Configure Network ACLs if required.
17. Launch EC2 resources in the required subnets.
18. Test connectivity.
19. Verify the routing configuration.
20. Monitor the resources.
21. Delete unused resources after completing the lab.

### Final Result

**Successfully completed the Amazon VPC Subnets lab and understood how subnets divide a VPC into smaller network ranges. Learned the difference between public and private subnets, CIDR blocks, Availability Zones, Route Tables, Internet Gateway, NAT Gateway, Security Groups, Network ACLs, subnet communication, public IP addressing, and secure subnet architecture.**
