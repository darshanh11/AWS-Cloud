# Lab 08 - Internet Gateway (IGW)

## Objective

The objective of this lab is to understand the **Internet Gateway (IGW)** in Amazon VPC and practically learn how to create, attach, configure, and use an Internet Gateway to provide internet connectivity for resources in a public subnet.

This lab covers:

- Internet Gateway
- VPC and Internet Gateway
- Public Subnet
- Route Table
- Default Route
- Internet Connectivity
- Public IPv4 Address
- Internet Gateway Architecture
- Practical Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is an Internet Gateway?

### Explanation

An **Internet Gateway (IGW)** is a VPC component that allows communication between resources in a VPC and the internet.

An Internet Gateway is horizontally scaled, redundant, and highly available.

An Internet Gateway does not automatically make a subnet public.

For a subnet to communicate with the internet, the required **Route Table** must contain a route to the Internet Gateway.

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

### Result

**Successfully understood that an Internet Gateway provides a path between a VPC and the internet.**

---

## 2. Internet Gateway and VPC

### Explanation

An Internet Gateway must be attached to a VPC before it can be used.

One Internet Gateway can be attached to one VPC at a time.

The basic relationship is:

```text
Internet Gateway
       |
       v
      VPC
       |
       v
Public Subnet
```

### Practical Steps

1. Open the **AWS Management Console**.
2. Search for **VPC**.
3. Open the **VPC** service.
4. Select **Internet Gateways**.
5. Review the existing Internet Gateways.
6. Check whether an Internet Gateway is attached to a VPC.
7. Verify the attached VPC.

### Result

**Successfully understood the relationship between an Internet Gateway and a VPC.**

---

## 3. Creating an Internet Gateway

### Explanation

An Internet Gateway can be created from the VPC console.

Creating an Internet Gateway does not automatically provide internet connectivity.

It must first be attached to the required VPC and then used as a target in an appropriate Route Table.

### Practical Steps

1. Open **VPC**.
2. Select **Internet Gateways**.
3. Click **Create internet gateway**.
4. Enter an Internet Gateway name.

Example:

```text
AWS-Lab-IGW
```

5. Click **Create internet gateway**.
6. Verify that the Internet Gateway has been created.

### Result

**Successfully created an Internet Gateway named AWS-Lab-IGW.**

---

## 4. Attaching an Internet Gateway to a VPC

### Explanation

After creating an Internet Gateway, it must be attached to a VPC.

Only an attached Internet Gateway can provide the VPC with a path to the internet.

### Practical Steps

1. Open **VPC > Internet Gateways**.
2. Select the created Internet Gateway.
3. Choose **Actions**.
4. Select **Attach to a VPC**.
5. Select the required VPC.
6. Click **Attach internet gateway**.
7. Verify the attachment.

Example:

```text
Internet Gateway:
AWS-Lab-IGW

VPC:
AWS-Lab-VPC
```

### Result

**Successfully attached the Internet Gateway to the VPC.**

---

## 5. Internet Gateway and Public Subnet

### Explanation

An Internet Gateway is commonly used to provide internet connectivity to resources in a public subnet.

However, the subnet must have a Route Table containing a route to the Internet Gateway.

### Example

```text
Internet
    |
    v
Internet Gateway
    |
    v
Public Route Table
    |
    v
Public Subnet
    |
    v
EC2 Instance
```

### Result

**Successfully understood how an Internet Gateway works with a public subnet through Route Table configuration.**

---

## 6. Default Route to Internet Gateway

### Explanation

A public subnet's Route Table commonly contains a default IPv4 route:

```text
0.0.0.0/0
```

The target of this route is the Internet Gateway.

Example:

```text
Destination       Target
--------------------------------
10.0.0.0/16       local
0.0.0.0/0         Internet Gateway
```

The `0.0.0.0/0` route represents all IPv4 destinations not matched by a more specific route.

### Practical Steps

1. Open **VPC**.
2. Select **Route Tables**.
3. Select the public Route Table.
4. Open the **Routes** tab.
5. Click **Edit routes**.
6. Click **Add route**.
7. Enter:

```text
Destination:
0.0.0.0/0
```

8. Select:

```text
Target:
Internet Gateway
```

9. Select the created Internet Gateway.
10. Save the route.
11. Verify the route.

### Result

**Successfully configured a default route from the public Route Table to the Internet Gateway.**

---

## 7. Internet Gateway and EC2

### Explanation

An EC2 instance can communicate with the internet when the required network configuration is present.

The main components are:

- VPC
- Public Subnet
- Route Table
- Internet Gateway
- Public IPv4 address
- Security Group

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
                             v
                       Public IPv4
```

### Practical Steps

1. Create or select a VPC.
2. Create a public subnet.
3. Create an Internet Gateway.
4. Attach the Internet Gateway to the VPC.
5. Create a Route Table.
6. Add the default route to the Internet Gateway.
7. Associate the Route Table with the public subnet.
8. Launch an EC2 instance in the public subnet.
9. Enable public IPv4 addressing when required.
10. Configure the Security Group.
11. Verify the network configuration.
12. Test connectivity.

### Result

**Successfully understood how an Internet Gateway, Route Table, public subnet, and EC2 instance work together to provide internet connectivity.**

---

## 8. Internet Gateway Does Not Provide a Public IP

### Explanation

An Internet Gateway does not automatically assign a public IP address to an EC2 instance.

The EC2 instance needs appropriate public IPv4 addressing.

The following components must work together:

```text
Internet Gateway
        +
Route Table
        +
Public Subnet
        +
Public IPv4 Address
        +
Security Group
        |
        v
Internet Connectivity
```

### Result

**Successfully understood that an Internet Gateway provides the network path but does not itself assign public IP addresses to EC2 instances.**

---

## 9. Internet Gateway vs NAT Gateway

### Explanation

An **Internet Gateway** and a **NAT Gateway** serve different purposes.

### Internet Gateway

Used to provide a direct internet path for resources configured for internet connectivity, such as resources in a public subnet.

```text
Public Subnet
     |
     v
Internet Gateway
     |
     v
Internet
```

### NAT Gateway

Used to allow resources in a private subnet to initiate outbound connections to the internet.

```text
Private Subnet
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

| Feature | Internet Gateway | NAT Gateway |
|---|---|---|
| VPC Component | Yes | Yes |
| Used by Public Subnet | Yes | No |
| Used by Private Subnet | Not directly for internet access | Yes |
| Provides Internet Path | Yes | Through IGW |
| Common Purpose | Internet connectivity | Outbound internet from private resources |

### Result

**Successfully understood the difference between an Internet Gateway and a NAT Gateway.**

---

## 10. Internet Gateway and Route Table

### Explanation

The Internet Gateway and Route Table work together.

The Internet Gateway provides the gateway between the VPC and internet, while the Route Table determines which traffic should be sent to the Internet Gateway.

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
     | 0.0.0.0/0
     v
Internet Gateway
     |
     v
Internet
```

### Result

**Successfully understood that both routing and gateway configuration are required for internet connectivity.**

---

## 11. Practical Lab - Create Internet Gateway

### Explanation

In this practical lab, an Internet Gateway is created and attached to a VPC.

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

Go to:

```text
VPC
   |
   v
Internet Gateways
```

Click:

```text
Create internet gateway
```

Enter:

```text
Name:
AWS-Lab-IGW
```

Create the Internet Gateway.

### Step 4 - Attach Internet Gateway

Select:

```text
AWS-Lab-IGW
```

Choose:

```text
Actions
   |
   v
Attach to a VPC
```

Select:

```text
AWS-Lab-VPC
```

Attach the Internet Gateway.

### Step 5 - Create Route Table

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

### Step 6 - Add Internet Route

Open:

```text
Routes
```

Add:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

Select:

```text
AWS-Lab-IGW
```

Save the route.

### Step 7 - Associate Public Subnet

Open:

```text
Subnet associations
```

Associate:

```text
Public-Subnet
```

with:

```text
Public-Route-Table
```

### Step 8 - Launch EC2

Launch an EC2 instance using:

```text
VPC:
AWS-Lab-VPC

Subnet:
Public-Subnet
```

Enable public IPv4 addressing when required.

### Step 9 - Configure Security Group

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

### Step 10 - Verify Connectivity

Check the complete path:

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
0.0.0.0/0
      |
      v
Internet Gateway
      |
      v
Internet
```

### Result

**Successfully created and configured an Internet Gateway and established the required routing path for internet connectivity from a public subnet.**

---

## 12. Internet Gateway Troubleshooting

### Explanation

If an EC2 instance in a public subnet cannot access the internet, several components should be checked.

### Troubleshooting Flow

```text
EC2 Cannot Access Internet
          |
          v
Check VPC
          |
          v
Check Public Subnet
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
Check Public IPv4
          |
          v
Check Security Group
          |
          v
Check Network ACL
```

### Practical Steps

1. Verify the EC2 instance is inside the correct VPC.
2. Verify that the EC2 instance is inside the intended public subnet.
3. Verify the subnet's Route Table.
4. Verify that the Route Table contains:

```text
0.0.0.0/0
```

5. Verify that the target is the correct Internet Gateway.
6. Verify that the Internet Gateway is attached to the VPC.
7. Verify that the EC2 instance has appropriate public IPv4 addressing.
8. Review the Security Group.
9. Review the Network ACL.
10. Test connectivity again.

### Result

**Successfully understood the basic troubleshooting process for Internet Gateway and public subnet connectivity problems.**

---

## 13. Internet Gateway Security

### Explanation

An Internet Gateway itself does not act as a firewall.

Network access must be controlled using other AWS security mechanisms such as:

- Security Groups
- Network ACLs
- IAM permissions where applicable
- Proper Route Tables

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
Security Group
   |
   v
EC2
```

### Security Best Practices

- Do not expose unnecessary services.
- Allow only required ports.
- Restrict SSH access.
- Restrict RDP access.
- Use private subnets for resources that do not require direct public access.
- Avoid unnecessary public IP addresses.
- Review Route Tables regularly.
- Monitor network traffic when required.

### Result

**Successfully understood that an Internet Gateway provides connectivity but security controls must be implemented using appropriate network security mechanisms.**

---

## 14. Internet Gateway Architecture

```text
                              AWS Cloud
                                  |
                                  v
                                VPC
                           10.0.0.0/16
                                  |
                    +-------------+-------------+
                    |                           |
                    v                           v
              Public Subnet               Private Subnet
              10.0.1.0/24                 10.0.2.0/24
                    |                           |
                    v                           v
             Public Route Table          Private Route Table
                    |                           |
                    v                           v
             Internet Gateway              NAT Gateway
                    |                           |
                    v                           v
                Internet                 Internet Gateway
```

---

## 15. Internet Gateway Traffic Flow

### Outbound Traffic

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
Internet Gateway
     |
     v
Internet
```

### Inbound Traffic

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

The actual traffic is also subject to the applicable security and network configuration.

### Result

**Successfully understood the basic inbound and outbound traffic flow through an Internet Gateway.**

---

## 16. Internet Gateway vs Route Table

### Explanation

An Internet Gateway and Route Table perform different functions.

### Internet Gateway

Provides:

```text
A gateway between the VPC and the internet.
```

### Route Table

Determines:

```text
Where network traffic should be sent.
```

### Example

```text
EC2
 |
 v
Route Table
 |
 | Determines destination
 v
Internet Gateway
 |
 v
Internet
```

### Result

**Successfully understood the difference between the routing function of a Route Table and the gateway function of an Internet Gateway.**

---

## 17. Complete Internet Gateway Workflow

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
Test Internet Connectivity
```

### Final Result

**Successfully completed Lab 08 - Internet Gateway and understood how an Internet Gateway connects a VPC to the internet. Learned how to create and attach an Internet Gateway, configure a public Route Table, add a default route, associate the Route Table with a public subnet, configure public IPv4 addressing, connect an EC2 instance, troubleshoot connectivity, and apply basic security practices.**
