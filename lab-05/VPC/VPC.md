# Lab 05 - Amazon VPC

## Objective

The objective of this lab is to understand **Amazon Virtual Private Cloud (VPC)** and practically learn how to create and configure a virtual network in AWS.

This lab covers:

- VPC
- CIDR Block
- Subnets
- Public Subnet
- Private Subnet
- Internet Gateway
- Route Tables
- NAT Gateway
- Security Groups
- Network ACLs
- Availability Zones
- VPC Peering
- VPC Endpoints
- VPC Flow Logs
- VPC DNS
- VPC Security
- VPC Architecture

---

## 1. What is Amazon VPC?

### Explanation

**Amazon Virtual Private Cloud (VPC)** is a logically isolated virtual network in the AWS Cloud.

A VPC allows you to create and control your own networking environment.

Inside a VPC, you can configure:

- IP address ranges
- Subnets
- Route tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- EC2 Instances

A VPC provides control over how AWS resources communicate with each other and with the internet.

### Example

```text
                         AWS Cloud
                             |
                             v
                           VPC
                             |
          +------------------+------------------+
          |                                     |
          v                                     v
    Public Subnet                         Private Subnet
          |                                     |
          v                                     v
    EC2 Instance                         EC2 Instance
          |                                     |
          v                                     v
 Internet Gateway                         NAT Gateway
          |                                     |
          v                                     v
       Internet                              Internet
```

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **VPC**.
3. Open the **VPC** service.
4. Open the **VPC Dashboard**.
5. Review the available VPC resources.
6. Review **VPCs**, **Subnets**, **Route Tables**, **Internet Gateways**, and **Security Groups**.

### Result

**Successfully opened Amazon VPC and understood that VPC provides an isolated virtual networking environment in AWS.**

---

## 2. VPC CIDR Block

### Explanation

A **CIDR Block** defines the IP address range available inside a VPC.

For example:

```text
10.0.0.0/16
```

The VPC CIDR range can be divided into smaller subnet CIDR ranges.

### Example

```text
VPC
10.0.0.0/16
     |
     +-----------------------+
     |                       |
     v                       v
10.0.1.0/24             10.0.2.0/24
Public Subnet            Private Subnet
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Your VPCs**.
3. Click **Create VPC**.
4. Select **VPC only**.
5. Enter a VPC name.

Example:

```text
My-VPC
```

6. Enter the IPv4 CIDR block.

Example:

```text
10.0.0.0/16
```

7. Review the configuration.
8. Click **Create VPC**.
9. Verify that the VPC has been created.

### Result

**Successfully created a VPC with an IPv4 CIDR block and understood how the CIDR block defines the VPC IP address range.**

---

## 3. VPC Subnet

### Explanation

A **Subnet** is a smaller network range inside a VPC.

Subnets are used to organize AWS resources within a VPC.

A VPC can contain multiple subnets.

Common subnet designs include:

- Public Subnet
- Private Subnet

### Example

```text
                    VPC
                10.0.0.0/16
                     |
          +----------+----------+
          |                     |
          v                     v
    Public Subnet          Private Subnet
    10.0.1.0/24            10.0.2.0/24
          |                     |
          v                     v
    EC2 Web Server        Application Server
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Subnets**.
3. Click **Create subnet**.
4. Select the required VPC.
5. Enter the subnet name.
6. Select the Availability Zone.
7. Enter the IPv4 subnet CIDR block.

Example:

```text
10.0.1.0/24
```

8. Click **Create subnet**.
9. Verify that the subnet has been created.

### Result

**Successfully created a subnet inside the VPC and understood how subnets divide a VPC into smaller network ranges.**

---

## 4. Public Subnet

### Explanation

A **Public Subnet** is a subnet whose route table contains a route to an **Internet Gateway**.

Resources placed in a public subnet can communicate with the internet when the required routing, public IP addressing, and security rules are configured.

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
2. Open **Route Tables**.
3. Create or select a route table.
4. Add a route to the Internet Gateway.
5. Associate the route table with the public subnet.
6. Enable public IPv4 addressing for the EC2 resource when required.
7. Launch an EC2 instance in the public subnet.
8. Configure the required Security Group rules.
9. Verify the network configuration.

### Result

**Successfully understood how a subnet becomes public through routing to an Internet Gateway.**

---

## 5. Private Subnet

### Explanation

A **Private Subnet** is a subnet that does not have a direct route to an Internet Gateway for inbound internet access.

Private subnets are commonly used for resources that should not be directly reachable from the public internet.

Examples include:

- Database servers
- Application servers
- Backend services
- Internal systems

### Example

```text
Internet
    |
    X
    |
Private Subnet
    |
    +---- Application Server
    |
    +---- Database Server
```

A private subnet can use a **NAT Gateway** for outbound internet connectivity when required.

### Practical Steps

1. Create a subnet inside the VPC.
2. Select the required Availability Zone.
3. Assign a private CIDR range.
4. Create or select a route table for the private subnet.
5. Do not configure a direct default route to the Internet Gateway.
6. Configure a NAT Gateway when outbound internet access is required.
7. Associate the private subnet with the appropriate route table.
8. Verify the routing configuration.

### Result

**Successfully understood the purpose of private subnets and how they can be used to keep resources away from direct public internet access.**

---

## 6. Internet Gateway

### Explanation

An **Internet Gateway (IGW)** is a VPC component that provides a path between a VPC and the internet.

An Internet Gateway is commonly used for resources in a public subnet.

### Example

```text
                 Internet
                    |
                    v
            Internet Gateway
                    |
                    v
                   VPC
                    |
                    v
             Public Subnet
                    |
                    v
               EC2 Instance
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Internet Gateways**.
3. Click **Create internet gateway**.
4. Enter the Internet Gateway name.
5. Click **Create internet gateway**.
6. Select the created Internet Gateway.
7. Choose **Attach to a VPC**.
8. Select the required VPC.
9. Attach the Internet Gateway.
10. Verify that the Internet Gateway is attached to the VPC.

### Result

**Successfully created and attached an Internet Gateway to the VPC.**

---

## 7. Route Table

### Explanation

A **Route Table** contains routing rules that determine where network traffic should be sent.

A route contains:

- Destination
- Target

Example:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

This route can send IPv4 internet-bound traffic toward an Internet Gateway.

### Example

```text
EC2 Instance
     |
     v
Route Table
     |
     +---- 10.0.0.0/16 ---> local
     |
     +---- 0.0.0.0/0 ------> Internet Gateway
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Route Tables**.
3. Click **Create route table**.
4. Enter the route table name.
5. Select the VPC.
6. Click **Create route table**.
7. Open the **Routes** tab.
8. Click **Edit routes**.
9. Add the required destination.
10. Select the required target.
11. Save the routes.
12. Open **Subnet associations**.
13. Associate the required subnet.
14. Verify the route table configuration.

### Result

**Successfully created and configured a Route Table and understood how routes control network traffic inside a VPC.**

---

## 8. Local Route

### Explanation

A VPC route table contains a local route that allows communication between resources within the VPC according to the VPC's CIDR range.

Example:

```text
Destination:
10.0.0.0/16

Target:
local
```

### Example

```text
EC2 Instance A
10.0.1.10
     |
     v
    VPC
     |
     v
EC2 Instance B
10.0.2.10
```

The local route allows communication between resources using the VPC's local network range, subject to the applicable security controls.

### Result

**Successfully understood the purpose of the local route in a VPC Route Table.**

---

## 9. NAT Gateway

### Explanation

A **NAT Gateway** allows resources in a private subnet to initiate outbound connections to the internet without allowing direct inbound internet connections to those resources.

A common architecture is:

```text
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

1. Open the **VPC Dashboard**.
2. Select **NAT Gateways**.
3. Click **Create NAT gateway**.
4. Select a suitable public subnet.
5. Allocate or select an Elastic IP address.
6. Create the NAT Gateway.
7. Wait for the NAT Gateway to become available.
8. Open the private subnet's route table.
9. Click **Edit routes**.
10. Add the required default route.

```text
Destination:
0.0.0.0/0

Target:
NAT Gateway
```

11. Save the route.
12. Verify the NAT Gateway and route configuration.

### Result

**Successfully understood how a NAT Gateway can provide outbound internet connectivity for resources in a private subnet.**

---

## 10. Security Group

### Explanation

A **Security Group** acts as a virtual firewall for resources such as EC2 instances.

Security Groups control:

- Inbound traffic
- Outbound traffic

Security Groups are associated with network interfaces and are used to control access to AWS resources.

### Example

```text
                  Internet
                     |
                     v
               Security Group
                /          \
               /            \
        Inbound Rules    Outbound Rules
               \            /
                \          /
                     |
                     v
                 EC2 Instance
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Security Groups**.
3. Click **Create security group**.
4. Enter the Security Group name.
5. Enter the description.
6. Select the VPC.
7. Configure inbound rules.
8. Configure outbound rules.
9. Review the configuration.
10. Click **Create security group**.
11. Associate the Security Group with the required resource.
12. Verify the Security Group configuration.

### Result

**Successfully created and understood how Security Groups control traffic to and from AWS resources.**

---

## 11. Inbound Rules

### Explanation

**Inbound Rules** control traffic coming into a resource protected by a Security Group.

Common ports include:

| Protocol | Port | Purpose |
|---|---:|---|
| SSH | 22 | Linux remote access |
| HTTP | 80 | Web traffic |
| HTTPS | 443 | Secure web traffic |
| RDP | 3389 | Windows remote access |

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

**Successfully configured inbound rules and understood how incoming network traffic is controlled.**

---

## 12. Outbound Rules

### Explanation

**Outbound Rules** control traffic leaving a resource protected by a Security Group.

These rules determine which destinations the resource can communicate with.

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

**Successfully reviewed outbound rules and understood how outgoing network traffic is controlled.**

---

## 13. Network ACL

### Explanation

A **Network Access Control List (Network ACL)** is a network-level security control associated with a subnet.

Network ACLs can control:

- Inbound traffic
- Outbound traffic

Network ACLs operate at the subnet level.

### Example

```text
                 VPC
                  |
                  v
               Subnet
                  |
                  v
             Network ACL
              /       \
             v         v
        Inbound     Outbound
             \       /
              \     /
               EC2
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Network ACLs**.
3. Click **Create network ACL**.
4. Enter the Network ACL name.
5. Select the VPC.
6. Create the Network ACL.
7. Open **Inbound rules**.
8. Configure the required rules.
9. Open **Outbound rules**.
10. Configure the required rules.
11. Associate the Network ACL with the required subnet.
12. Verify the configuration.

### Result

**Successfully understood how Network ACLs provide subnet-level network traffic control.**

---

## 14. Availability Zone

### Explanation

An **Availability Zone (AZ)** is an isolated location within an AWS Region.

A VPC can contain subnets in multiple Availability Zones.

Using multiple Availability Zones can help improve application availability and resilience.

### Example

```text
                    AWS Region
                        |
              +---------+---------+
              |                   |
              v                   v
        Availability Zone A  Availability Zone B
              |                   |
              v                   v
        Public Subnet        Private Subnet
```

### Result

**Successfully understood the relationship between AWS Regions, Availability Zones, VPCs, and Subnets.**

---

## 15. VPC Peering

### Explanation

**VPC Peering** allows two VPCs to communicate with each other using private IP addresses.

The VPCs must have appropriate non-overlapping CIDR ranges.

### Example

```text
VPC A
10.0.0.0/16
    |
    |
VPC Peering Connection
    |
    |
VPC B
10.1.0.0/16
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Peering connections**.
3. Click **Create peering connection**.
4. Select the requester VPC.
5. Select the accepter VPC.
6. Create the peering connection.
7. Accept the peering request if required.
8. Update the route tables.
9. Add routes for the peer VPC CIDR.
10. Verify the connectivity according to the configured security rules.

### Result

**Successfully understood how VPC Peering provides private network connectivity between two VPCs.**

---

## 16. VPC Endpoints

### Explanation

A **VPC Endpoint** provides private connectivity between a VPC and supported AWS services.

It can allow resources in a VPC to access supported AWS services without requiring traffic to use the public internet.

### Example

```text
EC2 Instance
     |
     v
Private Subnet
     |
     v
VPC Endpoint
     |
     v
AWS Service
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Endpoints**.
3. Click **Create endpoint**.
4. Select the required AWS service.
5. Select the VPC.
6. Select the required subnets or route tables according to the endpoint type.
7. Configure the required Security Group settings when applicable.
8. Create the endpoint.
9. Verify the endpoint configuration.

### Result

**Successfully understood the purpose of VPC Endpoints and how they can provide private connectivity to supported AWS services.**

---

## 17. VPC Flow Logs

### Explanation

**VPC Flow Logs** capture information about network traffic flowing to and from network interfaces in a VPC.

Flow Logs can help with:

- Network troubleshooting
- Security analysis
- Monitoring
- Traffic investigation

### Example

```text
Network Traffic
       |
       v
      VPC
       |
       v
VPC Flow Logs
       |
       v
Monitoring / Analysis
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select the required VPC or network resource.
3. Open the **Flow Logs** section.
4. Click **Create flow log**.
5. Configure the required traffic type.
6. Select the destination.
7. Configure the required settings.
8. Create the flow log.
9. Verify that the flow log is configured.

### Result

**Successfully understood how VPC Flow Logs can be used to capture and analyze network traffic information.**

---

## 18. VPC DNS

### Explanation

Amazon VPC provides DNS functionality that helps AWS resources resolve domain names.

DNS allows resources to use domain names instead of relying only on IP addresses.

### Example

```text
EC2 Instance
     |
     v
VPC DNS
     |
     v
Domain Name Resolution
     |
     v
IP Address
```

### Result

**Successfully understood the basic purpose of DNS functionality within an Amazon VPC.**

---

## 19. VPC and EC2 Architecture

### Explanation

An EC2 instance runs inside a VPC and is placed inside a subnet.

The VPC provides the networking environment, while the subnet provides the IP address range where the EC2 instance is located.

### Architecture

```text
                         AWS Cloud
                             |
                             v
                           VPC
                       10.0.0.0/16
                             |
              +--------------+--------------+
              |                             |
              v                             v
        Public Subnet                 Private Subnet
        10.0.1.0/24                   10.0.2.0/24
              |                             |
              v                             v
        Security Group                Security Group
              |                             |
              v                             v
        EC2 Web Server             EC2 Application Server
              |
              v
       Internet Gateway
              |
              v
           Internet
```

### Result

**Successfully understood how VPC, Subnets, Security Groups, Route Tables, Internet Gateways, and EC2 instances work together.**

---

## 20. Complete VPC Workflow

### Explanation

The complete VPC workflow includes creating a VPC, defining the CIDR range, creating subnets, configuring route tables, attaching an Internet Gateway, configuring security, and deploying AWS resources.

### Workflow

```text
Create VPC
    |
    v
Define CIDR Block
    |
    v
Create Subnets
    |
    +------------------+
    |                  |
    v                  v
Public Subnet     Private Subnet
    |                  |
    v                  v
Route Table        Route Table
    |                  |
    v                  v
Internet Gateway   NAT Gateway
    |                  |
    +--------+---------+
             |
             v
      Security Group
             |
             v
        Network ACL
             |
             v
         Launch EC2
             |
             v
      Test Connectivity
             |
             v
          Monitor
```

### Practical Steps

1. Open the **VPC Dashboard**.
2. Create a VPC.
3. Configure the VPC CIDR block.

```text
10.0.0.0/16
```

4. Create a public subnet.

```text
10.0.1.0/24
```

5. Create a private subnet.

```text
10.0.2.0/24
```

6. Create an Internet Gateway.
7. Attach the Internet Gateway to the VPC.
8. Create a Route Table for the public subnet.
9. Add the Internet Gateway route.
10. Associate the public subnet with the Route Table.
11. Create a NAT Gateway if private-subnet outbound internet access is required.
12. Configure the private subnet Route Table.
13. Configure Security Groups.
14. Configure Network ACLs if required.
15. Launch an EC2 instance.
16. Select the VPC.
17. Select the required subnet.
18. Configure the Security Group.
19. Test network connectivity.
20. Review the VPC configuration.
21. Monitor the resources.
22. Delete unused resources after completing the lab.

### Result

**Successfully completed the VPC lab and understood the complete process of creating and configuring an Amazon VPC, subnets, route tables, Internet Gateway, NAT Gateway, Security Groups, Network ACLs, and EC2 networking.**
