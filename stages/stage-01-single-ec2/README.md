# Stage 1 — Single EC2 Instance

> **Status:** In Progress
> **Difficulty:** Beginner–Intermediate
> **Estimated lab time:** ~60–90 minutes

---

## Video Series for This Stage

| Part | Title | Link |
| ---- | ----- | ---- |
| Part 1 | Project Introduction and Architecture Walkthrough | [Watch on YouTube](https://youtu.be/Kkt6g5VyWKU) |
| Part 2 | Architecture Diagram Deep Dive | [Watch on YouTube](https://youtu.be/Ngjx2LWfYFY) |
| Part 3 | AWS Console — Infrastructure Setup and SSM Parameters | Coming Soon |
| Part 4 | AWS Console — WordPress Installation and Verification | Coming Soon |

---

## Objective

Build a fully functional WordPress blog manually on a single EC2 instance. This instance hosts everything — the web server (Apache + PHP), the database (MySQL), and all content files — in one place.

The goal is not efficiency. It is understanding. By building this by hand, you experience exactly what WordPress needs to run, and you feel the limitations of this approach first-hand. Those limitations are the motivation for everything that follows in Stages 2–5.

---

## Architecture

![Stage 1 Architecture](./diagrams/aws-wordpress-arch-evolution-stage-1.drawio.png)

**What gets deployed:**

- A4L VPC (`10.16.0.0/16`) with public, app, and database subnets across three Availability Zones
- An Internet Gateway attached to the VPC
- One EC2 instance (`WordPress-manual`) in the public subnet of `us-east-1a`
- Apache, PHP, MySQL, and WordPress — all installed on that single instance
- SSM Parameter Store entries to hold database credentials and configuration

**Why a three-tier VPC for a single instance?**

The VPC is designed for the full five-stage architecture. It is deployed once in Stage 1 and built upon throughout the series. The database and app subnets are unused in Stage 1 but are required from Stage 3 onwards.

---

## Limitations of This Architecture

| Problem | Consequence |
| ------- | ----------- |
| Single point of failure | One instance crash brings the entire site down |
| No scaling | Cannot handle traffic spikes |
| Data tied to the instance | Terminating the instance destroys the database and all media |
| Manual rebuild required | Every recovery means repeating all these steps by hand |
| No Availability Zone redundancy | One AZ outage takes down everything |

These are not hypothetical concerns. They are the exact problems that Stages 2–5 solve, one at a time.

---

## Prerequisites

- IAM admin user logged in (use the management/general AWS account — not a restricted account)
- Region set to **us-east-1 (Northern Virginia)**
- Base VPC stack deployed via CloudFormation before starting the steps below

---

## Implementation

### Step 1 — Deploy the Base VPC

1. Go to **AWS Console → CloudFormation → Create stack → With new resources**
2. Choose **Upload a template file** and upload [`cloudformation/A4LVPC.yaml`](../../cloudformation/A4LVPC.yaml)
3. Stack name: `A4LVPC`
4. Scroll to the bottom and check the **IAM capabilities acknowledgement** box
5. Click **Create stack**
6. Wait for the status to reach **CREATE_COMPLETE** before continuing

This stack provisions the full VPC, all subnets, the Internet Gateway, security groups, IAM roles, and the CloudWatch agent SSM configuration used in later stages.

---

### Step 2 — Launch the EC2 Instance

1. Go to **AWS Console → EC2 → Launch Instance**
2. Set the following:

| Setting | Value |
| ------- | ----- |
| Name | `WordPress-manual` |
| AMI | Amazon Linux 2023 (64-bit x86) — confirm Free tier eligible |
| Instance type | `t2.micro` (or any free tier eligible equivalent) |
| Key pair | Proceed without a key pair |
| VPC | `A4LVPC` |
| Subnet | `sn-pub-A` |
| Auto-assign public IP | Enable |
| Auto-assign IPv6 IP | Enable |
| Security group | Select existing — `a4l-vpc-sg-wordpress` |
| Storage | 8 GiB gp3 (default — no changes needed) |
| IAM instance profile | `a4l-vpc-WordpressInstanceProfile-...` |
| Credit specification | Unlimited (use Standard if your account is new) |

1. Click **Launch Instance**

> We connect to this instance via Session Manager — no SSH key is needed. If your AWS account is brand new, select Standard for credit specification. Unlimited may not be available until the account has a billing history. If you select Unlimited and receive an error, repeat this step with Standard instead.

---

### Step 3 — Create SSM Parameter Store Parameters

While the EC2 instance initialises, set up the SSM parameters. WordPress will read these at install time, and the automated build scripts in later stages will also use them.

Go to **AWS Console → Systems Manager → Parameter Store**.

> If you have any existing parameters beginning with `/A4L`, delete them before continuing.

Create the following five parameters one by one:

#### /A4L/WordPress/DBUser

| Field | Value |
| ----- | ----- |
| Name | `/A4L/WordPress/DBUser` |
| Description | `WordPress database user` |
| Tier | Standard |
| Type | String |
| Value | `a4lwordpressuser` |

#### /A4L/WordPress/DBName

| Field | Value |
| ----- | ----- |
| Name | `/A4L/WordPress/DBName` |
| Description | `WordPress database name` |
| Tier | Standard |
| Type | String |
| Value | `a4lWordPressDB` |

#### /A4L/WordPress/DBEndpoint

| Field | Value |
| ----- | ----- |
| Name | `/A4L/WordPress/DBEndpoint` |
| Description | `WordPress endpoint name` |
| Tier | Standard |
| Type | String |
| Value | `localhost` |

> This is `localhost` in Stage 1 because the database runs on the same instance as the application. In Stage 3, when we migrate to RDS, this value is updated to the RDS endpoint — and nothing else in the configuration needs to change.

#### /A4L/WordPress/DBPassword

| Field | Value |
| ----- | ----- |
| Name | `/A4L/WordPress/DBPassword` |
| Description | `WordPress DB password` |
| Tier | Standard |
| Type | SecureString |
| KMS key ID | `alias/aws/ssm` |
| Value | Use the strong password from the course instructions |

#### /A4L/WordPress/DBRootPassword

| Field | Value |
| ----- | ----- |
| Name | `/A4L/WordPress/DBRootPassword` |
| Description | `WordPress DB root password` |
| Tier | Standard |
| Type | SecureString |
| KMS key ID | `alias/aws/ssm` |
| Value | Use the same strong password as above for this demo |

Once all five are created, confirm they all appear in the Parameter Store list under `/A4L/WordPress/`.

---

### Step 4 — Install WordPress on the EC2 Instance

To be documented after recording Part 4.

---

## Key Learnings

To be filled in after completing this stage.

---

## Next Stage

[Stage 2 — Launch Template](../stage-02-launch-template/README.md)
