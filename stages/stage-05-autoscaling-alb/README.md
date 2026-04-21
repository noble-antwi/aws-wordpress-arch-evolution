# Stage 5 — Auto Scaling Group + Application Load Balancer

> **Status:** Locked — Complete Stages 1–4 first
> **Difficulty:** Advanced
> **Estimated lab time:** ~60 minutes

---

## Video Walkthrough

Coming Soon

---

## Objective

Complete the architectural evolution by introducing an Application Load Balancer (ALB) and an Auto Scaling Group (ASG). This final stage makes the WordPress deployment fully elastic, self-healing, and highly available across multiple Availability Zones.

---

## Architecture

> See [`diagrams/stage-05-architecture.png`](./diagrams/stage-05-architecture.png)

```text
                Internet
                    |
      [ Application Load Balancer ]
         /          |          \
      EC2-1       EC2-2       EC2-3     (Auto Scaling Group)
         \          |          /
                    |
         ┌──────────┴──────────┐
         |                     |
   [ Amazon RDS ]       [ Amazon EFS ]
     (MySQL)             (/wp-content/)
```

---

## What Changes from Stage 4

| Stage 4 | Stage 5 |
| ------- | ------- |
| Customers connect directly to EC2 IP | Customers connect to ALB DNS name |
| Single EC2 instance | Multiple EC2 instances managed by ASG |
| Manual scaling required | Automatic scaling based on load |
| Instance failure causes downtime | Instance failure triggers automatic replacement |
| Single Availability Zone | Multi-AZ — fully resilient |

---

## Properties of the Final Architecture

| Property | How It Is Achieved |
| -------- | ------------------ |
| Self-healing | ASG detects failed instances and replaces them automatically |
| Elastic | ASG scales out under high load, scales in when load drops |
| Highly Available | ALB and ASG span multiple Availability Zones |
| Stateless Compute | Any instance can serve any request (DB on RDS, content on EFS) |
| Persistent Data | RDS and EFS exist independently of any EC2 instance |

---

## Prerequisites

- Stages 1–4 completed
- RDS running and connected to WordPress
- EFS mounted and containing wp-content
- Launch Template updated from Stage 4

---

## Steps

- [ ] ALB Security Group created (allow port 80 from internet)
- [ ] Application Load Balancer provisioned (across multiple AZs)
- [ ] Target Group created with health check settings
- [ ] ALB Listener configured (port 80 to Target Group)
- [ ] Auto Scaling Group created using the Launch Template
- [ ] ASG linked to the Target Group
- [ ] Scaling policies configured (CPU-based)
- [ ] WordPress URL updated to ALB DNS name
- [ ] All instances passing health checks verified
- [ ] Scale-out test performed
- [ ] Self-healing test — instance terminated and auto-replaced

---

## Key Learnings

To be filled in after completing this stage.

---

## Project Complete

You have built a production-grade, fully elastic, self-healing AWS architecture from scratch — and you understand every component and every decision that went into it.

See the full [Architecture Overview](../../docs/architecture-overview.md) for a summary of the entire journey.
