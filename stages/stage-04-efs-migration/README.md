# Stage 4 — EFS Migration (Shared File System)

> **Status:** 🔒 Locked — Complete Stages 1–3 first
> **Difficulty:** Intermediate–Advanced
> **Time to complete:** ~45 minutes

---

## 🎯 Objective

Move the WordPress content directory (`/wp-content/`) from the EC2 instance's local storage onto **Amazon EFS** — a managed, scalable, shared network file system. After this stage, the EC2 instance is completely stateless.

---

## 🏗️ Architecture Diagram

> 📐 See [`diagrams/stage-04-architecture.png`](./diagrams/stage-04-architecture.png)

```
         Internet
             ↓
    ┌──────────────────┐
    │   EC2 Instance   │◄─── Mounts EFS on startup
    │   (App only)     │
    └────────┬─────────┘
             │
      ┌──────┴───────┐
      ↓              ↓
┌──────────┐  ┌────────────────┐
│ Amazon   │  │  Amazon EFS    │
│ RDS      │  │  /wp-content/  │
│ (MySQL)  │  │                │
└──────────┘  └────────────────┘
```

---

## 🔄 What Changes from Stage 3

| Stage 3 | Stage 4 |
|---------|---------|
| `wp-content/` lives on EC2 disk | `wp-content/` lives on EFS |
| Uploads and plugins lost if instance replaced | Content persists across instance replacements |
| Only one instance can write content | Multiple instances can read and write the same content |
| EC2 is partially stateful | EC2 is fully stateless |

---

## 📋 Prerequisites

- Stages 1–3 completed
- RDS instance running and connected to WordPress
- Base VPC with EFS-compatible subnets (from CloudFormation)

---

## 🛠️ Steps Completed

- [ ] EFS Security Group created (allow NFS port 2049 from EC2 SG)
- [ ] EFS file system created
- [ ] EFS Mount Targets created in each Availability Zone
- [ ] EFS mounted temporarily on EC2 instance
- [ ] WordPress `wp-content/` migrated to EFS
- [ ] EC2 `/etc/fstab` updated for persistent EFS mount on reboot
- [ ] Launch Template updated to mount EFS on startup
- [ ] WordPress functionality verified (themes, uploads, plugins working)

---

## 📸 Screenshots

| Step | File |
|------|------|
| EFS file system creation | `screenshots/01-efs-creation.png` |
| Mount Targets configured | `screenshots/02-mount-targets.png` |
| EFS mounted on EC2 | `screenshots/03-efs-mounted.png` |
| Content migrated to EFS | `screenshots/04-content-migrated.png` |
| WordPress working with EFS | `screenshots/05-wp-efs-working.png` |

---

## 🎥 Video Walkthrough

> 🔜 YouTube video coming soon

---

## 📝 Key Learnings

*(To be filled in after completing this stage)*

---

## ➡️ Next Stage

[Stage 5 — Auto Scaling + ALB →](../stage-05-autoscaling-alb/README.md)
