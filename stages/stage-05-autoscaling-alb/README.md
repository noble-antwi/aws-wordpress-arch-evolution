# Stage 5 — Auto Scaling Group + Application Load Balancer

> **Status:** 🔒 Locked — Complete Stages 1–4 first
> **Difficulty:** Advanced
> **Time to complete:** ~60 minutes

---

## 🎯 Objective

Complete the architectural evolution by introducing an **Application Load Balancer (ALB)** and an **Auto Scaling Group (ASG)**. This final stage makes the WordPress deployment fully elastic, self-healing, and highly available across multiple Availability Zones.

---

## 🏗️ Architecture Diagram

> 📐 See [`diagrams/stage-05-architecture.png`](./diagrams/stage-05-architecture.png)

```
                Internet
                    ↓
      ┌─────────────────────────┐
      │  Application Load       │
      │  Balancer (ALB)         │
      └──────┬──────┬──────┬───┘
             │      │      │
          EC2-1  EC2-2  EC2-3   ← Auto Scaling Group
             │      │      │
             └──────┼──────┘
                    │
         ┌──────────┴──────────┐
         ↓                     ↓
   ┌──────────┐        ┌──────────────┐
   │ Amazon   │        │ Amazon EFS   │
   │ RDS      │        │ /wp-content/ │
   └──────────┘        └──────────────┘
```

---

## 🔄 What Changes from Stage 4

| Stage 4 | Stage 5 |
|---------|---------|
| Customers connect directly to EC2 IP | Customers connect to ALB DNS name |
| Single EC2 instance | Multiple EC2 instances managed by ASG |
| Manual scaling required | Automatic scaling based on load |
| Instance failure = downtime | Instance failure = automatic replacement |
| Single Availability Zone | Multi-AZ — fully resilient |

---

## ✅ Properties of the Final Architecture

| Property | How It Is Achieved |
|----------|--------------------|
| **Self-healing** | ASG detects failed instances and replaces them automatically |
| **Elastic** | ASG scales out under high load, scales in when load drops |
| **Highly Available** | ALB and ASG span multiple Availability Zones |
| **Stateless Compute** | Any instance can serve any request (DB on RDS, content on EFS) |
| **Persistent Data** | RDS and EFS exist independently of any EC2 instance |

---

## 📋 Prerequisites

- Stages 1–4 completed
- RDS running and connected to WordPress
- EFS mounted and containing wp-content
- Launch Template updated from Stage 4

---

## 🛠️ Steps Completed

- [ ] ALB Security Group created (allow port 80 from internet)
- [ ] Application Load Balancer provisioned (across multiple AZs)
- [ ] Target Group created with health check settings
- [ ] ALB Listener configured (port 80 → Target Group)
- [ ] Auto Scaling Group created using the Launch Template
- [ ] ASG linked to the Target Group
- [ ] Scaling policies configured (CPU-based)
- [ ] WordPress URL updated to ALB DNS name
- [ ] All instances passing health checks verified
- [ ] Scale-out test performed
- [ ] Self-healing test — instance terminated and auto-replaced

---

## 📸 Screenshots

| Step | File |
|------|------|
| ALB configuration | `screenshots/01-alb-config.png` |
| Target Group health checks | `screenshots/02-target-group-healthy.png` |
| Auto Scaling Group settings | `screenshots/03-asg-config.png` |
| Multiple instances healthy | `screenshots/04-instances-healthy.png` |
| WordPress via ALB DNS | `screenshots/05-wp-via-alb.png` |
| Scale-out event in CloudWatch | `screenshots/06-scale-out-event.png` |
| Self-healing — instance replaced | `screenshots/07-self-healing.png` |

---

## 🎥 Video Walkthrough

> 🔜 YouTube video coming soon

---

## 📝 Key Learnings

*(To be filled in after completing this stage)*

---

## 🏁 Project Complete!

You have built a **production-grade, fully elastic, self-healing AWS architecture** from scratch — and you understand every component and every decision that went into it.

👉 See the full [Architecture Overview](../../docs/architecture-overview.md) for a summary of the entire journey.
