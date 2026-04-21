# 🚀 AWS WordPress Architectural Evolution

> A hands-on project documenting the evolution of a WordPress deployment from a **single EC2 instance** to a **fully elastic, self-healing, scalable AWS architecture** — step by step.

[![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazon-aws)](https://aws.amazon.com/)
[![WordPress](https://img.shields.io/badge/WordPress-Blog-blue?logo=wordpress)](https://wordpress.org/)
[![Stages](https://img.shields.io/badge/Stages-5-green)]()
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)]()
[![Attribution](https://img.shields.io/badge/Based%20on-Adrian%20Cantrill's%20Course-red)](https://learn.cantrill.io)

---

## 📖 About This Project

This repository documents my hands-on journey through a **real-world AWS architectural evolution project**. Starting with a single EC2 instance hosting everything (app, database, and content), the architecture progressively evolves through five stages until it is fully elastic and resilient — the kind of architecture you would find in production environments.

This project is designed to:
- Reinforce AWS certifications with **practical, real-world experience**
- Serve as a **portfolio piece** for cloud engineering and solutions architect roles
- Help others learn by documenting **every step, screenshot, and decision**
- Demonstrate **architectural thinking** — not just clicking through consoles

> 🎓 **Course Credit:** This project is based on the Advanced Demo lesson from [Adrian Cantrill's AWS SysOps Administrator course](https://learn.cantrill.io). Adrian is one of the most respected AWS instructors in the industry, and this demo series is one of the best practical exercises available for AWS learners. All architectural concepts and lab scenarios are his — this repo documents my own implementation, notes, and learnings.

---

## 🎥 YouTube Series

I am documenting this entire project as a YouTube series. Each stage has a dedicated video walking through the implementation.

| Stage | Part | Title | Link |
| ----- | ---- | ----- | ---- |
| Stage 1 | Part 1 | Project Introduction and Architecture Walkthrough | [Watch](https://youtu.be/Kkt6g5VyWKU) |
| Stage 1 | Part 2 | Architecture Diagram Deep Dive | [Watch](https://youtu.be/Ngjx2LWfYFY) |
| Stage 1 | Part 3 | AWS Console — Infrastructure Setup and SSM Parameters | 🔜 Coming Soon |
| Stage 1 | Part 4 | AWS Console — WordPress Installation and Verification | 🔜 Coming Soon |
| Stage 2 | | Launch Template | 🔜 Coming Soon |
| Stage 3 | | RDS Migration | 🔜 Coming Soon |
| Stage 4 | | EFS Migration | 🔜 Coming Soon |
| Stage 5 | | Auto Scaling + ALB | 🔜 Coming Soon |

> 📌 Subscribe and turn on notifications so you don't miss an upload!

---

## 🏗️ Architecture Evolution Overview

The architecture evolves across **5 progressive stages**:

```
Stage 1 → Stage 2 → Stage 3 → Stage 4 → Stage 5
  EC2        EC2       EC2       EC2      ASG + ALB
(manual)  (template)   +RDS    +RDS+EFS  +RDS+EFS
```

### Stage Summary

| Stage | What Changes | Key AWS Services |
|-------|-------------|-----------------|
| [Stage 1](./stages/stage-01-single-ec2/) | Manual WordPress on one EC2 instance | EC2, VPC |
| [Stage 2](./stages/stage-02-launch-template/) | Automate provisioning with Launch Template | EC2, Launch Templates |
| [Stage 3](./stages/stage-03-rds-migration/) | Move database off EC2 to dedicated RDS | RDS, MySQL |
| [Stage 4](./stages/stage-04-efs-migration/) | Move content storage to shared EFS | EFS, NFS |
| [Stage 5](./stages/stage-05-autoscaling-alb/) | Full elasticity with ASG and Load Balancer | ALB, Auto Scaling Group |

---

## 📁 Repository Structure

```
aws-wordpress-arch-evolution/
│
├── README.md                        ← You are here
├── ATTRIBUTION.md                   ← Full credit to Adrian Cantrill
├── CHANGELOG.md                     ← Project progress log
├── LICENSE                          ← CC BY 4.0
│
├── docs/
│   ├── architecture-overview.md     ← Deep dive on all 5 stages
│   └── aws-services-reference.md    ← Quick reference for services used
│
├── scripts/                         ← Any helper scripts used
│
└── stages/
    ├── stage-01-single-ec2/
    │   ├── README.md                ← Stage write-up & learnings
    │   ├── diagrams/                ← Architecture diagram you created for this stage
    │   └── screenshots/             ← Your AWS console screenshots for this stage
    ├── stage-02-launch-template/
    │   ├── README.md
    │   ├── diagrams/
    │   └── screenshots/
    ├── stage-03-rds-migration/
    │   ├── README.md
    │   ├── diagrams/
    │   └── screenshots/
    ├── stage-04-efs-migration/
    │   ├── README.md
    │   ├── diagrams/
    │   └── screenshots/
    └── stage-05-autoscaling-alb/
        ├── README.md
        ├── diagrams/
        └── screenshots/
```

---

## ✅ Progress Tracker

- [ ] **Stage 1** – Single EC2 Instance (Manual WordPress Setup)
- [ ] **Stage 2** – Launch Template (Automated Provisioning)
- [ ] **Stage 3** – RDS Migration (Dedicated Database)
- [ ] **Stage 4** – EFS Migration (Shared File System)
- [ ] **Stage 5** – Auto Scaling Group + Application Load Balancer

---

## 🛠️ Prerequisites

To follow along with this project, you will need:

- An **AWS account** with administrator access
- The **Northern Virginia (us-east-1)** region selected
- Basic understanding of **EC2, VPC, and Linux**
- The base infrastructure CloudFormation stack (link in each stage's README)

---

## 🤝 Attribution & Disclaimer

This project is based on the **Advanced Demo lesson** from Adrian Cantrill's AWS SysOps Administrator course available at [learn.cantrill.io](https://learn.cantrill.io).

- **All architectural concepts, lab design, and course content** belong to Adrian Cantrill.
- **This repository** represents my personal implementation, documentation, and notes.
- No proprietary course content is reproduced here — only my own work, screenshots, and commentary.

See [ATTRIBUTION.md](./ATTRIBUTION.md) for full details.

---

## 📬 Connect With Me

- **GitHub:** [@noble-antwi](https://github.com/noble-antwi)
- **YouTube:** *(link coming soon)*
- **LinkedIn:** *(link coming soon)*

---

*⭐ If this helps you on your AWS journey, consider starring the repo — it really helps!*
