# Stage 1 — Single EC2 Instance (Manual WordPress Setup)

> **Status:** 🔜 In Progress
> **Difficulty:** Beginner–Intermediate
> **Time to complete:** ~45–60 minutes

---

## 🎯 Objective

Build a fully functional WordPress blog **manually** on a single EC2 instance. This instance hosts everything — the application (Apache + PHP), the database (MySQL), and all content files — all in one place.

The goal of this stage is **not efficiency** — it is **understanding**. By building everything by hand, you learn exactly what WordPress needs to run, which sets you up to automate, separate, and scale each component in later stages.

---

## 🏗️ Architecture Diagram

> 📐 See [`diagrams/stage-01-architecture.png`](./diagrams/stage-01-architecture.png)

```
         Internet
             ↓
    ┌─────────────────────┐
    │     EC2 Instance    │
    │                     │
    │  Apache + PHP       │
    │  WordPress App      │
    │  MySQL Database     │
    │  /wp-content/       │
    └─────────────────────┘
```

---

## ⚠️ Limitations of This Architecture

| Issue | Impact |
|-------|--------|
| Single point of failure | If the instance goes down, the whole site goes down |
| No scaling | Cannot handle traffic spikes |
| Data loss risk | Terminating the instance destroys all data |
| No redundancy | No failover across Availability Zones |

These limitations are exactly what the next four stages solve.

---

## 📋 Prerequisites

- AWS account with admin access
- Northern Virginia (us-east-1) region selected
- Base VPC infrastructure deployed via CloudFormation one-click link
  > 🔗 *(Add the CloudFormation one-click link from Adrian's GitHub here)*

---

## 🛠️ Steps Completed

- [ ] Base VPC infrastructure deployed via CloudFormation
- [ ] EC2 instance launched (Amazon Linux 2, t2.micro)
- [ ] Security Group configured (HTTP port 80 inbound)
- [ ] Apache web server installed and started
- [ ] PHP and required modules installed
- [ ] MySQL installed and secured
- [ ] WordPress database and user created in MySQL
- [ ] WordPress downloaded and configured
- [ ] WordPress installation wizard completed via browser

---

## 📸 Screenshots

| Step | File |
|------|------|
| CloudFormation stack complete | `screenshots/01-cfn-stack-complete.png` |
| EC2 instance running | `screenshots/02-ec2-running.png` |
| WordPress install screen | `screenshots/03-wp-install.png` |
| WordPress live | `screenshots/04-wp-live.png` |

---

## 🎥 Video Walkthrough

> 🔜 YouTube video coming soon

---

## 📝 Key Learnings

*(To be filled in after completing this stage)*

---

## ➡️ Next Stage

[Stage 2 — Launch Template →](../stage-02-launch-template/README.md)
