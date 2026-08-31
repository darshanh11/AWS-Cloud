# Lab 07 - Route Tables and Internet Gateway

## Objective

The objective of this lab is to understand **Route Tables** and **Internet Gateway (IGW)** in Amazon VPC and practically learn how they control communication between AWS resources and the internet.

This lab covers:

- Route Tables
- Routes
- Local Routes
- Internet Gateway
- Public Route Table
- Public Subnet
- Route Table Association
- Default Route
- Internet Connectivity
- VPC Routing
- Practical Configuration
- Routing Architecture

---

## 1. What is a Route Table?

### Explanation

A **Route Table** is a set of rules called routes that determine where network traffic should be sent.

Every subnet in a VPC is associated with a Route Table.

A Route Table contains:

- Destination
- Target

Example:

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

The destination specifies where the traffic is going.

The target specifies where the traffic should be sent.

### Example

```text
EC2 Instance
     |
     v
Subnet
     |
     v
Route Table
     |
     +---- VPC Traffic ------> local
     |
     +---- Internet Traffic -> Internet Gateway
```

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **VPC**.
3. Open the **VPC** service.
4. Select **Route Tables**.
5. Review the available Route Tables.
6. Select a Route Table.
7. Open the **Routes** tab.
8. Review the configured destinations and targets.

### Result

**Successfully opened Route Tables and understood how routing rules determine where network traffic is sent.**

---

## 2. What is a Route?

### Explanation

A **Route** is an individual rule inside a Route Table.

A route contains:

```text
Destination
Target
```

Example:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

This route means IPv4 traffic destined for addresses outside the VPC can be sent toward the Internet Gateway.

### Example

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         igw-xxxxxxxx
```

### Result

**Successfully understood that routes define the destination and target for network traffic.**

---

## 3. Local Route

### Explanation

A VPC Route Table normally contains a **local route** for the VPC CIDR block.

Example:

```text
Destination:
10.0.0.0/16

Target:
local
```

The local route allows communication between resources within the VPC according to the VPC's routing configuration.

### Example

```text
VPC
10.0.0.0/16
     |
     +-------------------+
     |                   |
     v                   v
Subnet A             Subnet B
10.0.1.0/24          10.0.2.0/24
     |                   |
     v                   v
EC2 A                EC2 B
```

The local route provides the VPC-level routing path between the subnets.

### Result

**Successfully understood the purpose of the local route in a VPC Route Table.**

---

## 4. What is an Internet Gateway?

### Explanation

An **Internet Gateway (IGW)** is a VPC component that provides a path between a VPC and the internet.

An Internet Gateway is commonly used with resources in a public subnet.

An Internet Gateway must be attached to a VPC before it can be used for internet connectivity.

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
7. Choose **Actions**.
8. Select **Attach to a VPC**.
9. Select the required VPC.
10. Attach the Internet Gateway.
11. Verify that the Internet Gateway is attached.

### Result

**Successfully created and attached an Internet Gateway to the VPC.**

---

## 5. Public Route Table

### Explanation

A **Public Route Table** is a Route Table that contains a route to an Internet Gateway.

Example:

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

The route:

```text
0.0.0.0/0
```

represents all IPv4 destinations that are not covered by a more specific route.

### Example

```text
Public Subnet
      |
      v
Public Route Table
      |
      +---- 10.0.0.0/16 ---> local
      |
      +---- 0.0.0.0/0 ------> Internet Gateway
```

### Result

**Successfully understood how a Route Table can provide a routing path from a public subnet toward the internet.**

---

## 6. Creating a Route Table

### Explanation

A Route Table can be created inside a VPC and then associated with one or more subnets.

### Practical Steps

1. Open the **VPC Dashboard**.
2. Select **Route Tables**.
3. Click **Create route table**.
4. Enter the Route Table name.

Example:

```text
Public-Route-Table
```

5. Select the required VPC.
6. Click **Create route table**.
7. Verify that the Route Table has been created.

### Result

**Successfully created a Route Table inside the selected VPC.**

---

## 7. Adding an Internet Gateway Route

### Explanation

After creating an Internet Gateway, a route must be added to the appropriate Route Table.

Example:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

This creates a route toward the internet for traffic that matches the default IPv4 destination.

### Practical Steps

1. Open **VPC > Route Tables**.
2. Select the public Route Table.
3. Open the **Routes** tab.
4. Click **Edit routes**.
5. Click **Add route**.
6. Enter:

```text
Destination:
0.0.0.0/0
```

7. Select:

```text
Target:
Internet Gateway
```

8. Select the attached Internet Gateway.
9. Save the changes.
10. Verify the route.

### Result

**Successfully added a default route from the Route Table to the Internet Gateway.**

---

## 8. Associating a Route Table with a Subnet

### Explanation

A Route Table must be associated with a subnet for the subnet to use its routes.

Example:

```text
Route Table
     |
     v
Public Subnet
     |
     v
EC2 Instance
```

### Practical Steps

1. Open **VPC > Route Tables**.
2. Select the required Route Table.
3. Open **Subnet associations**.
4. Click **Edit subnet associations**.
5. Select the required public subnet.
6. Save the association.
7. Verify that the subnet is associated with the Route Table.

### Result

**Successfully associated the Route Table with the subnet.**

---

## 9. Public Subnet and Internet Gateway

### Explanation

A subnet becomes public when its associated Route Table has a route to an Internet Gateway.

The Internet Gateway alone does not make a subnet public.

The following components work together:

```text
VPC
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

The EC2 instance also needs appropriate public addressing and Security Group configuration for internet connectivity.

### Result

**Successfully understood that public subnet functionality depends on routing through an Internet Gateway along with the required resource and security configuration.**

---

## 10. Default Route

### Explanation

A **Default Route** is commonly represented as:

```text
0.0.0.0/0
```

It matches IPv4 destinations that are not matched by a more specific route.

For a public subnet, the default route can point to an Internet Gateway.

### Example

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

### Example Flow

```text
EC2 Instance
     |
     v
Destination: 8.8.8.8
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

### Result

**Successfully understood how the default route can direct internet-bound IPv4 traffic toward an Internet Gateway.**

---

## 11. Route Table and Public EC2 Instance

### Explanation

A public EC2 instance requires the correct combination of:

- VPC
- Public Subnet
- Route Table
- Internet Gateway
- Public IPv4 address
- Security Group rules

### Architecture

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
                             |
                       Public IPv4
```

### Practical Steps

1. Create or select a VPC.
2. Create a public subnet.
3. Create an Internet Gateway.
4. Attach the Internet Gateway to the VPC.
5. Create a Route Table.
6. Add the default route.
7. Associate the Route Table with the public subnet.
8. Create or select a Security Group.
9. Launch an EC2 instance in the public subnet.
10. Enable public IPv4 addressing when required.
11. Verify the EC2 instance network configuration.
12. Test connectivity according to the configured Security Group rules.

### Result

**Successfully understood the complete routing path required for an EC2 instance in a public subnet to communicate with the internet.**

---

## 12. Route Table and Private Subnet

### Explanation

A private subnet normally does not have a direct route to an Internet Gateway.

If private resources need outbound internet connectivity, the Route Table can send internet-bound traffic to a NAT Gateway.

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

### Result

**Successfully understood the difference between public subnet routing through an Internet Gateway and private subnet outbound routing through a NAT Gateway.**

---

## 13. Route Table Association

### Explanation

A Route Table can be associated with multiple subnets.

Example:

```text
Public Route Table
       |
       +---- Public Subnet 1
       |
       +---- Public Subnet 2
```

A subnet uses one Route Table association at a time, either an explicit association or the VPC's main Route Table.

### Practical Steps

1. Open **VPC > Route Tables**.
2. Select the required Route Table.
3. Open **Subnet associations**.
4. Click **Edit subnet associations**.
5. Select the required subnets.
6. Save the changes.
7. Verify the associations.

### Result

**Successfully understood how Route Tables are associated with subnets.**

---

## 14. Main Route Table

### Explanation

Every VPC has a **Main Route Table**.

The main Route Table is used by subnets that do not have an explicit Route Table association.

A different Route Table can be explicitly associated with a subnet when specific routing is required.

### Example

```text
VPC
 |
 +---- Main Route Table
 |
 +---- Public Route Table
 |
 +---- Private Route Table
```

### Result

**Successfully understood the purpose of the Main Route Table and explicit subnet Route Table associations.**

---

## 15. Route Priority

### Explanation

When multiple routes match a destination, AWS uses the route with the most specific matching destination.

For example:

```text
10.0.0.0/16
10.0.1.0/24
0.0.0.0/0
```

A destination within:

```text
10.0.1.0/24
```

matches the more specific route rather than the broader VPC or default route.

### Example

```text
Destination:
10.0.1.20

Possible Routes:

10.0.0.0/16
10.0.1.0/24
0.0.0.0/0

Most Specific:
10.0.1.0/24
```

### Result

**Successfully understood that routing decisions use the most specific matching route.**

---

## 16. Route Table Troubleshooting

### Explanation

If an EC2 instance cannot communicate with the internet, the Route Table should be one of the first components to check.

Important items to verify:

- Correct VPC
- Correct subnet
- Correct Route Table
- Internet Gateway attached
- Default route configured
- Public IPv4 address
- Security Group
- Network ACL

### Troubleshooting Flow

```text
EC2 Cannot Access Internet
          |
          v
Check Subnet
          |
          v
Check Route Table
          |
          v
Check 0.0.0.0/0 Route
          |
          v
Check Internet Gateway
          |
          v
Check Public IP
          |
          v
Check Security Group
          |
          v
Check Network ACL
```

### Result

**Successfully understood the basic troubleshooting process for Route Table and Internet connectivity problems.**

---

## 17. Practical Lab - Create Public Network

### Explanation

In this practical lab, a VPC, public subnet, Internet Gateway, Route Table, and EC2 instance are connected together to create a basic public network.

### Practical Steps

### Step 1 - Create VPC

Create:

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

### Step 3 - Create Internet Gateway

Create:

```text
Internet Gateway:
AWS-Lab-IGW
```

Attach it to:

```text
AWS-Lab-VPC
```

### Step 4 - Create Route Table

Create:

```text
Route Table:
Public-Route-Table
```

Select:

```text
VPC:
AWS-Lab-VPC
```

### Step 5 - Add Default Route

Add:

```text
Destination:
0.0.0.0/0

Target:
AWS-Lab-IGW
```

### Step 6 - Associate Subnet

Associate:

```text
Public-Subnet
```

with:

```text
Public-Route-Table
```

### Step 7 - Launch EC2

Launch an EC2 instance using:

```text
VPC:
AWS-Lab-VPC

Subnet:
Public-Subnet
```

Enable public IPv4 addressing when required.

### Step 8 - Configure Security Group

Allow only the required traffic.

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

### Step 9 - Verify

Check:

```text
EC2
 |
 v
Public Subnet
 |
 v
Public Route Table
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

### Result

**Successfully created a basic public VPC network using a VPC, public subnet, Route Table, Internet Gateway, and EC2 instance.**

---

## 18. Complete Route Table and Internet Gateway Architecture

```text
                              Internet
                                  |
                                  v
                         Internet Gateway
                                  |
                                  v
                           Public Route Table
                                  |
                  +---------------+---------------+
                  |                               |
                  v                               v
            Public Subnet 1                Public Subnet 2
            10.0.1.0/24                    10.0.3.0/24
                  |                               |
                  v                               v
             EC2 Web Server                  EC2 Server
```

### Private Network

```text
                         Internet
                             |
                             v
                     Internet Gateway
                             |
                             v
                       NAT Gateway
                             |
                             v
                     Private Route Table
                             |
                             v
                      Private Subnet
                             |
                             v
                      Private EC2
```

---

## 19. Route Table vs Security Group

### Explanation

Route Tables and Security Groups perform different functions.

### Route Table

Determines:

```text
Where should the traffic go?
```

### Security Group

Determines:

```text
Which traffic is allowed?
```

### Example

```text
Traffic
   |
   v
Route Table
   |
   | Determines destination
   v
Security Group
   |
   | Allows or blocks traffic
   v
EC2 Instance
```

### Result

**Successfully understood the difference between routing decisions and security filtering.**

---

## 20. Route Table vs Network ACL

### Explanation

A Route Table controls **where traffic is routed**.

A Network ACL controls **whether traffic is allowed or denied at the subnet level**.

### Comparison

| Component | Purpose | Level |
|---|---|---|
| Route Table | Determines traffic destination | Subnet routing |
| Security Group | Controls allowed traffic | Resource/network interface |
| Network ACL | Controls allowed or denied traffic | Subnet |

### Example

```text
Traffic
   |
   v
Route Table
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
EC2
```

### Result

**Successfully understood the different responsibilities of Route Tables, Security Groups, and Network ACLs.**

---

## 21. Route Table Security Best Practices

### Explanation

Route Tables should be configured carefully to prevent unintended network exposure.

Important practices include:

- Use public routes only where required.
- Keep private resources in private subnets.
- Do not add unnecessary Internet Gateway routes.
- Use NAT Gateway when private resources require outbound internet access.
- Review Route Table associations.
- Use separate Route Tables for different network requirements.
- Avoid unnecessary public IP addresses.
- Regularly review network configuration.

### Result

**Successfully understood important Route Table security and network design practices.**

---

## 22. Complete Practical Workflow

### Workflow

```text
Create VPC
    |
    v
Create Public Subnet
    |
    v
Create Internet Gateway
    |
    v
Attach Internet Gateway to VPC
    |
    v
Create Route Table
    |
    v
Add 0.0.0.0/0 Route
    |
    v
Target Internet Gateway
    |
    v
Associate Route Table
    |
    v
Public Subnet
    |
    v
Launch EC2
    |
    v
Assign Public IPv4
    |
    v
Configure Security Group
    |
    v
Test Connectivity
```

### Final Result

**Successfully completed Lab 07 - Route Tables and Internet Gateway and understood how AWS VPC routing works. Learned how Route Tables determine traffic destinations, how local routes provide VPC connectivity, how Internet Gateways provide a path to the internet, how public subnets are configured, how Route Tables are associated with subnets, how default routes work, and how Route Tables, Internet Gateways, Security Groups, and Network ACLs work together to provide controlled network connectivity.**
