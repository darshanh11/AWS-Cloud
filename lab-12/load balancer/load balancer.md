# Lab 12 - Load Balancer

## Objective

The objective of this lab is to understand **AWS Elastic Load Balancing (ELB)** and practically learn how a Load Balancer distributes incoming traffic across multiple servers.

This lab covers:

- Load Balancer
- Elastic Load Balancing
- Application Load Balancer
- Network Load Balancer
- Target Groups
- Listeners
- Listener Rules
- EC2 Instances
- Health Checks
- Public Load Balancer
- Availability Zones
- Security Groups
- Traffic Distribution
- High Availability
- Practical Load Balancer Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is a Load Balancer?

### Explanation

A **Load Balancer** distributes incoming application traffic across multiple targets such as EC2 instances.

Instead of users directly connecting to one server, they connect to the Load Balancer.

The Load Balancer then forwards the requests to healthy backend targets.

### Example

```text
                         Users
                           |
                           v
                     Load Balancer
                           |
              +------------+------------+
              |                         |
              v                         v
          EC2 Instance 1           EC2 Instance 2
              |                         |
              v                         v
          Application              Application
```

### Result

**Successfully understood that a Load Balancer distributes incoming traffic across multiple backend targets.**

---

## 2. Why is a Load Balancer Used?

### Explanation

A Load Balancer can improve:

- Availability
- Scalability
- Fault tolerance
- Traffic distribution
- Application reliability

If one backend server becomes unhealthy, the Load Balancer can stop sending new requests to that unhealthy target when health checks identify it as unhealthy.

### Example

```text
                    Load Balancer
                         |
             +-----------+-----------+
             |                       |
             v                       v
         EC2 Server 1           EC2 Server 2
          Healthy                  Healthy
             |                       |
             +-----------+-----------+
                         |
                    Application
```

If one server becomes unhealthy:

```text
                    Load Balancer
                         |
             +-----------+-----------+
             |                       |
             v                       v
         EC2 Server 1           EC2 Server 2
          Unhealthy                Healthy
             X                       |
                                     v
                               Application
```

### Result

**Successfully understood how a Load Balancer improves application availability by distributing traffic across healthy targets.**

---

## 3. Types of AWS Load Balancers

### Explanation

AWS Elastic Load Balancing provides different types of Load Balancers.

The main types are:

```text
Application Load Balancer (ALB)
Network Load Balancer (NLB)
Gateway Load Balancer (GWLB)
Classic Load Balancer (CLB)
```

For modern application architectures, **Application Load Balancer** and **Network Load Balancer** are commonly used depending on the traffic requirements.

### Result

**Successfully understood the major types of AWS Load Balancers.**

---

## 4. Application Load Balancer (ALB)

### Explanation

An **Application Load Balancer (ALB)** operates at the application layer and is designed for HTTP and HTTPS traffic.

ALB supports features such as:

- Path-based routing
- Host-based routing
- HTTP/HTTPS listeners
- Target Groups
- Health Checks

### Example

```text
                         Users
                           |
                           v
                    Application
                   Load Balancer
                           |
                 +---------+---------+
                 |                   |
                 v                   v
             Web Server 1        Web Server 2
                 |                   |
                 v                   v
             Application         Application
```

### Result

**Successfully understood the purpose of an Application Load Balancer for HTTP and HTTPS application traffic.**

---

## 5. Network Load Balancer (NLB)

### Explanation

A **Network Load Balancer (NLB)** operates at the network layer and is designed for high-performance TCP, TLS, UDP, and related traffic.

NLB is useful when applications require high performance, low latency, or protocols beyond standard HTTP/HTTPS application-layer routing.

### Example

```text
                    Client
                       |
                       v
               Network Load Balancer
                       |
              +--------+--------+
              |                 |
              v                 v
           EC2-01            EC2-02
```

### Result

**Successfully understood the purpose of a Network Load Balancer and how it differs from an Application Load Balancer.**

---

## 6. Application Load Balancer vs Network Load Balancer

### Comparison

| Feature | ALB | NLB |
|---|---|---|
| Layer | Application Layer | Network Layer |
| Common Traffic | HTTP/HTTPS | TCP/TLS/UDP |
| Path-Based Routing | Yes | No |
| Host-Based Routing | Yes | No |
| Target Groups | Yes | Yes |
| Health Checks | Yes | Yes |
| Common Use | Web Applications | High-performance Network Traffic |

### Result

**Successfully understood the difference between Application Load Balancer and Network Load Balancer.**

---

## 7. What is a Target Group?

### Explanation

A **Target Group** contains the backend resources that receive traffic from a Load Balancer.

Targets can include supported resources such as:

- EC2 instances
- IP addresses
- Lambda functions for supported ALB configurations

For an EC2-based lab, the Target Group can contain multiple EC2 instances.

### Example

```text
                  Load Balancer
                        |
                        v
                   Target Group
                  /            \
                 v              v
             EC2-01          EC2-02
```

### Result

**Successfully understood that a Target Group defines the backend targets that receive traffic from a Load Balancer.**

---

## 8. What is a Listener?

### Explanation

A **Listener** checks for connection requests on a configured protocol and port.

For an Application Load Balancer, common listeners include:

```text
HTTP  : 80
HTTPS : 443
```

The listener forwards traffic to a Target Group according to its configuration and rules.

### Example

```text
User
 |
 v
Load Balancer
 |
 v
Listener
 |
 | HTTP : 80
 v
Target Group
 |
 +---- EC2-01
 |
 +---- EC2-02
```

### Result

**Successfully understood that a Listener receives traffic on a configured port and forwards it according to its rules.**

---

## 9. What is a Listener Rule?

### Explanation

A Listener Rule determines how incoming requests should be handled.

For an Application Load Balancer, rules can be based on conditions such as:

- Host
- Path
- HTTP headers
- Query parameters
- Source IP address

### Example

```text
Request
   |
   v
Listener
   |
   +---- /app/* ------> App Target Group
   |
   +---- /api/* ------> API Target Group
```

### Result

**Successfully understood how Listener Rules can route application requests to different Target Groups.**

---

## 10. Health Checks

### Explanation

A Load Balancer uses **Health Checks** to determine whether targets are healthy and able to receive traffic.

For an HTTP application, a health check can use a path such as:

```text
/
```

or:

```text
/health
```

The exact path depends on the application.

### Example

```text
                  Target Group
                 /            \
                v              v
            EC2-01           EC2-02
            Healthy         Unhealthy
                |               X
                v
             Receives         No new
              traffic         traffic
```

### Practical Steps

1. Open the **EC2** service.
2. Select **Target Groups**.
3. Select the required Target Group.
4. Open the **Health checks** section.
5. Configure the protocol.
6. Configure the health check port.
7. Configure the health check path.
8. Save the configuration.
9. Open the **Targets** tab.
10. Check the health status.

### Result

**Successfully configured and reviewed Load Balancer health checks for backend targets.**

---

## 11. Load Balancer and Availability Zones

### Explanation

A Load Balancer can distribute traffic across targets in multiple Availability Zones.

Using multiple Availability Zones can improve application availability and resilience.

### Example

```text
                         Load Balancer
                              |
                +-------------+-------------+
                |                           |
                v                           v
        Availability Zone A        Availability Zone B
                |                           |
                v                           v
             EC2-01                      EC2-02
```

### Result

**Successfully understood how multiple Availability Zones can be used with Load Balancers to improve availability.**

---

## 12. Load Balancer Security Group

### Explanation

A Load Balancer can have a Security Group associated with it.

For a public web application, the Load Balancer Security Group can allow the required web traffic.

Example:

```text
Load Balancer Security Group

Inbound:
HTTP  : 80
HTTPS : 443
```

Backend EC2 Security Groups can then be configured to allow application traffic from the Load Balancer's Security Group rather than directly from the internet.

### Architecture

```text
Internet
    |
    v
Load Balancer SG
    |
    v
Load Balancer
    |
    v
EC2 Security Group
    |
    v
EC2 Instance
```

### Result

**Successfully understood how Security Groups can be used to secure traffic between users, the Load Balancer, and backend EC2 instances.**

---

## 13. Load Balancer Traffic Flow

### Explanation

The Load Balancer acts as the entry point for client requests.

### Traffic Flow

```text
Client
  |
  v
Internet
  |
  v
Load Balancer
  |
  v
Listener
  |
  v
Target Group
  |
  +------------+
  |            |
  v            v
EC2-01       EC2-02
  |            |
  +------------+
       |
       v
   Application
```

### Result

**Successfully understood the complete traffic flow through a Load Balancer.**

---

## 14. Creating a Target Group

### Explanation

Before configuring the Load Balancer listener, a Target Group can be created to contain the backend EC2 instances.

### Practical Steps

1. Open **EC2**.
2. Select **Target Groups**.
3. Click **Create target group**.
4. Select the target type.

For an EC2 lab:

```text
Target type:
Instances
```

5. Enter a Target Group name.

Example:

```text
AWS-Web-TG
```

6. Select the VPC.
7. Select the protocol.

Example:

```text
HTTP
```

8. Configure the target port.

Example:

```text
80
```

9. Configure the health check.
10. Click **Next**.
11. Select the EC2 instances.
12. Select the appropriate ports.
13. Register the targets.
14. Create the Target Group.
15. Verify the registered targets.

### Result

**Successfully created a Target Group and registered EC2 instances as backend targets.**

---

## 15. Creating an Application Load Balancer

### Explanation

An Application Load Balancer can be created to distribute HTTP or HTTPS application traffic across registered targets.

### Practical Steps

1. Open **EC2**.
2. Select **Load Balancers**.
3. Click **Create Load Balancer**.
4. Select:

```text
Application Load Balancer
```

5. Enter a Load Balancer name.

Example:

```text
AWS-Web-ALB
```

6. Select:

```text
Scheme:
Internet-facing
```

when a public web application is required.

7. Select the required IP address type.
8. Select the VPC.
9. Select subnets in the required Availability Zones.
10. Configure the Load Balancer Security Group.
11. Configure the listener.
12. Select the previously created Target Group.
13. Review the configuration.
14. Click **Create Load Balancer**.
15. Wait for the Load Balancer to become available.

### Result

**Successfully created an Application Load Balancer and configured it to receive application traffic.**

---

## 16. Configuring HTTP Listener

### Explanation

An HTTP Listener receives HTTP traffic on port 80 and forwards it to the configured Target Group.

### Example

```text
Listener:
HTTP

Port:
80

Default Action:
Forward to AWS-Web-TG
```

### Practical Steps

1. Open the Load Balancer.
2. Open the **Listeners and rules** section.
3. Select the HTTP listener.
4. Review the listener port.
5. Verify:

```text
Protocol:
HTTP

Port:
80
```

6. Verify the default action.
7. Confirm that traffic is forwarded to the correct Target Group.

### Result

**Successfully configured and verified an HTTP Listener forwarding traffic to the Target Group.**

---

## 17. Configuring HTTPS Listener

### Explanation

HTTPS uses port 443 and encrypts traffic between clients and the Load Balancer when configured with an appropriate certificate.

### Example

```text
Listener:
HTTPS

Port:
443

Certificate:
Configured TLS Certificate

Default Action:
Forward to Target Group
```

### Practical Steps

1. Open the Load Balancer.
2. Select **Listeners and rules**.
3. Add or configure an HTTPS listener.
4. Select port:

```text
443
```

5. Configure the required certificate.
6. Select the Target Group.
7. Save the configuration.
8. Verify the HTTPS listener.

### Result

**Successfully understood how an HTTPS listener can be configured for encrypted client-to-Load-Balancer traffic.**

---

## 18. Registering EC2 Instances

### Explanation

EC2 instances must be registered with the Target Group so the Load Balancer can forward traffic to them.

### Practical Steps

1. Open **EC2 > Target Groups**.
2. Select the Target Group.
3. Open the **Targets** tab.
4. Click **Register targets**.
5. Select the EC2 instances.
6. Select the application port.
7. Add the instances to the registered targets.
8. Complete the registration.
9. Wait for the health checks.
10. Verify the target status.

### Example

```text
Target Group
     |
     +---- EC2-01 -> Healthy
     |
     +---- EC2-02 -> Healthy
```

### Result

**Successfully registered EC2 instances with the Target Group and verified their health status.**

---

## 19. Practical Lab - Complete Load Balancer

### Explanation

In this practical lab, two EC2 instances are placed behind an Application Load Balancer.

### Architecture

```text
                         Internet
                             |
                             v
                    Application Load Balancer
                             |
                         HTTP : 80
                             |
                             v
                       Target Group
                       /           \
                      v             v
                  EC2-01          EC2-02
                  Healthy         Healthy
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

### Step 2 - Create Public Subnets

Create subnets in appropriate Availability Zones.

Example:

```text
Public-Subnet-A
10.0.1.0/24

Public-Subnet-B
10.0.2.0/24
```

### Step 3 - Configure Internet Gateway

Attach:

```text
AWS-Lab-IGW
```

to:

```text
AWS-Lab-VPC
```

### Step 4 - Configure Route Table

Add:

```text
Destination:
0.0.0.0/0

Target:
Internet Gateway
```

Associate the required public subnets.

### Step 5 - Launch EC2 Instance 1

Launch:

```text
EC2-01
```

in:

```text
Public-Subnet-A
```

Install and configure a web server as required.

### Step 6 - Launch EC2 Instance 2

Launch:

```text
EC2-02
```

in:

```text
Public-Subnet-B
```

Install and configure a web server as required.

### Step 7 - Create Target Group

Create:

```text
Target Group:
AWS-Web-TG
```

Configure:

```text
Protocol:
HTTP

Port:
80
```

Register:

```text
EC2-01
EC2-02
```

### Step 8 - Configure Health Check

Example:

```text
Protocol:
HTTP

Path:
/

Port:
Traffic Port
```

Save the configuration.

### Step 9 - Create Load Balancer

Create:

```text
Load Balancer:
AWS-Web-ALB
```

Select:

```text
Scheme:
Internet-facing
```

Select appropriate subnets in multiple Availability Zones.

### Step 10 - Configure Load Balancer Security Group

Allow:

```text
HTTP:
Port 80
```

and HTTPS when required.

### Step 11 - Configure Listener

Configure:

```text
Protocol:
HTTP

Port:
80

Default Action:
Forward to AWS-Web-TG
```

### Step 12 - Verify Target Health

Open:

```text
EC2
   |
   v
Target Groups
   |
   v
AWS-Web-TG
   |
   v
Targets
```

Verify:

```text
EC2-01:
Healthy

EC2-02:
Healthy
```

### Step 13 - Test Load Balancer

Open the Load Balancer details.

Copy the DNS name provided by AWS.

Open the Load Balancer DNS name in a browser.

### Result

**Successfully created an Application Load Balancer, configured a Target Group, registered EC2 instances, configured health checks and a listener, and verified traffic distribution through the Load Balancer.**

---

## 20. Load Balancer Health Check Failure

### Explanation

If a target shows **Unhealthy**, the Load Balancer will not normally send new requests to that unhealthy target.

Common causes include:

- Web server is not running.
- Incorrect health check path.
- Incorrect port.
- Security Group blocking traffic.
- Network ACL blocking traffic.
- Application returning an unhealthy response.
- Incorrect Target Group configuration.

### Troubleshooting Flow

```text
Target Unhealthy
      |
      v
Check EC2 Status
      |
      v
Check Application
      |
      v
Check Port
      |
      v
Check Health Check Path
      |
      v
Check Security Group
      |
      v
Check Network ACL
      |
      v
Check Target Group
      |
      v
Check Again
```

### Result

**Successfully understood how to troubleshoot unhealthy targets in a Load Balancer Target Group.**

---

## 21. Load Balancer High Availability

### Explanation

A Load Balancer can distribute traffic across multiple Availability Zones.

If one target becomes unavailable, healthy targets can continue serving traffic.

### Example

```text
                    Load Balancer
                         |
            +------------+------------+
            |                         |
            v                         v
       Availability Zone A      Availability Zone B
            |                         |
            v                         v
         EC2-01                    EC2-02
         Healthy                  Healthy
```

If EC2-01 becomes unhealthy:

```text
                    Load Balancer
                         |
            +------------+------------+
            |                         |
            v                         v
         EC2-01                    EC2-02
       Unhealthy                   Healthy
            X                         |
                                      v
                              Receives Traffic
```

### Result

**Successfully understood how Load Balancers can improve application availability by distributing traffic across multiple Availability Zones and healthy targets.**

---

## 22. Load Balancer and Security Groups

### Explanation

A recommended architecture separates the Security Group of the Load Balancer from the Security Group of the backend instances.

### Example

```text
Internet
    |
    v
Load Balancer
    |
    | Load Balancer SG
    v
Target Group
    |
    v
EC2
    |
    | EC2 SG
    v
Application
```

The backend Security Group can be configured to accept the required application traffic from the Load Balancer Security Group.

### Result

**Successfully understood how separate Security Groups can be used to control traffic between the Load Balancer and backend EC2 instances.**

---

## 23. Load Balancer and Auto Scaling

### Explanation

A Load Balancer can work with an **Auto Scaling Group** to distribute traffic across dynamically changing EC2 instances.

### Example

```text
                    Load Balancer
                         |
                         v
                  Auto Scaling Group
                  /       |        \
                 v        v         v
              EC2-01   EC2-02    EC2-03
```

When instances are added or removed, the architecture can continue distributing traffic among available healthy targets.

### Result

**Successfully understood how Load Balancers can work with Auto Scaling to support scalable applications.**

---

## 24. Load Balancer vs Direct EC2 Access

### Direct EC2 Access

```text
User
 |
 v
EC2 Instance
```

If the instance fails:

```text
User
 |
 v
EC2 Instance
 |
 X
Failure
```

### Load Balancer Access

```text
User
 |
 v
Load Balancer
 |
 +---- EC2-01
 |
 +---- EC2-02
 |
 +---- EC2-03
```

The Load Balancer provides a single entry point while distributing requests among backend targets.

### Result

**Successfully understood the advantage of using a Load Balancer instead of directing all users to a single EC2 instance.**

---

## 25. Load Balancer Security Best Practices

### Explanation

Important Load Balancer security practices include:

- Allow only required listener ports.
- Use HTTPS for encrypted application traffic when required.
- Use appropriate TLS certificates.
- Restrict backend EC2 access to the Load Balancer Security Group where appropriate.
- Keep backend instances private when direct public access is not required.
- Use health checks.
- Remove unhealthy targets.
- Monitor Load Balancer activity.
- Review Security Group rules regularly.
- Avoid unnecessary public exposure.

### Example

```text
Internet
    |
    v
HTTPS : 443
    |
    v
Load Balancer
    |
    v
Target Group
    |
    v
Private EC2
```

### Result

**Successfully understood important security practices for protecting Load Balancer and backend application traffic.**

---

## 26. Load Balancer Troubleshooting

### Explanation

If users cannot access the application through the Load Balancer, check the complete architecture.

### Troubleshooting Flow

```text
Application Not Accessible
          |
          v
Check Load Balancer
          |
          v
Check Listener
          |
          v
Check Listener Rule
          |
          v
Check Target Group
          |
          v
Check Target Health
          |
          v
Check EC2 Application
          |
          v
Check Security Groups
          |
          v
Check Network ACL
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

**Successfully understood the basic troubleshooting process for Load Balancer connectivity and target health problems.**

---

## 27. Complete Load Balancer Architecture

```text
                              Internet
                                  |
                                  v
                         Load Balancer
                         AWS-Web-ALB
                                  |
                       +----------+----------+
                       |                     |
                       v                     v
                  Availability Zone A   Availability Zone B
                       |                     |
                       v                     v
                  Public/Private        Public/Private
                     Subnet                Subnet
                       |                     |
                       v                     v
                    EC2-01                EC2-02
                       |                     |
                       +----------+----------+
                                  |
                                  v
                              Application
```

---

## 28. Complete Load Balancer Workflow

### Workflow

```text
Create VPC
    |
    v
Create Subnets
    |
    v
Launch EC2 Instances
    |
    v
Configure Web Application
    |
    v
Create Security Groups
    |
    v
Create Target Group
    |
    v
Register EC2 Instances
    |
    v
Configure Health Checks
    |
    v
Create Load Balancer
    |
    v
Select Availability Zones
    |
    v
Configure Listener
    |
    v
Forward Traffic to Target Group
    |
    v
Check Target Health
    |
    v
Test Load Balancer DNS
    |
    v
Monitor Application
```

### Practical Steps

1. Create or select a VPC.
2. Create appropriate subnets.
3. Launch multiple EC2 instances.
4. Install and configure the application.
5. Create Security Groups.
6. Create a Target Group.
7. Register the EC2 instances.
8. Configure health checks.
9. Create the Load Balancer.
10. Select appropriate Availability Zones.
11. Configure the Load Balancer Security Group.
12. Create the Listener.
13. Configure the Listener Rule.
14. Forward traffic to the Target Group.
15. Verify target health.
16. Test the Load Balancer DNS name.
17. Monitor the Load Balancer and targets.
18. Remove unused resources after completing the lab.

### Final Result

**Successfully completed Lab 12 - Load Balancer and understood how AWS Elastic Load Balancing distributes incoming traffic across backend resources. Learned about Application Load Balancers, Network Load Balancers, Target Groups, Listeners, Listener Rules, Health Checks, Availability Zones, Security Groups, traffic distribution, high availability, Auto Scaling integration, troubleshooting, and Load Balancer security best practices.**
