# Lab 11 - Elastic IP Address

## Objective

The objective of this lab is to understand **Elastic IP (EIP)** in AWS and practically learn how to allocate, associate, disassociate, and release an Elastic IP address for an EC2 instance.

This lab covers:

- Elastic IP Address
- Public IPv4 Address
- Private IPv4 Address
- Elastic IP Allocation
- Elastic IP Association
- Elastic IP Disassociation
- Elastic IP Release
- EC2 and Elastic IP
- Elastic IP and Internet Gateway
- Elastic IP and NAT Gateway
- Static Public IP
- Elastic IP Architecture
- Practical Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is an Elastic IP?

### Explanation

An **Elastic IP (EIP)** is a static public IPv4 address that can be allocated to your AWS account and associated with an AWS resource such as an EC2 instance or a NAT Gateway.

Unlike an automatically assigned public IPv4 address, an Elastic IP is designed to remain associated with your AWS account until you release it.

Elastic IP addresses are useful when you need a consistent public IPv4 address.

### Example

```text
EC2 Instance
     |
     v
Elastic IP
     |
     v
Internet
```

### Result

**Successfully understood that an Elastic IP is a static public IPv4 address that can be associated with supported AWS resources.**

---

## 2. Public IPv4 Address vs Elastic IP

### Explanation

An EC2 instance can receive a public IPv4 address automatically when configured to do so.

An automatically assigned public IPv4 address can change when the instance is stopped and started.

An Elastic IP provides a persistent public IPv4 address that can be moved between supported resources when required.

### Comparison

| Feature | Public IPv4 Address | Elastic IP |
|---|---|---|
| Public Address | Yes | Yes |
| Static | No | Yes |
| Can be reassociated | Limited | Yes |
| Controlled by AWS account | No | Yes |
| Common Use | Temporary/public connectivity | Stable public IP requirement |

### Example

```text
Normal Public IP:

EC2
 |
 +---- Public IPv4
       |
       v
    Internet


Elastic IP:

EC2
 |
 +---- Elastic IP
       |
       v
    Internet
```

### Result

**Successfully understood the difference between an automatically assigned public IPv4 address and an Elastic IP address.**

---

## 3. Elastic IP Allocation

### Explanation

Before using an Elastic IP, it must be **allocated** to your AWS account.

Allocation reserves an Elastic IP address for your account.

### Practical Steps

1. Sign in to the **AWS Management Console**.
2. Search for **EC2**.
3. Open the **EC2** service.
4. Select **Elastic IPs** under **Network & Security**.
5. Click **Allocate Elastic IP address**.
6. Keep the default IPv4 address settings unless your requirements are different.
7. Click **Allocate**.
8. Verify that the Elastic IP appears in the list.

### Example

```text
Elastic IP:
203.0.113.10

Status:
Allocated
```

### Result

**Successfully allocated an Elastic IP address to the AWS account.**

---

## 4. Associating Elastic IP with EC2

### Explanation

After allocating an Elastic IP, it can be associated with an EC2 instance or another supported resource.

Association assigns the Elastic IP to the selected resource.

### Practical Steps

1. Open **EC2 > Elastic IPs**.
2. Select the allocated Elastic IP.
3. Click **Actions**.
4. Select **Associate Elastic IP address**.
5. Select the resource type.
6. Select the required EC2 instance or network interface.
7. Select the private IP address when required.
8. Click **Associate**.
9. Verify the association.

### Example

```text
Elastic IP
203.0.113.10
     |
     v
EC2 Instance
     |
     v
Private IP
10.0.1.10
```

### Result

**Successfully associated an Elastic IP address with an EC2 instance.**

---

## 5. Elastic IP and EC2 Architecture

### Explanation

An Elastic IP provides a stable public IPv4 address for an EC2 instance.

The EC2 instance still has a private IPv4 address inside the VPC.

### Architecture

```text
                         Internet
                             |
                             v
                       Elastic IP
                       203.0.113.10
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
                             |
                             v
                      Private IP Address
                         10.0.1.10
```

### Result

**Successfully understood how an Elastic IP provides a stable public IPv4 address while the EC2 instance continues to use a private IP inside the VPC.**

---

## 6. Elastic IP and Internet Gateway

### Explanation

An Elastic IP is used with the VPC networking architecture to provide public IPv4 connectivity.

For an EC2 instance to communicate with the internet, the VPC must have the appropriate Internet Gateway and Route Table configuration.

### Example

```text
EC2
 |
 v
Private IP
 |
 v
Elastic IP
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

### Result

**Successfully understood how Elastic IP, Route Tables, and Internet Gateway work together to provide public IPv4 connectivity.**

---

## 7. Elastic IP and Public Subnet

### Explanation

An EC2 instance using an Elastic IP is normally placed in a subnet with appropriate routing to an Internet Gateway for internet connectivity.

A public subnet requires a Route Table containing an appropriate route to the Internet Gateway.

### Example

```text
VPC
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

### Practical Steps

1. Create or select a VPC.
2. Create or select a public subnet.
3. Verify the Route Table.
4. Verify that the Route Table has:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

5. Launch or select an EC2 instance.
6. Allocate an Elastic IP.
7. Associate the Elastic IP with the EC2 instance.
8. Verify the configuration.

### Result

**Successfully understood how an Elastic IP can be used with an EC2 instance in a properly configured public subnet.**

---

## 8. Elastic IP and NAT Gateway

### Explanation

A **NAT Gateway** can use an Elastic IP address for its public-facing IPv4 address.

This allows resources in private subnets to access the internet through the NAT Gateway.

### Architecture

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
Elastic IP
     |
     v
Internet Gateway
     |
     v
Internet
```

### Practical Steps

1. Open the VPC service.
2. Select **NAT Gateways**.
3. Create a NAT Gateway in a public subnet.
4. Allocate or select an Elastic IP address.
5. Create the NAT Gateway.
6. Configure the private subnet Route Table.
7. Add the NAT Gateway as the target for the required outbound route.
8. Verify the NAT Gateway configuration.

### Result

**Successfully understood how an Elastic IP can be used by a NAT Gateway to provide outbound internet connectivity for private subnet resources.**

---

## 9. Elastic IP Disassociation

### Explanation

An Elastic IP can be disassociated from a resource without releasing the Elastic IP from the AWS account.

After disassociation, the Elastic IP remains allocated to the account.

### Practical Steps

1. Open **EC2 > Elastic IPs**.
2. Select the Elastic IP.
3. Click **Actions**.
4. Select **Disassociate Elastic IP address**.
5. Confirm the disassociation.
6. Verify that the Elastic IP is no longer associated with the resource.

### Example

```text
Before:

Elastic IP
    |
    v
EC2


After:

Elastic IP

    X

EC2
```

The Elastic IP remains allocated to the account.

### Result

**Successfully disassociated an Elastic IP from an EC2 resource while keeping the Elastic IP allocated to the account.**

---

## 10. Elastic IP Release

### Explanation

When an Elastic IP is no longer required, it should be released.

Releasing the Elastic IP returns it to the AWS pool.

Once released, the address cannot be assumed to remain available for future use.

### Practical Steps

1. Open **EC2 > Elastic IPs**.
2. Select the unused Elastic IP.
3. Click **Actions**.
4. Select **Release Elastic IP address**.
5. Confirm the release.
6. Verify that the Elastic IP has been removed from the allocated addresses.

### Example

```text
Allocated Elastic IP
       |
       v
Disassociate
       |
       v
Release
       |
       v
AWS Address Pool
```

### Result

**Successfully understood how to release an unused Elastic IP address.**

---

## 11. Elastic IP and EC2 Failure

### Explanation

One benefit of an Elastic IP is that it can be reassociated with another supported resource when required.

This can be useful when replacing or recovering an EC2 instance.

### Example

```text
Elastic IP
203.0.113.10
      |
      +----------+
      |          |
      v          v
    EC2-A      EC2-B
```

The Elastic IP can be moved from one supported resource to another when the network configuration allows it.

### Result

**Successfully understood how an Elastic IP can provide a stable public endpoint that can be reassociated when required.**

---

## 12. Elastic IP and DNS

### Explanation

A stable public IP can be useful when an application requires a consistent network endpoint.

DNS can be configured to point a domain name to a stable public address depending on the architecture.

Example:

```text
Domain Name
example.com
     |
     v
Elastic IP
     |
     v
EC2 Instance
```

### Result

**Successfully understood how a stable public IP can be used as part of a DNS-based application architecture.**

---

## 13. Elastic IP and Security Group

### Explanation

An Elastic IP provides an address, but it does not control which traffic is allowed.

A Security Group controls network traffic to and from the EC2 resource.

### Example

```text
Internet
    |
    v
Elastic IP
    |
    v
Security Group
    |
    v
EC2 Instance
```

### Practical Steps

1. Associate an Elastic IP with the EC2 instance.
2. Open the EC2 instance's Security Group.
3. Review inbound rules.
4. Allow only the required ports.
5. Review outbound rules.
6. Save any required changes.
7. Test the required connectivity.

### Result

**Successfully understood that Elastic IP provides public addressing while Security Groups control the allowed network traffic.**

---

## 14. Elastic IP and Private IP

### Explanation

An EC2 instance can have a private IPv4 address inside the VPC and an Elastic IP associated with it for public IPv4 connectivity.

### Example

```text
EC2 Instance
     |
     +---- Private IP
     |     10.0.1.10
     |
     +---- Elastic IP
           203.0.113.10
```

The private IP is used for communication inside the VPC.

The Elastic IP provides a stable public IPv4 address.

### Result

**Successfully understood the difference between private IPv4 addressing and Elastic IP addressing.**

---

## 15. Elastic IP Practical Lab

### Explanation

In this practical lab, an Elastic IP is allocated and associated with an EC2 instance.

### Practical Steps

### Step 1 - Launch EC2

Launch an EC2 instance inside the required VPC and subnet.

Example:

```text
VPC:
AWS-Lab-VPC

Subnet:
Public-Subnet
```

### Step 2 - Open Elastic IP

Go to:

```text
EC2
   |
   v
Network & Security
   |
   v
Elastic IPs
```

### Step 3 - Allocate Elastic IP

Click:

```text
Allocate Elastic IP address
```

Click:

```text
Allocate
```

Verify:

```text
Status:
Allocated
```

### Step 4 - Associate Elastic IP

Select the Elastic IP.

Choose:

```text
Actions
   |
   v
Associate Elastic IP address
```

Select:

```text
Resource:
EC2 Instance
```

Select the required EC2 instance.

Click:

```text
Associate
```

### Step 5 - Verify EC2

Open:

```text
EC2
   |
   v
Instances
   |
   v
Select Instance
```

Check:

```text
Public IPv4 Address
```

Verify that the Elastic IP is displayed.

### Step 6 - Verify Network Configuration

Check:

```text
EC2
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

### Step 7 - Test Connectivity

Verify the required connectivity according to the configured Security Group rules.

### Result

**Successfully allocated and associated an Elastic IP with an EC2 instance and verified the public IPv4 network configuration.**

---

## 16. Elastic IP Disassociation Practical Lab

### Practical Steps

1. Open **EC2 > Elastic IPs**.
2. Select the Elastic IP.
3. Click **Actions**.
4. Select **Disassociate Elastic IP address**.
5. Confirm the action.
6. Verify that the Elastic IP is no longer associated with the EC2 instance.
7. Confirm that the Elastic IP remains allocated.

### Result

**Successfully disassociated the Elastic IP from the EC2 instance while retaining the allocation.**

---

## 17. Elastic IP Release Practical Lab

### Practical Steps

1. Open **EC2 > Elastic IPs**.
2. Select an Elastic IP that is no longer required.
3. Click **Actions**.
4. Select **Release Elastic IP address**.
5. Confirm the release.
6. Verify that the Elastic IP is no longer allocated.

### Result

**Successfully released an unused Elastic IP address.**

---

## 18. Elastic IP Troubleshooting

### Explanation

If an EC2 instance cannot be accessed using its Elastic IP, check the complete network configuration.

Important items include:

- Elastic IP association
- EC2 instance state
- Public subnet
- Route Table
- Internet Gateway
- Security Group
- Network ACL
- Application/service
- Listening port

### Troubleshooting Flow

```text
Cannot Access EC2 Using Elastic IP
              |
              v
      Check Elastic IP
              |
              v
    Check EC2 Association
              |
              v
       Check Public Subnet
              |
              v
        Check Route Table
              |
              v
     Check Internet Gateway
              |
              v
      Check Security Group
              |
              v
        Check Network ACL
              |
              v
       Check Application
              |
              v
          Test Again
```

### Result

**Successfully understood the basic troubleshooting process for Elastic IP connectivity problems.**

---

## 19. Elastic IP Security Best Practices

### Explanation

An Elastic IP is a public address and should be protected using appropriate network security controls.

Important practices include:

- Use Elastic IPs only when a stable public IPv4 address is required.
- Restrict Security Group inbound rules.
- Avoid opening unnecessary ports.
- Restrict SSH access to trusted sources.
- Restrict RDP access to trusted sources.
- Use private subnets for resources that do not require direct public access.
- Release unused Elastic IPs.
- Monitor public-facing resources.
- Review network configuration regularly.

### Example

```text
Internet
    |
    v
Elastic IP
    |
    v
Security Group
    |
    v
Public EC2
    |
    v
Application
```

### Result

**Successfully understood important security practices for resources using Elastic IP addresses.**

---

## 20. Elastic IP Architecture

```text
                              Internet
                                  |
                                  v
                             Elastic IP
                                  |
                                  v
                          Internet Gateway
                                  |
                                  v
                                VPC
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
                            EC2 Instance
                                  |
                                  v
                            Private IP
                           10.0.1.10
```

---

## 21. Elastic IP Complete Workflow

### Workflow

```text
Launch EC2
    |
    v
Create / Select Public Subnet
    |
    v
Configure Route Table
    |
    v
Attach Internet Gateway
    |
    v
Allocate Elastic IP
    |
    v
Associate Elastic IP
    |
    v
Configure Security Group
    |
    v
Verify EC2
    |
    v
Test Connectivity
    |
    v
Disassociate When Required
    |
    v
Release When No Longer Required
```

### Practical Steps

1. Create or select a VPC.
2. Create or select a public subnet.
3. Configure the Route Table.
4. Attach an Internet Gateway to the VPC.
5. Add the appropriate default route.
6. Launch an EC2 instance.
7. Configure the Security Group.
8. Allocate an Elastic IP.
9. Associate the Elastic IP with the EC2 instance.
10. Verify the public IPv4 address.
11. Test the required connectivity.
12. Disassociate the Elastic IP when it is no longer required for the resource.
13. Release the Elastic IP when it is no longer required.
14. Verify the final AWS resource configuration.

### Final Result

**Successfully completed Lab 11 - Elastic IP and understood how Elastic IP addresses provide stable public IPv4 addressing in AWS. Learned how to allocate, associate, disassociate, and release Elastic IPs, how Elastic IPs work with EC2, Public Subnets, Route Tables, Internet Gateways, NAT Gateways, Security Groups, and private IP addresses, and how to troubleshoot and securely manage Elastic IP resources.**
