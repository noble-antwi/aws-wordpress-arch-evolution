# Architecture Overview

This document provides a detailed breakdown of all five stages of the architectural evolution, explaining what changes, why it matters, and what problem it solves.

---

## The Problem We Start With

A WordPress blog running entirely on a single EC2 instance:

```text
┌─────────────────────────────┐
│         EC2 Instance        │
│  ┌────────┐  ┌───────────┐  │
│  │  App   │  │  MySQL DB │  │
│  │  PHP   │  │           │  │
│  └────────┘  └───────────┘  │
│  ┌───────────────────────┐  │
│  │   /wp-content/ files  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
          ↑
       Customers
```

Problems with this:

- Single point of failure — if the instance goes down, everything goes down
- Cannot scale — one instance handles all load regardless of demand
- Data is tied to the instance lifecycle — terminate the instance, lose everything
- No resilience across Availability Zones

---

## Stage 1 — Single EC2 Instance (Manual)

**Goal:** Understand every component needed to run WordPress manually.

```text
Internet → EC2 (App + DB + Content)
```

What you build:

- VPC with base infrastructure (via CloudFormation)
- EC2 instance running Amazon Linux 2023
- Apache, PHP, WordPress installed manually
- MySQL database running on the same instance
- WordPress content stored locally on the instance

Why this stage matters:
You need to understand what WordPress needs before you can automate or separate its components. This stage ensures you know exactly what is happening under the hood.

AWS Services Used: EC2, VPC (pre-provisioned via CloudFormation), Security Groups

---

## Stage 2 — Launch Template

**Goal:** Remove the manual work by automating instance provisioning.

```text
Internet → EC2 (from Launch Template — App + DB + Content still on instance)
```

What changes:

- A Launch Template is created that includes a User Data script
- The User Data script automatically installs and configures WordPress when a new instance launches
- You can now terminate and replace the instance without manually rebuilding it

Why this stage matters:
This is the foundation for autoscaling. You cannot have an autoscaling group without a launch template — instances need to be able to provision themselves without human intervention.

AWS Services Used: EC2 Launch Templates, EC2 User Data

---

## Stage 3 — RDS Migration

**Goal:** Move the database off the EC2 instance and onto a dedicated, managed database service.

```text
Internet → EC2 (App + Content) → RDS (MySQL)
```

What changes:

- An RDS MySQL instance is provisioned in a dedicated subnet
- The WordPress database is migrated from the EC2 instance to RDS
- WordPress is reconfigured to point to the RDS endpoint
- The MySQL service on the EC2 instance is stopped and removed

Why this stage matters:
The database is now outside the lifecycle of the EC2 instance. You can terminate, replace, or scale the EC2 instances without losing any data. RDS also provides automated backups, Multi-AZ failover, and managed maintenance.

AWS Services Used: RDS (MySQL), DB Subnet Groups, Security Groups (database tier)

---

## Stage 4 — EFS Migration

**Goal:** Move WordPress content files off the EC2 instance and onto a shared, resilient network file system.

```text
Internet → EC2 (App only) → RDS (MySQL)
                  |
                 EFS (wp-content/)
```

What changes:

- An EFS (Elastic File System) is provisioned across multiple Availability Zones
- The `/wp-content/` directory (themes, plugins, uploads) is migrated from the EC2 instance to EFS
- The EC2 instance mounts EFS on boot
- The Launch Template is updated to include the EFS mount on startup

Why this stage matters:
With both the database (RDS) and the content (EFS) now external to the EC2 instance, the instance itself is stateless. Any instance can serve any request because they all read from and write to the same shared file system.

AWS Services Used: EFS (Elastic File System), EFS Mount Targets, Security Groups (EFS tier)

---

## Stage 5 — Auto Scaling Group + Application Load Balancer

**Goal:** Make the architecture fully elastic, self-healing, and highly available.

```text
             Internet
                |
    Application Load Balancer
       /          |          \
    EC2-1       EC2-2       EC2-3    (Auto Scaling Group)
       \          |          /
              RDS (MySQL)
                  |
                 EFS
```

What changes:

- An Application Load Balancer (ALB) is placed in front of the instances
- An Auto Scaling Group (ASG) replaces the single instance
- The ASG uses the Launch Template to provision instances automatically
- Instances scale out when load increases, scale in when load decreases
- If an instance fails health checks, it is automatically terminated and replaced
- Customers connect to the ALB DNS name, never directly to instances

Why this stage matters:
This is the final, production-grade architecture. It is resilient, scalable, highly available, and self-healing.

AWS Services Used: Application Load Balancer (ALB), Target Groups, Auto Scaling Group (ASG), CloudWatch Alarms

---

## Final Architecture Summary

| Concern | Solution |
| ------- | -------- |
| Application Layer | EC2 instances in Auto Scaling Group |
| Database | Amazon RDS (MySQL) |
| Shared Content | Amazon EFS |
| Traffic Distribution | Application Load Balancer |
| Automatic Scaling | Auto Scaling Group + CloudWatch |
| Network | VPC with public/private subnets across AZs |
