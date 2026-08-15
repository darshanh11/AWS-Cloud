# Lab 01 - AWS Introduction

## Objective

To understand the fundamentals of Amazon Web Services (AWS), cloud computing, AWS Regions, Availability Zones, and the AWS Management Console.

## What is AWS?

Amazon Web Services (AWS) is a cloud computing platform provided by Amazon. It provides on-demand cloud services such as compute, storage, networking, databases, security, and monitoring over the internet.

## What is Cloud Computing?

Cloud computing is the delivery of computing resources such as servers, storage, databases, networking, and applications over the internet.

Instead of purchasing and maintaining physical infrastructure, organizations can use cloud resources on demand.

## AWS Service Models

### Infrastructure as a Service (IaaS)

Provides infrastructure resources such as virtual machines, storage, and networking.

**Example:** Amazon EC2

### Platform as a Service (PaaS)

Provides a platform for developing and deploying applications without managing the underlying infrastructure.

**Example:** AWS Elastic Beanstalk

### Software as a Service (SaaS)

Provides ready-to-use software applications through the internet.

## AWS Management Console

The AWS Management Console is a web-based interface used to create, configure, monitor, and manage AWS resources and services.

## AWS Regions

An AWS Region is a geographical location that contains multiple Availability Zones.

Examples:

- Asia Pacific (Mumbai)
- Asia Pacific (Singapore)
- US East (N. Virginia)
- Europe (Ireland)

The selected Region determines where AWS resources are deployed.

## Availability Zones

Availability Zones are isolated locations within an AWS Region.

A Region contains multiple Availability Zones to provide high availability and fault tolerance.

```text
AWS Region
│
├── Availability Zone 1
├── Availability Zone 2
└── Availability Zone 3
