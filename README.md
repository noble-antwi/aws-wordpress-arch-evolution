# AWS WordPress Architectural Evolution

> A hands-on project documenting the evolution of a WordPress deployment from a single EC2 instance to a fully elastic, self-healing, scalable AWS architecture — step by step.

[![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)](https://aws.amazon.com/)
[![WordPress](https://img.shields.io/badge/WordPress-Blog-blue?logo=wordpress)](https://wordpress.org/)
[![Stages](https://img.shields.io/badge/Stages-5-green)](https://github.com/noble-antwi/aws-wordpress-arch-evolution)
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)](https://github.com/noble-antwi/aws-wordpress-arch-evolution)
[![Attribution](https://img.shields.io/badge/Based%20on-Adrian%20Cantrill's%20Course-red)](https://learn.cantrill.io)

---

## About This Project

This repository documents my hands-on journey through a real-world AWS architectural evolution project. Starting with a single EC2 instance hosting everything (app, database, and content), the architecture progressively evolves through five stages until it is fully elastic and resilient — the kind of architecture you would find in production environments.

This project is designed to:

- Reinforce AWS certifications with practical, real-world experience
- Serve as a portfolio piece for cloud engineering and solutions architect roles
- Help others learn by documenting every step and decision
- Demonstrate architectural thinking — not just clicking through consoles

> **Course Credit:** This project is based on the Advanced Demo lesson from [Adrian Cantrill's AWS SysOps Administrator course](https://learn.cantrill.io). Adrian is one of the most respected AWS instructors in the industry, and this demo series is one of the best practical exercises available for AWS learners. All architectural concepts and lab scenarios are his — this repo documents my own implementation, notes, and learnings.

---

## YouTube Series

I am documenting this entire project as a YouTube series.

| Stage | Part | Title | Link |
| ----- | ---- | ----- | ---- |
| Stage 1 | Part 1 | Project Introduction and Architecture Walkthrough | [Watch](https://youtu.be/Ngjx2LWfYFY?si=YH5znZg8kpX9SShD) |
| Stage 1 | Part 2 | Architecture Diagram Deep Dive | [Watch](https://youtu.be/Kkt6g5VyWKU?si=8_NCv8HnA4Mp6e5i) |
| Stage 1 | Part 3 | Deploying the Base Infrastructure with CloudFormation | [Watch](https://youtu.be/hPf9r07op5w) |
| Stage 1 | Part 4 | Launching the EC2 Instance | [Watch](https://youtu.be/Zv2jIfefBjg) |
| Stage 1 | Part 5 | Configuring SSM Parameter Store | [Watch](https://youtu.be/i3q5NDssjC8) |
| Stage 1 | Part 6 | Installing WordPress and Exposing the Limitations | [Watch](https://youtu.be/z3AEENtFhBs) |
| Stage 2 | | Launch Template | Coming Soon |
| Stage 3 | | RDS Migration | Coming Soon |
| Stage 4 | | EFS Migration | Coming Soon |
| Stage 5 | | Auto Scaling + ALB | Coming Soon |

---

## Architecture Evolution Overview

The architecture evolves across five progressive stages:

```text
Stage 1 → Stage 2 → Stage 3 → Stage 4 → Stage 5
  EC2        EC2       EC2       EC2      ASG + ALB
(manual)  (template)   +RDS    +RDS+EFS  +RDS+EFS
```

### Stage Summary

| Stage | What Changes | Key AWS Services |
| ----- | ------------ | ---------------- |
| [Stage 1](./stages/stage-01-single-ec2/) | Manual WordPress on one EC2 instance | EC2, VPC |
| [Stage 2](./stages/stage-02-launch-template/) | Automate provisioning with a Launch Template | EC2, Launch Templates |
| [Stage 3](./stages/stage-03-rds-migration/) | Move the database off EC2 to dedicated RDS | RDS, MySQL |
| [Stage 4](./stages/stage-04-efs-migration/) | Move content storage to shared EFS | EFS, NFS |
| [Stage 5](./stages/stage-05-autoscaling-alb/) | Full elasticity with ASG and Load Balancer | ALB, Auto Scaling Group |

---

## Repository Structure

```text
aws-wordpress-arch-evolution/
│
├── README.md                        ← You are here
├── ATTRIBUTION.md                   ← Full credit to Adrian Cantrill
├── LICENSE                          ← CC BY 4.0
│
├── cloudformation/
│   └── A4LVPC.yaml                  ← Base VPC stack (deployed once, used across all stages)
│
├── docs/
│   ├── architecture-overview.md     ← Deep dive on all 5 stages
│   └── aws-services-reference.md    ← Quick reference for services used
│
├── scripts/                         ← Helper scripts
│
└── stages/
    ├── stage-01-single-ec2/
    │   ├── README.md                ← Stage write-up and implementation steps
    │   ├── diagrams/                ← Architecture diagram for this stage
    │   └── screenshots/             ← AWS console screenshots
    ├── stage-02-launch-template/
    ├── stage-03-rds-migration/
    ├── stage-04-efs-migration/
    └── stage-05-autoscaling-alb/
```

---

## Progress Tracker

- [x] Stage 1 — Complete (6 videos published, full implementation documented)
- [ ] Stage 2 — Launch Template
- [ ] Stage 3 — RDS Migration
- [ ] Stage 4 — EFS Migration
- [ ] Stage 5 — Auto Scaling Group + Application Load Balancer

---

## Prerequisites

To follow along with this project, you will need:

- An AWS account with administrator access
- The Northern Virginia (us-east-1) region selected
- Basic understanding of EC2, VPC, and Linux
- The base infrastructure CloudFormation stack — see [cloudformation/A4LVPC.yaml](./cloudformation/A4LVPC.yaml)

---

## Attribution and Disclaimer

This project is based on the Advanced Demo lesson from Adrian Cantrill's AWS SysOps Administrator course at [learn.cantrill.io](https://learn.cantrill.io).

- All architectural concepts, lab design, and course content belong to Adrian Cantrill.
- This repository represents my personal implementation, documentation, and notes.
- No proprietary course content is reproduced here — only my own work and commentary.

See [ATTRIBUTION.md](./ATTRIBUTION.md) for full details.

---

## Connect With Me

- **GitHub:** [@noble-antwi](https://github.com/noble-antwi)
- **YouTube:** Coming Soon
- **LinkedIn:** Coming Soon

---

*If this helps you on your AWS journey, consider starring the repo.*
