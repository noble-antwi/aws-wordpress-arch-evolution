# Stage 3 — RDS Migration

> **Status:** Locked — Complete Stages 1 and 2 first
> **Difficulty:** Intermediate
> **Estimated lab time:** ~45 minutes

---

## Video Walkthrough

Coming Soon

---

## Objective

Move the MySQL database off the EC2 instance and onto a dedicated Amazon RDS instance. This is the first major step in separating the architecture's components and making the EC2 layer stateless.

---

## Architecture

> See [`diagrams/stage-03-architecture.png`](./diagrams/stage-03-architecture.png)

```text
         Internet
             |
    [ EC2 Instance ]
    (App + Content)
             |  MySQL connection
             |
    [ Amazon RDS — MySQL ]
```

---

## What Changes from Stage 2

| Stage 2 | Stage 3 |
| ------- | ------- |
| MySQL runs on EC2 | MySQL runs on dedicated RDS |
| DB data lost if instance is terminated | DB data persists independently of EC2 |
| No automated DB backups | RDS provides automated backups |
| App and DB fail together | DB failure is isolated from the app layer |

---

## Prerequisites

- Stages 1 and 2 completed
- Base VPC with private DB subnets (from CloudFormation)
- WordPress database credentials from Stage 1

---

## Steps

- [ ] DB Subnet Group created (spanning multiple AZs)
- [ ] RDS Security Group created (allow port 3306 from EC2 SG only)
- [ ] RDS MySQL instance provisioned
- [ ] Database migrated from EC2 to RDS (mysqldump)
- [ ] WordPress `wp-config.php` updated with RDS endpoint
- [ ] SSM Parameter `/A4L/WordPress/DBEndpoint` updated to RDS endpoint
- [ ] Connection to RDS verified
- [ ] MySQL service disabled on EC2 instance
- [ ] Launch Template updated with RDS endpoint

---

## Key Learnings

To be filled in after completing this stage.

---

## Next Stage

[Stage 4 — EFS Migration](../stage-04-efs-migration/README.md)
