# Stage 2 — Launch Template (Automated Provisioning)

> **Status:** 🔒 Locked — Complete Stage 1 first
> **Difficulty:** Intermediate
> **Time to complete:** ~30 minutes

---

## 🎯 Objective

Replace the manual EC2 setup from Stage 1 with an **EC2 Launch Template** that automatically provisions a fully configured WordPress instance using a **User Data script**. The architecture still uses a single instance, but it can now be recreated on demand without any manual work.

---

## 🏗️ Architecture Diagram

> 📐 See [`diagrams/stage-02-architecture.png`](./diagrams/stage-02-architecture.png)

```
         Internet
             ↓
    ┌──────────────────────────┐
    │   EC2 (Launch Template)  │
    │                          │
    │  Auto-provisioned via    │
    │  User Data script        │
    │  (App + DB + Content)    │
    └──────────────────────────┘
```

---

## 🔄 What Changes from Stage 1

| Stage 1 | Stage 2 |
|---------|---------|
| Everything installed manually via SSH | Everything installed automatically via User Data |
| Instance cannot be easily replaced | Instance can be terminated and relaunched identically |
| Rebuild takes ~60 minutes of manual work | Rebuild is fully automatic on launch |

---

## 📋 Prerequisites

- Stage 1 completed and understood
- WordPress configuration details from Stage 1 (DB name, user, password)

---

## 🛠️ Steps Completed

- [ ] Launch Template created with Amazon Linux 2 AMI
- [ ] User Data script written to install Apache, PHP, MySQL, WordPress
- [ ] Security Group attached to Launch Template
- [ ] New instance launched from the Launch Template
- [ ] WordPress accessible via the new instance's public IP
- [ ] Old manual instance terminated

---

## 📸 Screenshots

| Step | File |
|------|------|
| Launch Template configuration | `screenshots/01-launch-template-config.png` |
| User Data script | `screenshots/02-user-data.png` |
| New instance launching | `screenshots/03-instance-launching.png` |
| WordPress running from template | `screenshots/04-wp-from-template.png` |

---

## 🎥 Video Walkthrough

> 🔜 YouTube video coming soon

---

## 📝 Key Learnings

*(To be filled in after completing this stage)*

---

## ➡️ Next Stage

[Stage 3 — RDS Migration →](../stage-03-rds-migration/README.md)
