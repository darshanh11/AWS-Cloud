# Lab 10 - Network ACL (NACL)

## Objective

The objective of this lab is to understand **Network Access Control Lists (NACLs)** in Amazon VPC and practically learn how to create, configure, associate, and use Network ACLs to control inbound and outbound traffic at the subnet level.

This lab covers:

- Network ACL
- Inbound Rules
- Outbound Rules
- Allow Rules
- Deny Rules
- Rule Numbers
- Protocols
- Ports
- Sources and Destinations
- Subnet Association
- Default Network ACL
- Custom Network ACL
- Stateless Nature
- Security Group vs Network ACL
- Practical Configuration
- Troubleshooting
- Security Best Practices
- NACL Architecture

---

## 1. What is a Network ACL?

### Explanation

A **Network Access Control List (NACL)** is a network-level security control that controls traffic entering and leaving a subnet in an Amazon VPC.

A Network ACL can contain:

- Inbound rules
- Outbound rules
- Allow rules
- Deny rules
- Rule numbers

Unlike Security Groups, Network ACLs operate at the **subnet level**.

### Example

```text
                    VPC
                     |
                     v
                  Subnet
                     |
                     v
                Network ACL
                 /        \
                v          v
          Inbound       Outbound
             |             |
             v             v
          Traffic       Traffic
```

### Result

**Successfully understood that a Network ACL provides subnet-level control over inbound and outbound network traffic.**

---

## 2. Network ACL Components

### Explanation

A Network ACL rule contains important information such as:

- Rule number
- Type
- Protocol
- Port range
- Source or destination
- Allow or Deny

Example:

```text
Rule Number:
100

Type:
HTTP

Protocol:
TCP

Port:
80

Source:
0.0.0.0/0

Action:
ALLOW
```

### Result

**Successfully understood the main components used to configure Network ACL rules.**

---

## 3. Inbound Rules

### Explanation

**Inbound Rules** control traffic entering a subnet.

Network ACL inbound rules determine whether incoming traffic should be allowed or denied.

### Example

```text
Internet
    |
    v
Network ACL
    |
    +---- HTTP : 80 ---> ALLOW
    |
    +---- SSH  : 22 ---> ALLOW
    |
    +---- Other -------> DENY
    |
    v
Subnet
```

### Practical Steps

1. Open the **AWS Management Console**.
2. Search for **VPC**.
3. Open the **VPC** service.
4. Select **Network ACLs**.
5. Select the required Network ACL.
6. Open the **Inbound rules** tab.
7. Click **Edit inbound rules**.
8. Add the required rule.
9. Enter the rule number.
10. Select the protocol.
11. Specify the port.
12. Specify the source CIDR.
13. Select **Allow** or **Deny**.
14. Save the rules.
15. Verify the inbound rules.

### Result

**Successfully configured inbound Network ACL rules and understood how incoming traffic to a subnet is controlled.**

---

## 4. Outbound Rules

### Explanation

**Outbound Rules** control traffic leaving a subnet.

Outbound rules determine whether traffic leaving the subnet should be allowed or denied.

### Example

```text
Subnet
   |
   v
Network ACL
   |
   +---- HTTP : 80 ---> ALLOW
   |
   +---- HTTPS : 443 -> ALLOW
   |
   +---- Other -------> DENY
   |
   v
Internet
```

### Practical Steps

1. Open the required Network ACL.
2. Select **Outbound rules**.
3. Click **Edit outbound rules**.
4. Add the required rule.
5. Enter the rule number.
6. Select the protocol.
7. Specify the port.
8. Specify the destination CIDR.
9. Select **Allow** or **Deny**.
10. Save the rules.
11. Verify the outbound configuration.

### Result

**Successfully configured outbound Network ACL rules and understood how outgoing subnet traffic is controlled.**

---

## 5. Allow Rule

### Explanation

An **Allow Rule** permits traffic that matches the rule.

Example:

```text
Rule:
100

Protocol:
TCP

Port:
80

Source:
0.0.0.0/0

Action:
ALLOW
```

This allows matching HTTP traffic according to the rule configuration.

### Example

```text
Traffic
   |
   v
NACL Rule 100
   |
   v
HTTP Port 80
   |
   v
ALLOW
```

### Result

**Successfully understood how an Allow rule permits matching network traffic.**

---

## 6. Deny Rule

### Explanation

A **Deny Rule** blocks traffic that matches the rule.

Example:

```text
Rule:
110

Protocol:
TCP

Port:
22

Source:
203.0.113.0/24

Action:
DENY
```

This blocks matching SSH traffic from the specified source range.

### Example

```text
Traffic
   |
   v
NACL Rule 110
   |
   v
SSH Port 22
   |
   v
DENY
```

### Result

**Successfully understood how a Deny rule blocks matching network traffic.**

---

## 7. Rule Numbers

### Explanation

Network ACL rules have **rule numbers**.

Rules are evaluated in ascending order, starting with the lowest rule number.

The first rule that matches the traffic is applied.

Example:

```text
Rule 100:
Allow HTTP

Rule 110:
Deny HTTP
```

HTTP traffic matches Rule 100 first, so it is allowed.

### Example

```text
Traffic
   |
   v
Rule 100
   |
   | Match?
   v
ALLOW
```

If the traffic does not match Rule 100:

```text
Rule 110
   |
   v
DENY
```

### Result

**Successfully understood how Network ACL rule numbers determine the order in which rules are evaluated.**

---

## 8. Default Network ACL

### Explanation

Every VPC automatically has a **default Network ACL**.

The default Network ACL is associated with subnets unless a different Network ACL is explicitly associated.

The default Network ACL allows all inbound and outbound traffic by default.

### Example

```text
VPC
 |
 v
Default Network ACL
 |
 +---- Inbound: ALLOW
 |
 +---- Outbound: ALLOW
 |
 v
Subnets
```

### Result

**Successfully understood the purpose of the default Network ACL and its default traffic behavior.**

---

## 9. Custom Network ACL

### Explanation

A **Custom Network ACL** can be created when more specific subnet-level traffic control is required.

A custom Network ACL can contain customized inbound and outbound rules.

### Practical Steps

1. Open **VPC**.
2. Select **Network ACLs**.
3. Click **Create network ACL**.
4. Enter a name.

Example:

```text
Custom-NACL
```

5. Select the VPC.
6. Click **Create network ACL**.
7. Verify the Network ACL.
8. Configure inbound rules.
9. Configure outbound rules.
10. Associate the Network ACL with the required subnet.

### Result

**Successfully created a custom Network ACL and understood how it can be used for customized subnet-level traffic control.**

---

## 10. Associating Network ACL with a Subnet

### Explanation

A Network ACL must be associated with a subnet to control traffic for that subnet.

### Example

```text
Network ACL
     |
     v
Subnet
     |
     v
EC2 Instance
```

### Practical Steps

1. Open **VPC > Network ACLs**.
2. Select the required Network ACL.
3. Open the **Subnet associations** tab.
4. Click **Edit subnet associations**.
5. Select the required subnet.
6. Save the association.
7. Verify that the subnet is associated with the Network ACL.

### Result

**Successfully associated a Network ACL with a subnet.**

---

## 11. Network ACL and EC2

### Explanation

An EC2 instance receives network protection from the Network ACL associated with its subnet.

The traffic path can be represented as:

```text
Internet
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

Both Network ACL rules and Security Group rules must permit the required traffic.

### Result

**Successfully understood how Network ACLs and Security Groups can work together to control traffic to an EC2 instance.**

---

## 12. Network ACL and Security Group

### Explanation

Network ACLs and Security Groups are both security mechanisms, but they operate at different levels.

### Network ACL

Controls traffic at the **subnet level**.

### Security Group

Controls traffic at the **resource/network-interface level**.

### Comparison

| Feature | Network ACL | Security Group |
|---|---|---|
| Level | Subnet | Resource / Network Interface |
| Stateful | No | Yes |
| Rules | Allow and Deny | Allow |
| Applies To | Subnet | Resource |
| Rule Evaluation | Rule number order | All applicable rules |
| Default | Default NACL allows traffic | Default SG allows outbound traffic and no inbound traffic |

### Architecture

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

**Successfully understood the difference between Network ACLs and Security Groups.**

---

## 13. Stateless Nature of Network ACL

### Explanation

Network ACLs are **stateless**.

This means inbound and outbound traffic are evaluated independently.

If inbound traffic is allowed, the response traffic must also be allowed by the outbound rules.

### Example

```text
Client
  |
  | Inbound Request
  v
Network ACL
  |
  v
EC2
  |
  | Outbound Response
  v
Network ACL
  |
  v
Client
```

Both directions need appropriate rules.

### Result

**Successfully understood that Network ACLs are stateless and that inbound and outbound traffic are evaluated independently.**

---

## 14. Port 22 - SSH

### Explanation

SSH commonly uses TCP port **22**.

It is commonly used for remote administration of Linux-based systems.

Example:

```text
Protocol:
TCP

Port:
22

Purpose:
SSH
```

### Practical Steps

1. Open the required Network ACL.
2. Open **Inbound rules**.
3. Add a rule.
4. Select TCP.
5. Enter port `22`.
6. Specify the trusted source CIDR.
7. Select **ALLOW**.
8. Save the rule.
9. Configure the required outbound response traffic.
10. Verify the rules.

### Result

**Successfully understood how a Network ACL can control SSH traffic at the subnet level.**

---

## 15. Port 80 - HTTP

### Explanation

HTTP commonly uses TCP port **80**.

It is commonly used for web traffic.

Example:

```text
Protocol:
TCP

Port:
80

Purpose:
HTTP
```

### Practical Steps

1. Open the required Network ACL.
2. Open **Inbound rules**.
3. Add a rule.
4. Select HTTP.
5. Verify port `80`.
6. Specify the required source.
7. Select **ALLOW**.
8. Save the rule.
9. Configure the required outbound traffic.
10. Verify the configuration.

### Result

**Successfully understood how a Network ACL can control HTTP traffic at the subnet level.**

---

## 16. Port 443 - HTTPS

### Explanation

HTTPS commonly uses TCP port **443**.

It is used for encrypted web traffic.

Example:

```text
Protocol:
TCP

Port:
443

Purpose:
HTTPS
```

### Result

**Successfully understood how a Network ACL can control HTTPS traffic at the subnet level.**

---

## 17. Practical Lab - Create Custom Network ACL

### Explanation

In this practical lab, a custom Network ACL is created and associated with a subnet.

### Practical Steps

### Step 1 - Open VPC

1. Sign in to AWS.
2. Search for **VPC**.
3. Open the VPC service.
4. Select **Network ACLs**.

### Step 2 - Create Network ACL

Click:

```text
Create network ACL
```

Enter:

```text
Name:
AWS-Lab-NACL
```

Select:

```text
VPC:
AWS-Lab-VPC
```

Click:

```text
Create network ACL
```

### Step 3 - Configure Inbound Rule

Open:

```text
Inbound rules
```

Add:

```text
Rule Number:
100

Type:
HTTP

Protocol:
TCP

Port:
80

Source:
0.0.0.0/0

Action:
ALLOW
```

Save the rule.

### Step 4 - Configure SSH Rule

Add:

```text
Rule Number:
110

Type:
SSH

Protocol:
TCP

Port:
22

Source:
Trusted IP Address

Action:
ALLOW
```

Save the rule.

### Step 5 - Configure Outbound Rules

Open:

```text
Outbound rules
```

Configure the required outbound rules.

Example:

```text
Rule Number:
100

Protocol:
All

Destination:
0.0.0.0/0

Action:
ALLOW
```

Save the rule.

### Step 6 - Associate Subnet

Open:

```text
Subnet associations
```

Click:

```text
Edit subnet associations
```

Select:

```text
Public-Subnet
```

Save the association.

### Step 7 - Verify

Check:

```text
AWS-Lab-NACL
       |
       v
Public-Subnet
       |
       v
EC2 Instance
```

### Result

**Successfully created a custom Network ACL, configured inbound and outbound rules, and associated the Network ACL with a subnet.**

---

## 18. Practical Lab - Deny Specific Traffic

### Explanation

Network ACLs can be used to deny specific traffic.

Example:

```text
Rule Number:
120

Protocol:
TCP

Port:
22

Source:
203.0.113.0/24

Action:
DENY
```

### Practical Steps

1. Open the custom Network ACL.
2. Open **Inbound rules**.
3. Click **Edit inbound rules**.
4. Add a new rule.
5. Enter a rule number lower than any broader allow rule that would otherwise match the same traffic.
6. Select TCP.
7. Enter port `22`.
8. Enter the source CIDR.
9. Select **DENY**.
10. Save the rule.
11. Review the rule order.
12. Verify the configuration.

### Result

**Successfully understood how a Network ACL can deny specific traffic using a deny rule and rule ordering.**

---

## 19. Network ACL Rule Evaluation

### Explanation

Network ACL rules are evaluated from the lowest rule number to the highest rule number.

The first matching rule determines whether traffic is allowed or denied.

Example:

```text
Rule 100:
Allow HTTP from 0.0.0.0/0

Rule 110:
Deny HTTP from 203.0.113.0/24
```

If the deny rule is intended to override the broad allow rule, it must be evaluated first.

Correct example:

```text
Rule 100:
Deny HTTP from 203.0.113.0/24

Rule 110:
Allow HTTP from 0.0.0.0/0
```

Traffic from the denied CIDR matches Rule 100 first and is denied.

### Result

**Successfully understood the importance of Network ACL rule numbers and rule evaluation order.**

---

## 20. Ephemeral Ports

### Explanation

When using Network ACLs, response traffic must also be allowed because Network ACLs are stateless.

For client connections, response traffic often uses ephemeral ports.

Therefore, NACL rules may need to allow the appropriate ephemeral port range depending on the application and traffic pattern.

Example:

```text
Client
   |
   | Request
   | Port 80
   v
EC2
   |
   | Response
   | Ephemeral Port
   v
Client
```

### Result

**Successfully understood why Network ACL configurations may need appropriate ephemeral-port rules for return traffic.**

---

## 21. Network ACL Troubleshooting

### Explanation

If traffic is not reaching an EC2 instance, the Network ACL should be checked along with the other network components.

Important items include:

- Correct Network ACL
- Correct subnet association
- Inbound rules
- Outbound rules
- Rule numbers
- Protocol
- Port
- Source
- Destination
- Security Group
- Route Table
- Internet Gateway
- Public IP

### Troubleshooting Flow

```text
Traffic Not Working
       |
       v
Check Subnet
       |
       v
Check Network ACL
       |
       v
Check Inbound Rules
       |
       v
Check Outbound Rules
       |
       v
Check Rule Numbers
       |
       v
Check Security Group
       |
       v
Check Route Table
       |
       v
Check Internet Gateway
       |
       v
Test Again
```

### Result

**Successfully understood the basic troubleshooting process for Network ACL connectivity problems.**

---

## 22. Network ACL Security Best Practices

### Explanation

Network ACLs should be configured carefully to avoid unnecessary network exposure.

Important practices include:

- Allow only required traffic.
- Deny unwanted traffic where appropriate.
- Use appropriate rule numbers.
- Keep rules simple and understandable.
- Review inbound rules regularly.
- Review outbound rules regularly.
- Restrict administrative ports.
- Use Security Groups for resource-level security.
- Use private subnets for sensitive resources.
- Monitor and review network traffic.

### Result

**Successfully understood important Network ACL security practices and the importance of controlling subnet-level traffic.**

---

## 23. Network ACL Architecture

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
                           Network ACL
                         +----------------+
                         | Inbound Rules  |
                         | Outbound Rules |
                         +----------------+
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

---

## 24. Network ACL Traffic Flow

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
Network ACL
    |
    | Inbound Rule
    v
Subnet
    |
    v
Security Group
    |
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
    v
Subnet
    |
    v
Network ACL
    |
    | Outbound Rule
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

**Successfully understood how inbound and outbound traffic passes through Network ACLs at the subnet level.**

---

## 25. Network ACL vs Security Group - Practical Example

### Scenario

A web server is running in a public subnet.

Required traffic:

```text
HTTP:
Port 80

HTTPS:
Port 443

SSH:
Port 22
```

### Security Group

```text
HTTP 80  -> Allow
HTTPS 443 -> Allow
SSH 22   -> Allow from trusted IP
```

### Network ACL

```text
HTTP 80  -> Allow
HTTPS 443 -> Allow
SSH 22   -> Allow from trusted IP
Required return traffic -> Allow
```

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
Network ACL
    |
    v
Public Subnet
    |
    v
Security Group
    |
    v
EC2 Web Server
```

### Result

**Successfully understood how Network ACLs and Security Groups can provide layered network security for an EC2 web server.**

---

## 26. Complete Network ACL Workflow

### Workflow

```text
Create VPC
    |
    v
Create Subnet
    |
    v
Create Network ACL
    |
    v
Configure Inbound Rules
    |
    v
Configure Outbound Rules
    |
    v
Associate Network ACL
    |
    v
Subnet
    |
    v
Configure Security Group
    |
    v
Launch EC2
    |
    v
Configure Route Table
    |
    v
Configure Internet Gateway
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
3. Create a custom Network ACL.
4. Configure inbound rules.
5. Configure outbound rules.
6. Assign appropriate rule numbers.
7. Associate the Network ACL with the subnet.
8. Configure the Security Group.
9. Configure the Route Table.
10. Configure the Internet Gateway when internet connectivity is required.
11. Launch the EC2 instance.
12. Test the required network traffic.
13. Review Network ACL rules.
14. Review Security Group rules.
15. Troubleshoot any blocked traffic.
16. Remove unnecessary rules after completing the lab.

### Final Result

**Successfully completed Lab 10 - Network ACL and understood how Network ACLs provide subnet-level network security in Amazon VPC. Learned how to create and configure Network ACLs, manage inbound and outbound rules, use Allow and Deny rules, understand rule numbers and evaluation order, associate NACLs with subnets, understand the stateless nature of NACLs, configure traffic for common ports, compare Network ACLs with Security Groups, troubleshoot network connectivity, and apply Network ACL security best practices.**
