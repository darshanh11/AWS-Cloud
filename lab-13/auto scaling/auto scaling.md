# Lab 13 - Auto Scaling

## Objective

The objective of this lab is to understand **Amazon EC2 Auto Scaling** and practically learn how to automatically increase or decrease the number of EC2 instances based on application demand.

This lab covers:

- Auto Scaling
- Auto Scaling Group
- Launch Template
- Minimum Capacity
- Maximum Capacity
- Desired Capacity
- Scaling Out
- Scaling In
- Health Checks
- Availability Zones
- Load Balancer Integration
- Scaling Policies
- Target Tracking
- CloudWatch Metrics
- Instance Replacement
- High Availability
- Practical Auto Scaling Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is Auto Scaling?

### Explanation

**Amazon EC2 Auto Scaling** automatically adjusts the number of EC2 instances in an application according to demand.

It can:

- Add EC2 instances when demand increases.
- Remove EC2 instances when demand decreases.
- Replace unhealthy instances.
- Maintain the required number of instances.
- Distribute instances across Availability Zones.

### Example

```text
                    Auto Scaling Group
                           |
              +------------+------------+
              |            |            |
              v            v            v
            EC2-01       EC2-02       EC2-03
```

When demand increases:

```text
                    Auto Scaling Group
                           |
        +----------+-------+-------+----------+
        |          |               |          |
        v          v               v          v
      EC2-01     EC2-02          EC2-03     EC2-04
```

When demand decreases:

```text
                    Auto Scaling Group
                           |
              +------------+------------+
              |            |            |
              v            v            v
            EC2-01       EC2-02       EC2-03
```

### Result

**Successfully understood that Auto Scaling automatically adjusts EC2 capacity according to application requirements.**

---

## 2. Why is Auto Scaling Used?

### Explanation

Auto Scaling helps applications maintain availability while using resources efficiently.

It can help with:

- High availability
- Scalability
- Fault tolerance
- Automatic instance replacement
- Handling changing workloads
- Cost optimization

### Example

```text
Low Traffic
     |
     v
Fewer EC2 Instances
     |
     v
Lower Resource Usage


High Traffic
     |
     v
More EC2 Instances
     |
     v
Higher Capacity
```

### Result

**Successfully understood why Auto Scaling is used to maintain application availability and dynamically adjust capacity.**

---

## 3. What is an Auto Scaling Group?

### Explanation

An **Auto Scaling Group (ASG)** is a collection of EC2 instances that are managed together by Auto Scaling.

The Auto Scaling Group maintains the configured capacity and can launch or terminate instances according to the scaling configuration.

### Example

```text
                Auto Scaling Group
                       |
          +------------+------------+
          |            |            |
          v            v            v
       EC2-01       EC2-02       EC2-03
```

### Result

**Successfully understood that an Auto Scaling Group manages a group of EC2 instances as a single scalable unit.**

---

## 4. Desired Capacity

### Explanation

**Desired Capacity** specifies the number of EC2 instances that the Auto Scaling Group should try to maintain.

Example:

```text
Desired Capacity:
2
```

The Auto Scaling Group attempts to maintain two instances under normal conditions.

### Example

```text
Desired Capacity = 2

Auto Scaling Group
       |
       +---- EC2-01
       |
       +---- EC2-02
```

### Result

**Successfully understood that Desired Capacity defines the normal number of instances the Auto Scaling Group attempts to maintain.**

---

## 5. Minimum Capacity

### Explanation

**Minimum Capacity** defines the minimum number of instances that the Auto Scaling Group should maintain.

Example:

```text
Minimum Capacity:
2
```

The Auto Scaling Group should not normally scale below the configured minimum.

### Example

```text
Minimum:
2

EC2-01
EC2-02
```

### Result

**Successfully understood that Minimum Capacity defines the lower limit of instances in an Auto Scaling Group.**

---

## 6. Maximum Capacity

### Explanation

**Maximum Capacity** defines the maximum number of EC2 instances that the Auto Scaling Group can launch.

Example:

```text
Maximum Capacity:
5
```

The Auto Scaling Group can scale up to five instances according to its scaling policies and other constraints.

### Example

```text
Maximum = 5

EC2-01
EC2-02
EC2-03
EC2-04
EC2-05
```

### Result

**Successfully understood that Maximum Capacity defines the upper limit of instances that the Auto Scaling Group can maintain.**

---

## 7. Minimum, Desired, and Maximum Capacity

### Explanation

An Auto Scaling Group commonly uses three important capacity values.

```text
Minimum Capacity
Desired Capacity
Maximum Capacity
```

Example:

```text
Minimum:
2

Desired:
2

Maximum:
5
```

### Architecture

```text
Minimum = 2
Desired = 2
Maximum = 5

          Auto Scaling Group
                  |
       +----------+----------+
       |                     |
       v                     v
     EC2-01                EC2-02
```

If demand increases:

```text
2 Instances
     |
     v
3 Instances
     |
     v
4 Instances
     |
     v
5 Instances
```

### Result

**Successfully understood the relationship between Minimum, Desired, and Maximum Capacity.**

---

## 8. What is a Launch Template?

### Explanation

A **Launch Template** defines the configuration that Auto Scaling uses when launching EC2 instances.

A Launch Template can specify settings such as:

- AMI
- Instance type
- Key pair
- Security Groups
- Storage
- Network configuration
- User data

### Example

```text
Launch Template
       |
       v
Auto Scaling Group
       |
       +----------+----------+
       |                     |
       v                     v
    EC2-01                EC2-02
```

### Result

**Successfully understood that a Launch Template provides the configuration used to launch EC2 instances in an Auto Scaling Group.**

---

## 9. Creating a Launch Template

### Explanation

Before creating an Auto Scaling Group, a Launch Template can be created to define the EC2 instance configuration.

### Practical Steps

1. Open the **EC2** service.
2. Select **Launch Templates**.
3. Click **Create launch template**.
4. Enter the Launch Template name.

Example:

```text
AWS-Lab-Launch-Template
```

5. Select the required AMI.
6. Select the required instance type.
7. Select the required key pair when needed.
8. Configure the Security Group.
9. Configure storage.
10. Add user data when required.
11. Review the configuration.
12. Click **Create launch template**.
13. Verify the Launch Template.

### Result

**Successfully created a Launch Template for the Auto Scaling lab.**

---

## 10. What is Scaling Out?

### Explanation

**Scaling Out** means increasing the number of EC2 instances when application demand increases.

### Example

```text
Before Scaling Out:

EC2-01
EC2-02

        |
        v

After Scaling Out:

EC2-01
EC2-02
EC2-03
EC2-04
```

### Result

**Successfully understood that Scaling Out increases the number of EC2 instances to handle increased demand.**

---

## 11. What is Scaling In?

### Explanation

**Scaling In** means reducing the number of EC2 instances when application demand decreases.

### Example

```text
Before Scaling In:

EC2-01
EC2-02
EC2-03
EC2-04

        |
        v

After Scaling In:

EC2-01
EC2-02
```

The Auto Scaling Group maintains the configured minimum capacity.

### Result

**Successfully understood that Scaling In reduces the number of EC2 instances when additional capacity is no longer required.**

---

## 12. Scaling Policies

### Explanation

A **Scaling Policy** defines when and how Auto Scaling should adjust capacity.

Common approaches include:

- Target Tracking Scaling
- Step Scaling
- Scheduled Scaling
- Simple Scaling

### Example

```text
High CPU Utilization
        |
        v
Scaling Policy
        |
        v
Launch EC2 Instance
```

### Result

**Successfully understood that scaling policies determine when Auto Scaling should add or remove EC2 instances.**

---

## 13. Target Tracking Scaling

### Explanation

**Target Tracking Scaling** attempts to keep a selected CloudWatch metric near a target value.

For example, a policy can target average CPU utilization.

Example:

```text
Target CPU:
50%
```

If average CPU rises significantly above the target, Auto Scaling can increase capacity.

If demand decreases and CPU utilization falls, Auto Scaling can reduce capacity when appropriate.

### Example

```text
CPU Utilization
      |
      v
CloudWatch Metric
      |
      v
Target Tracking Policy
      |
      +----------+----------+
      |                     |
      v                     v
Scale Out               Scale In
```

### Result

**Successfully understood how Target Tracking Scaling can automatically adjust EC2 capacity based on a target metric.**

---

## 14. CloudWatch and Auto Scaling

### Explanation

Amazon CloudWatch provides monitoring metrics that can be used with Auto Scaling policies.

Examples include:

```text
CPU Utilization
Network Traffic
Application Load
```

The exact metric used depends on the scaling configuration.

### Example

```text
EC2 Instances
      |
      v
CloudWatch
      |
      v
Scaling Policy
      |
      v
Auto Scaling Group
      |
      v
Scale Out / Scale In
```

### Result

**Successfully understood how CloudWatch metrics can be used by Auto Scaling policies to make scaling decisions.**

---

## 15. Health Checks

### Explanation

Auto Scaling can use health checks to determine whether an instance is healthy.

If an instance is determined to be unhealthy, the Auto Scaling Group can terminate and replace it to maintain the desired capacity.

### Example

```text
Auto Scaling Group
       |
       +---- EC2-01 -> Healthy
       |
       +---- EC2-02 -> Unhealthy
                         |
                         v
                      Replace
                         |
                         v
                      EC2-03
```

### Result

**Successfully understood how Auto Scaling can replace unhealthy EC2 instances and maintain the required capacity.**

---

## 16. Auto Scaling and Availability Zones

### Explanation

An Auto Scaling Group can use subnets in multiple Availability Zones.

This improves application resilience by distributing instances across separate Availability Zones.

### Example

```text
                    Auto Scaling Group
                           |
              +------------+------------+
              |                         |
              v                         v
       Availability Zone A       Availability Zone B
              |                         |
              v                         v
           EC2-01                    EC2-02
```

### Result

**Successfully understood how Auto Scaling can distribute instances across multiple Availability Zones for improved availability.**

---

## 17. Auto Scaling and Load Balancer

### Explanation

A Load Balancer can distribute incoming traffic across the instances managed by an Auto Scaling Group.

When Auto Scaling launches or terminates instances, the Load Balancer can work with the Target Group to distribute traffic to available healthy targets.

### Architecture

```text
                         Internet
                             |
                             v
                       Load Balancer
                             |
                             v
                       Target Group
                             |
                             v
                     Auto Scaling Group
                    /        |        \
                   v         v         v
                EC2-01    EC2-02    EC2-03
```

### Result

**Successfully understood how Load Balancers and Auto Scaling work together to provide scalable and highly available applications.**

---

## 18. Creating an Auto Scaling Group

### Explanation

An Auto Scaling Group is created using a Launch Template and network configuration.

### Practical Steps

1. Open **EC2**.
2. Select **Auto Scaling Groups**.
3. Click **Create Auto Scaling group**.
4. Enter the Auto Scaling Group name.

Example:

```text
AWS-Lab-ASG
```

5. Select the Launch Template.

```text
AWS-Lab-Launch-Template
```

6. Select the VPC.
7. Select subnets in the required Availability Zones.
8. Configure the desired capacity.
9. Configure minimum capacity.
10. Configure maximum capacity.

Example:

```text
Desired:
2

Minimum:
2

Maximum:
4
```

11. Configure Load Balancer integration if required.
12. Configure health checks.
13. Configure scaling policies.
14. Review the configuration.
15. Create the Auto Scaling Group.
16. Verify the instances.

### Result

**Successfully created an Auto Scaling Group using a Launch Template and configured its capacity limits and network settings.**

---

## 19. Practical Lab - Auto Scaling with EC2

### Explanation

In this practical lab, an Auto Scaling Group is created to maintain multiple EC2 instances automatically.

### Architecture

```text
                    Auto Scaling Group
                           |
              +------------+------------+
              |                         |
              v                         v
           EC2-01                    EC2-02
         Availability A           Availability B
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

### Step 2 - Create Subnets

Create subnets in multiple Availability Zones.

Example:

```text
Subnet A:
10.0.1.0/24

Subnet B:
10.0.2.0/24
```

### Step 3 - Configure Security Group

Create:

```text
AWS-ASG-SG
```

Allow only the required application traffic.

Example:

```text
HTTP:
Port 80

HTTPS:
Port 443
```

Allow administrative access only from a trusted source when required.

### Step 4 - Create Launch Template

Create:

```text
AWS-Lab-Launch-Template
```

Configure:

```text
AMI:
Required AMI

Instance Type:
Required Instance Type

Security Group:
AWS-ASG-SG
```

### Step 5 - Create Auto Scaling Group

Create:

```text
AWS-Lab-ASG
```

Select:

```text
Launch Template:
AWS-Lab-Launch-Template
```

Select the VPC.

Select:

```text
Subnet A
Subnet B
```

### Step 6 - Configure Capacity

Set:

```text
Desired Capacity:
2

Minimum Capacity:
2

Maximum Capacity:
4
```

### Step 7 - Configure Health Checks

Configure the required health check type.

Verify that the Auto Scaling Group monitors instance health.

### Step 8 - Create Auto Scaling Group

Review the configuration.

Click:

```text
Create Auto Scaling group
```

### Step 9 - Verify EC2 Instances

Open:

```text
EC2
   |
   v
Instances
```

Verify that the Auto Scaling Group launched the expected instances.

Example:

```text
AWS-Lab-ASG

EC2-01
EC2-02
```

### Result

**Successfully created an Auto Scaling Group that maintains the configured number of EC2 instances across the selected Availability Zones.**

---

## 20. Practical Lab - Target Tracking Scaling

### Explanation

In this lab, a Target Tracking policy is configured to automatically adjust the number of EC2 instances according to CPU utilization.

### Practical Steps

1. Open **EC2 > Auto Scaling Groups**.
2. Select:

```text
AWS-Lab-ASG
```

3. Open the **Automatic scaling** section.
4. Add a scaling policy.
5. Select **Target tracking scaling**.
6. Select the required metric.

Example:

```text
Average CPU Utilization
```

7. Set a target value.

Example:

```text
Target:
50%
```

8. Save the scaling policy.
9. Verify the policy.

### Example

```text
CPU increases
     |
     v
Target Tracking
     |
     v
Scale Out
     |
     v
More EC2 Instances
```

When demand decreases:

```text
CPU decreases
     |
     v
Target Tracking
     |
     v
Scale In
     |
     v
Fewer EC2 Instances
```

### Result

**Successfully configured a Target Tracking scaling policy based on CPU utilization.**

---

## 21. Practical Lab - Auto Scaling with Load Balancer

### Explanation

A Load Balancer can be connected to an Auto Scaling Group so that incoming traffic is distributed among automatically managed EC2 instances.

### Architecture

```text
                         Internet
                             |
                             v
                     Application Load Balancer
                             |
                             v
                        Target Group
                             |
                             v
                      Auto Scaling Group
                   +---------+---------+
                   |         |         |
                   v         v         v
                EC2-01    EC2-02    EC2-03
```

### Practical Steps

1. Create an Application Load Balancer.
2. Create a Target Group.
3. Configure health checks.
4. Create a Launch Template.
5. Create an Auto Scaling Group.
6. Select the Load Balancer Target Group.
7. Configure minimum capacity.
8. Configure desired capacity.
9. Configure maximum capacity.
10. Configure a scaling policy.
11. Create the Auto Scaling Group.
12. Verify that instances are registered with the Target Group.
13. Verify target health.
14. Test the Load Balancer DNS name.

### Result

**Successfully integrated an Auto Scaling Group with a Load Balancer and understood how traffic can be distributed across dynamically managed EC2 instances.**

---

## 22. Scaling Out Practical Test

### Explanation

Scaling Out can be tested by increasing workload or using a controlled scaling policy.

### Practical Steps

1. Open the Auto Scaling Group.
2. Verify the current desired capacity.
3. Verify the minimum and maximum capacity.
4. Review the scaling policy.
5. Generate an appropriate test workload if required.
6. Monitor CloudWatch metrics.
7. Observe the Auto Scaling Group activity.
8. Verify whether a new EC2 instance is launched.
9. Check the Target Group if a Load Balancer is configured.
10. Verify the new instance health.

### Example

```text
Before:

Desired Capacity = 2

EC2-01
EC2-02


After Scaling Out:

Desired Capacity = 3

EC2-01
EC2-02
EC2-03
```

### Result

**Successfully understood and verified the process of Scaling Out by increasing EC2 capacity.**

---

## 23. Scaling In Practical Test

### Explanation

Scaling In reduces the number of EC2 instances when additional capacity is no longer required.

### Practical Steps

1. Open the Auto Scaling Group.
2. Review the current capacity.
3. Reduce workload or allow the scaling policy to respond naturally.
4. Monitor CloudWatch metrics.
5. Observe Auto Scaling activity.
6. Verify whether an instance is removed.
7. Check that the Auto Scaling Group does not go below the configured minimum capacity.
8. Verify remaining instance health.

### Example

```text
Before:

EC2-01
EC2-02
EC2-03


After Scaling In:

EC2-01
EC2-02
```

### Result

**Successfully understood and verified the process of Scaling In while maintaining the configured minimum capacity.**

---

## 24. Auto Scaling Instance Replacement

### Explanation

Auto Scaling can replace an unhealthy instance to maintain the desired capacity.

### Example

```text
Desired Capacity = 2

EC2-01 -> Healthy
EC2-02 -> Unhealthy
```

Auto Scaling can replace the unhealthy instance:

```text
EC2-01 -> Healthy
EC2-02 -> Removed
EC2-03 -> New Instance
```

### Result

**Successfully understood how Auto Scaling can replace unhealthy instances to maintain application capacity.**

---

## 25. Auto Scaling and Load Balancer Health Checks

### Explanation

When a Load Balancer is integrated with an Auto Scaling Group, the Target Group can perform health checks on the application targets.

This allows unhealthy targets to be identified.

### Example

```text
Load Balancer
      |
      v
Target Group
      |
      +---- EC2-01 -> Healthy
      |
      +---- EC2-02 -> Unhealthy
```

The Auto Scaling Group can replace an unhealthy instance according to its health-check configuration.

### Result

**Successfully understood how Load Balancer health checks and Auto Scaling health management can work together.**

---

## 26. Auto Scaling Troubleshooting

### Explanation

If an Auto Scaling Group is not launching or scaling instances correctly, check the complete configuration.

Important items include:

- Launch Template
- AMI
- Instance type
- Security Group
- VPC
- Subnets
- Availability Zones
- Minimum capacity
- Desired capacity
- Maximum capacity
- Scaling policy
- Health checks
- Load Balancer
- Target Group
- IAM permissions
- CloudWatch metrics

### Troubleshooting Flow

```text
Auto Scaling Not Working
          |
          v
Check Auto Scaling Group
          |
          v
Check Capacity
          |
          v
Check Launch Template
          |
          v
Check VPC and Subnets
          |
          v
Check Availability Zones
          |
          v
Check Scaling Policy
          |
          v
Check CloudWatch Metrics
          |
          v
Check Health Checks
          |
          v
Check Load Balancer
          |
          v
Check Target Group
          |
          v
Review Activity History
```

### Result

**Successfully understood the basic troubleshooting process for Auto Scaling problems.**

---

## 27. Auto Scaling Activity History

### Explanation

The Auto Scaling Group provides activity information showing actions such as:

- Instance launch
- Instance termination
- Instance replacement
- Scaling activity
- Failed launches

### Practical Steps

1. Open **EC2**.
2. Select **Auto Scaling Groups**.
3. Select the required Auto Scaling Group.
4. Open the **Activity** section.
5. Review recent scaling activities.
6. Check whether instances were launched or terminated.
7. Review any failure messages.
8. Use the information for troubleshooting.

### Result

**Successfully learned how to review Auto Scaling activity history to understand scaling events and failures.**

---

## 28. Auto Scaling Security Best Practices

### Explanation

Auto Scaling environments should follow security best practices.

Important practices include:

- Use secure AMIs.
- Use least-privilege IAM permissions.
- Use appropriate Security Groups.
- Keep unnecessary ports closed.
- Avoid unnecessary public IP addresses.
- Use private subnets for backend instances when appropriate.
- Use HTTPS for secure application traffic.
- Monitor instances using CloudWatch.
- Regularly update the AMI and application.
- Review Launch Template configuration.
- Use multiple Availability Zones for high availability.

### Example

```text
Internet
    |
    v
Load Balancer
    |
    v
Target Group
    |
    v
Auto Scaling Group
    |
    +---- Private Subnet
    |         |
    |         +---- EC2-01
    |         +---- EC2-02
    |
    +---- Private Subnet
              |
              +---- EC2-03
```

### Result

**Successfully understood important security practices for Auto Scaling environments.**

---

## 29. Auto Scaling Architecture

```text
                              Internet
                                  |
                                  v
                         Application Load Balancer
                                  |
                                  v
                             Target Group
                                  |
                                  v
                          Auto Scaling Group
                     +------------+------------+
                     |                         |
                     v                         v
             Availability Zone A       Availability Zone B
                     |                         |
                     v                         v
                  EC2-01                    EC2-02
                     |                         |
                     +------------+------------+
                                  |
                                  v
                              Application
```

---

## 30. Complete Auto Scaling Workflow

### Workflow

```text
Create VPC
    |
    v
Create Subnets
    |
    v
Create Security Group
    |
    v
Create Launch Template
    |
    v
Create Target Group
    |
    v
Create Load Balancer
    |
    v
Create Auto Scaling Group
    |
    v
Select Launch Template
    |
    v
Select Availability Zones
    |
    v
Set Minimum Capacity
    |
    v
Set Desired Capacity
    |
    v
Set Maximum Capacity
    |
    v
Configure Health Checks
    |
    v
Configure Scaling Policy
    |
    v
Launch EC2 Instances
    |
    v
Register Targets
    |
    v
Monitor CloudWatch Metrics
    |
    +-------------------+
    |                   |
    v                   v
  Scale Out           Scale In
    |                   |
    v                   v
More EC2            Fewer EC2
Instances            Instances
```

### Practical Steps

1. Create or select a VPC.
2. Create subnets in multiple Availability Zones.
3. Create a Security Group.
4. Create a Launch Template.
5. Configure the AMI.
6. Configure the instance type.
7. Configure the Security Group.
8. Create a Target Group.
9. Create an Application Load Balancer when required.
10. Create an Auto Scaling Group.
11. Select the Launch Template.
12. Select the VPC.
13. Select the required subnets.
14. Configure Minimum Capacity.
15. Configure Desired Capacity.
16. Configure Maximum Capacity.
17. Configure health checks.
18. Configure the Load Balancer integration when required.
19. Configure a scaling policy.
20. Verify the EC2 instances.
21. Verify Target Group health.
22. Monitor CloudWatch metrics.
23. Test Scaling Out.
24. Test Scaling In.
25. Review Auto Scaling activity history.
26. Verify unhealthy instance replacement when applicable.
27. Remove unused resources after completing the lab.

### Final Result

**Successfully completed Lab 13 - Auto Scaling and understood how Amazon EC2 Auto Scaling automatically manages EC2 capacity. Learned about Auto Scaling Groups, Launch Templates, Minimum Capacity, Desired Capacity, Maximum Capacity, Scaling Out, Scaling In, Scaling Policies, Target Tracking, CloudWatch metrics, health checks, Availability Zones, Load Balancer integration, instance replacement, troubleshooting, and Auto Scaling security best practices.**
