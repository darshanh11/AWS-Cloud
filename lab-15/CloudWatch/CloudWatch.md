# Lab 15 - Amazon CloudWatch

## Objective

The objective of this lab is to understand **Amazon CloudWatch** and practically learn how to monitor AWS resources, collect metrics, create alarms, view logs, and monitor application performance.

This lab covers:

- Amazon CloudWatch
- Monitoring
- Metrics
- Namespaces
- Dimensions
- Statistics
- Dashboards
- Alarms
- CloudWatch Logs
- Log Groups
- Log Streams
- CloudWatch Agent
- EC2 Monitoring
- CPU Utilization
- Network Metrics
- Status Checks
- SNS Notifications
- Auto Scaling Integration
- RDS Monitoring
- Practical CloudWatch Configuration
- Troubleshooting
- Security Best Practices

---

## 1. What is Amazon CloudWatch?

### Explanation

**Amazon CloudWatch** is an AWS monitoring and observability service.

It can collect and monitor metrics, logs, and other operational information from AWS resources and applications.

CloudWatch can be used to:

- Monitor AWS resources
- Track performance
- Create alarms
- Collect logs
- Build dashboards
- Detect problems
- Trigger automated actions

### Example

```text
AWS Resources
     |
     +---- EC2
     |
     +---- RDS
     |
     +---- Load Balancer
     |
     +---- Auto Scaling
     |
     v
Amazon CloudWatch
     |
     +---- Metrics
     |
     +---- Logs
     |
     +---- Alarms
     |
     +---- Dashboards
```

### Result

**Successfully understood that Amazon CloudWatch is used to monitor AWS resources, applications, metrics, and logs.**

---

## 2. Why is CloudWatch Used?

### Explanation

CloudWatch helps administrators and engineers understand the health and performance of AWS resources.

It can help identify:

- High CPU usage
- Low available storage
- Network activity
- Application errors
- Unhealthy resources
- Performance problems

### Example

```text
EC2
 |
 v
CloudWatch
 |
 +---- CPU Usage
 |
 +---- Network Traffic
 |
 +---- Status Checks
 |
 v
Monitoring
```

### Result

**Successfully understood how CloudWatch helps monitor resource health and application performance.**

---

## 3. CloudWatch Metrics

### Explanation

A **metric** is a numerical measurement that represents the performance or behavior of a resource or application.

Examples include:

```text
CPUUtilization
NetworkIn
NetworkOut
DiskReadOps
DiskWriteOps
DatabaseConnections
```

### Example

```text
EC2 Instance
     |
     v
CloudWatch Metrics
     |
     +---- CPUUtilization
     |
     +---- NetworkIn
     |
     +---- NetworkOut
```

### Result

**Successfully understood that CloudWatch metrics are numerical measurements used to monitor AWS resources and applications.**

---

## 4. CloudWatch Namespace

### Explanation

A **namespace** is a container for CloudWatch metrics.

AWS services publish metrics into their respective namespaces.

Example:

```text
AWS/EC2
AWS/RDS
AWS/Lambda
AWS/ApplicationELB
```

### Example

```text
AWS/EC2
   |
   +---- CPUUtilization
   +---- NetworkIn
   +---- NetworkOut
```

### Result

**Successfully understood how CloudWatch namespaces organize metrics from different AWS services.**

---

## 5. CloudWatch Dimensions

### Explanation

**Dimensions** identify the resource or category associated with a metric.

For example, EC2 metrics can use dimensions such as:

```text
InstanceId
```

Example:

```text
Metric:
CPUUtilization

Dimension:
InstanceId

Value:
i-xxxxxxxxxxxxxxxxx
```

### Result

**Successfully understood how dimensions identify the specific resource associated with a CloudWatch metric.**

---

## 6. CloudWatch Statistics

### Explanation

CloudWatch can display statistics for metrics over a selected period.

Common statistics include:

```text
Average
Minimum
Maximum
Sum
Sample Count
```

### Example

```text
CPU Utilization

Average:
45%

Minimum:
20%

Maximum:
80%
```

### Result

**Successfully understood how CloudWatch statistics can be used to analyze metric values.**

---

## 7. EC2 Monitoring with CloudWatch

### Explanation

CloudWatch automatically provides several metrics for EC2 instances.

Common EC2 metrics include:

```text
CPUUtilization
NetworkIn
NetworkOut
DiskReadOps
DiskWriteOps
StatusCheckFailed
```

The available metrics depend on the EC2 configuration and monitoring options.

### Example

```text
EC2 Instance
     |
     v
CloudWatch
     |
     +---- CPUUtilization
     +---- NetworkIn
     +---- NetworkOut
     +---- Status Checks
```

### Result

**Successfully understood how CloudWatch monitors important EC2 performance metrics.**

---

## 8. CPU Utilization

### Explanation

**CPUUtilization** shows the percentage of allocated EC2 compute capacity being used.

Example:

```text
CPU Utilization:
25%
```

If CPU utilization becomes consistently high, additional investigation or scaling may be required.

### Example

```text
CPU Usage
   |
   +---- 20% -> Normal
   |
   +---- 50% -> Moderate
   |
   +---- 90% -> High
```

The appropriate threshold depends on the workload.

### Result

**Successfully understood how CPU utilization can be monitored using CloudWatch.**

---

## 9. Network Metrics

### Explanation

CloudWatch provides EC2 network metrics such as:

```text
NetworkIn
NetworkOut
```

These metrics help understand network traffic to and from an instance.

### Example

```text
EC2
 |
 +---- NetworkIn
 |
 +---- NetworkOut
 |
 v
CloudWatch
```

### Result

**Successfully understood how CloudWatch can be used to monitor EC2 network traffic.**

---

## 10. EC2 Status Checks

### Explanation

EC2 provides status checks that help determine whether an instance and its underlying infrastructure are functioning correctly.

CloudWatch can monitor status-check-related metrics.

Example:

```text
EC2
 |
 v
Status Checks
 |
 +---- System Status
 |
 +---- Instance Status
 |
 v
CloudWatch
```

### Result

**Successfully understood how CloudWatch can be used to monitor EC2 status checks.**

---

## 11. CloudWatch Dashboard

### Explanation

A **CloudWatch Dashboard** provides a visual view of selected metrics and monitoring information.

A dashboard can contain widgets such as:

- Line charts
- Number widgets
- Text
- Other supported monitoring visualizations

### Example

```text
CloudWatch Dashboard
+----------------------------+
| EC2 CPU Utilization        |
+----------------------------+
| Network Traffic            |
+----------------------------+
| RDS Connections             |
+----------------------------+
| Load Balancer Metrics       |
+----------------------------+
```

### Result

**Successfully understood how CloudWatch Dashboards provide a centralized view of important monitoring metrics.**

---

## 12. Creating a CloudWatch Dashboard

### Practical Steps

1. Open the AWS Management Console.
2. Search for **CloudWatch**.
3. Open the CloudWatch service.
4. Select **Dashboards**.
5. Click **Create dashboard**.
6. Enter a dashboard name.

Example:

```text
AWS-Lab-Dashboard
```

7. Click **Create dashboard**.
8. Select the required widget type.
9. Select the required metric.
10. Select the EC2 instance.
11. Add the metric to the dashboard.
12. Add additional metrics when required.
13. Save the dashboard.
14. Verify the dashboard.

### Example

```text
AWS-Lab-Dashboard

EC2 CPU:
45%

Network In:
XX

Network Out:
XX
```

### Result

**Successfully created a CloudWatch Dashboard and added resource monitoring metrics.**

---

## 13. CloudWatch Alarm

### Explanation

A **CloudWatch Alarm** monitors a metric against a defined threshold.

When the metric meets the configured condition, the alarm can change state and can trigger configured actions.

### Example

```text
CPU Utilization
       |
       v
CloudWatch Alarm
       |
       | > 80%
       v
ALARM
       |
       v
Notification / Action
```

### Result

**Successfully understood how CloudWatch Alarms monitor metrics and respond to configured threshold conditions.**

---

## 14. Creating a CloudWatch Alarm

### Explanation

A CloudWatch Alarm can be created for an EC2 CPU metric.

### Practical Steps

1. Open **CloudWatch**.
2. Select **Alarms**.
3. Click **Create alarm**.
4. Select a metric.
5. Select:

```text
EC2
```

6. Select the required instance.
7. Select:

```text
CPUUtilization
```

8. Select the required statistic.
9. Select the evaluation period.
10. Configure the threshold.

Example:

```text
Condition:
CPUUtilization > 80%
```

11. Configure the alarm action when required.
12. Enter an alarm name.

Example:

```text
High-CPU-Alarm
```

13. Review the configuration.
14. Create the alarm.
15. Verify the alarm state.

### Result

**Successfully created a CloudWatch Alarm to monitor EC2 CPU utilization.**

---

## 15. Alarm States

### Explanation

A CloudWatch Alarm can have different states.

Common states include:

```text
OK
ALARM
INSUFFICIENT_DATA
```

### Example

```text
Metric
  |
  v
Alarm Evaluation
  |
  +---- Normal ------> OK
  |
  +---- Threshold Met -> ALARM
  |
  +---- Not Enough Data -> INSUFFICIENT_DATA
```

### Result

**Successfully understood the main CloudWatch Alarm states and their meanings.**

---

## 16. CloudWatch Logs

### Explanation

**CloudWatch Logs** allows logs from supported AWS services, applications, and systems to be collected and monitored.

Logs can help troubleshoot application and infrastructure problems.

### Example

```text
Application
     |
     v
CloudWatch Logs
     |
     v
Log Group
     |
     v
Log Stream
     |
     v
Log Events
```

### Result

**Successfully understood how CloudWatch Logs can collect and organize application and system log information.**

---

## 17. Log Group

### Explanation

A **Log Group** is a collection of log streams that share the same retention, monitoring, and access settings.

Example:

```text
Log Group:
AWS-Lab-Logs
```

### Architecture

```text
Log Group
    |
    +---- Log Stream 1
    |
    +---- Log Stream 2
    |
    +---- Log Stream 3
```

### Result

**Successfully understood that a Log Group organizes related CloudWatch log streams.**

---

## 18. Log Stream

### Explanation

A **Log Stream** is a sequence of log events from the same source or related source.

Example:

```text
Log Group:
AWS-Lab-Logs

    |
    +---- Stream-01
    |
    +---- Stream-02
```

### Result

**Successfully understood how Log Streams organize individual sequences of log events inside a Log Group.**

---

## 19. Log Events

### Explanation

A **log event** represents an individual entry in CloudWatch Logs.

Example:

```text
2026-09-01 15:00:00
Application started

2026-09-01 15:01:00
User request received

2026-09-01 15:02:00
Database connection successful
```

### Result

**Successfully understood how individual log events are stored inside CloudWatch Logs.**

---

## 20. Creating a Log Group

### Practical Steps

1. Open **CloudWatch**.
2. Select **Logs**.
3. Select **Log groups**.
4. Click **Create log group**.
5. Enter:

```text
/aws/lab/application
```

6. Configure the required retention setting.
7. Create the Log Group.
8. Verify the Log Group.

### Result

**Successfully created a CloudWatch Log Group for application logs.**

---

## 21. CloudWatch Agent

### Explanation

The **CloudWatch Agent** can collect additional metrics and logs from EC2 instances beyond the standard metrics available automatically.

It can collect information such as:

```text
Memory Utilization
Disk Usage
Log Files
Additional System Metrics
```

### Example

```text
EC2
 |
 v
CloudWatch Agent
 |
 +---- Memory
 +---- Disk
 +---- Logs
 |
 v
CloudWatch
```

### Result

**Successfully understood how the CloudWatch Agent can collect additional system metrics and logs from EC2 instances.**

---

## 22. CloudWatch Agent Practical Steps

### Practical Steps

1. Launch an EC2 instance.
2. Connect to the EC2 instance.
3. Install the CloudWatch Agent using the appropriate installation method for the operating system.
4. Create or configure the CloudWatch Agent configuration.
5. Specify the metrics and log files to collect.
6. Start the CloudWatch Agent.
7. Verify the agent status.
8. Open CloudWatch.
9. Check the collected metrics.
10. Check the configured Log Group.
11. Verify that logs are being received.

### Example

```text
EC2
 |
 v
CloudWatch Agent
 |
 +---- Memory Utilization
 |
 +---- Disk Usage
 |
 +---- Application Logs
 |
 v
CloudWatch
```

### Result

**Successfully understood the practical workflow for installing and configuring the CloudWatch Agent to collect additional EC2 metrics and logs.**

---

## 23. CloudWatch and SNS

### Explanation

CloudWatch Alarms can integrate with **Amazon SNS** to send notifications when an alarm enters a configured state.

### Example

```text
EC2
 |
 v
CPU Utilization
 |
 v
CloudWatch Alarm
 |
 v
SNS
 |
 v
Notification
```

### Result

**Successfully understood how CloudWatch Alarms can work with SNS to send notifications about monitoring events.**

---

## 24. CloudWatch Alarm with SNS Practical Steps

### Practical Steps

1. Open **Amazon SNS**.
2. Create an SNS topic.
3. Add an appropriate subscription.
4. Confirm the subscription when required.
5. Open **CloudWatch**.
6. Create or edit a CloudWatch Alarm.
7. Select the required metric.
8. Configure the threshold.
9. Under alarm actions, select the SNS topic.
10. Save the alarm.
11. Verify the alarm configuration.
12. Test the notification workflow when appropriate.

### Example

```text
High CPU
   |
   v
CloudWatch Alarm
   |
   v
SNS Topic
   |
   v
Subscriber
```

### Result

**Successfully understood how to connect a CloudWatch Alarm with an SNS topic for notifications.**

---

## 25. CloudWatch and Auto Scaling

### Explanation

CloudWatch metrics can be used by Auto Scaling policies to adjust EC2 capacity.

### Example

```text
EC2
 |
 v
CloudWatch
 |
 v
CPU Metric
 |
 v
Auto Scaling Policy
 |
 +---- High CPU ---> Scale Out
 |
 +---- Low CPU ----> Scale In
```

### Result

**Successfully understood how CloudWatch metrics can support Auto Scaling decisions.**

---

## 26. CloudWatch and RDS

### Explanation

Amazon RDS publishes monitoring metrics to CloudWatch.

Examples include:

```text
CPUUtilization
DatabaseConnections
FreeStorageSpace
ReadIOPS
WriteIOPS
NetworkReceiveThroughput
NetworkTransmitThroughput
```

### Example

```text
RDS
 |
 v
CloudWatch
 |
 +---- CPU
 +---- Connections
 +---- Storage
 +---- IOPS
 +---- Network
```

### Result

**Successfully understood how CloudWatch can monitor RDS database performance and resource utilization.**

---

## 27. CloudWatch and Load Balancer

### Explanation

Load Balancers publish monitoring metrics to CloudWatch.

These metrics can help monitor:

- Request traffic
- Target health
- Response behavior
- Load Balancer performance

### Example

```text
Load Balancer
      |
      v
CloudWatch
      |
      +---- Requests
      +---- Target Health
      +---- Response Metrics
```

### Result

**Successfully understood how CloudWatch can be used to monitor Load Balancer performance and traffic.**

---

## 28. CloudWatch Metric Alarm Practical Lab

### Explanation

In this practical lab, an alarm is created to monitor EC2 CPU utilization.

### Practical Steps

### Step 1 - Launch EC2

Launch an EC2 instance.

Example:

```text
Instance:
AWS-Lab-EC2
```

### Step 2 - Open CloudWatch

Go to:

```text
AWS Console
   |
   v
CloudWatch
```

### Step 3 - Select Metrics

Open:

```text
Metrics
   |
   v
EC2
   |
   v
Per-Instance Metrics
```

### Step 4 - Select CPU Metric

Select:

```text
CPUUtilization
```

Select the required EC2 instance.

### Step 5 - Create Alarm

Click:

```text
Create alarm
```

Configure:

```text
Metric:
CPUUtilization

Condition:
Greater than 80%

Evaluation:
Required evaluation period
```

### Step 6 - Configure Action

Configure SNS notification when required.

### Step 7 - Name Alarm

Example:

```text
AWS-Lab-High-CPU
```

### Step 8 - Create Alarm

Click:

```text
Create alarm
```

### Step 9 - Verify

Open:

```text
CloudWatch
   |
   v
Alarms
```

Verify:

```text
AWS-Lab-High-CPU
```

### Result

**Successfully created and configured a CloudWatch CPU utilization alarm for an EC2 instance.**

---

## 29. Practical Lab - CloudWatch Dashboard

### Explanation

In this practical lab, a dashboard is created to monitor multiple AWS resources.

### Practical Steps

1. Open CloudWatch.
2. Select **Dashboards**.
3. Click **Create dashboard**.
4. Enter:

```text
AWS-Lab-Monitoring
```

5. Add an EC2 CPU widget.
6. Add an EC2 network widget.
7. Add an RDS metric when an RDS database is available.
8. Add Load Balancer metrics when a Load Balancer is available.
9. Arrange the widgets.
10. Save the dashboard.
11. Open the dashboard.
12. Verify the metrics.

### Example

```text
+----------------------------------+
|        AWS-Lab-Monitoring        |
+----------------------------------+
| EC2 CPU Utilization              |
+----------------------------------+
| EC2 Network Traffic              |
+----------------------------------+
| RDS Database Connections         |
+----------------------------------+
| Load Balancer Requests           |
+----------------------------------+
```

### Result

**Successfully created a CloudWatch Dashboard containing monitoring information from AWS resources.**

---

## 30. Practical Lab - CloudWatch Logs

### Explanation

In this lab, CloudWatch Logs are configured to collect application or system log information.

### Practical Steps

1. Open CloudWatch.
2. Select **Logs**.
3. Select **Log groups**.
4. Create:

```text
/aws/lab/application
```

5. Configure the required retention setting.
6. Configure an appropriate log source.
7. Send logs to the Log Group.
8. Open the Log Group.
9. Select the available Log Stream.
10. Review the log events.
11. Search for relevant log entries.
12. Verify that logs are being received.

### Example

```text
EC2 Application
      |
      v
CloudWatch Logs
      |
      v
/aws/lab/application
      |
      v
Log Stream
      |
      v
Log Events
```

### Result

**Successfully understood the practical workflow for collecting and reviewing application logs using CloudWatch Logs.**

---

## 31. CloudWatch Monitoring Workflow

### Explanation

CloudWatch monitoring follows a continuous process of collecting, analyzing, and responding to operational information.

### Workflow

```text
AWS Resource
     |
     v
Metrics / Logs
     |
     v
CloudWatch
     |
     +---- Dashboard
     |
     +---- Alarm
     |
     +---- Logs
     |
     v
Monitoring
     |
     v
Action / Investigation
```

### Result

**Successfully understood the complete CloudWatch monitoring workflow.**

---

## 32. CloudWatch Troubleshooting

### Explanation

CloudWatch can help identify resource and application problems.

Common troubleshooting steps include:

- Check metrics.
- Check alarms.
- Check logs.
- Check dashboards.
- Check EC2 status.
- Check CPU utilization.
- Check network metrics.
- Check RDS metrics.
- Check Load Balancer metrics.
- Check Auto Scaling activity.

### Troubleshooting Flow

```text
Application Problem
       |
       v
Check CloudWatch Dashboard
       |
       v
Check Metrics
       |
       v
Check Alarms
       |
       v
Check CloudWatch Logs
       |
       v
Identify Problem
       |
       v
Take Corrective Action
       |
       v
Monitor Again
```

### Result

**Successfully understood how CloudWatch can be used to troubleshoot AWS resource and application problems.**

---

## 33. CloudWatch Security Best Practices

### Explanation

CloudWatch data should be protected using appropriate AWS security controls.

Important practices include:

- Use least-privilege IAM permissions.
- Restrict access to CloudWatch resources.
- Protect application logs.
- Configure appropriate log retention.
- Avoid storing sensitive information in logs.
- Monitor CloudWatch Alarms.
- Use encryption where appropriate.
- Review IAM permissions regularly.
- Monitor important AWS resources.
- Create meaningful alarms.
- Remove unnecessary monitoring resources.

### Example

```text
IAM
 |
 v
CloudWatch Permissions
 |
 +---- Metrics
 +---- Logs
 +---- Alarms
 +---- Dashboards
```

### Result

**Successfully understood important security practices for CloudWatch monitoring and logging.**

---

## 34. CloudWatch Complete Architecture

```text
                              AWS Resources
                                  |
             +--------------------+--------------------+
             |                    |                    |
             v                    v                    v
            EC2                  RDS              Load Balancer
             |                    |                    |
             +--------------------+--------------------+
                                  |
                                  v
                            CloudWatch
                                  |
              +-------------------+-------------------+
              |                   |                   |
              v                   v                   v
           Metrics               Logs              Alarms
              |                   |                   |
              v                   v                   v
         Dashboards          Log Groups             SNS
                                  |                   |
                                  v                   v
                            Log Streams          Notifications
```

---

## 35. Complete CloudWatch Workflow

### Workflow

```text
Create AWS Resource
        |
        v
Generate Metrics / Logs
        |
        v
CloudWatch
        |
        +---- Metrics
        |
        +---- Logs
        |
        +---- Dashboards
        |
        +---- Alarms
        |
        v
Monitor Resource
        |
        v
Detect Threshold / Problem
        |
        v
Notification / Automated Action
        |
        v
Troubleshoot / Scale / Recover
```

### Practical Steps

1. Launch or select an AWS resource.
2. Open CloudWatch.
3. Review available metrics.
4. Select the required resource.
5. Monitor CPU utilization.
6. Monitor network activity.
7. Monitor status checks.
8. Create a CloudWatch Dashboard.
9. Add important metrics.
10. Create CloudWatch Alarms.
11. Configure appropriate thresholds.
12. Configure SNS notifications when required.
13. Create Log Groups when application logs are required.
14. Configure log collection.
15. Review Log Streams.
16. Review Log Events.
17. Install and configure CloudWatch Agent when additional EC2 metrics or logs are required.
18. Monitor RDS metrics when using RDS.
19. Monitor Load Balancer metrics when using a Load Balancer.
20. Use CloudWatch metrics with Auto Scaling when required.
21. Review alarms regularly.
22. Investigate abnormal metrics and logs.
23. Apply corrective actions.
24. Remove unused monitoring resources after completing the lab.

### Final Result

**Successfully completed Lab 15 - Amazon CloudWatch and understood how CloudWatch provides monitoring and observability for AWS resources and applications. Learned about metrics, namespaces, dimensions, statistics, dashboards, alarms, logs, Log Groups, Log Streams, CloudWatch Agent, EC2 monitoring, CPU and network metrics, SNS notifications, Auto Scaling integration, RDS monitoring, Load Balancer monitoring, troubleshooting, and CloudWatch security best practices.**
