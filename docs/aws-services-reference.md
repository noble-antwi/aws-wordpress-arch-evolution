# AWS Services Reference

A quick reference for every AWS service used across the five stages of this project.

---

## EC2 — Elastic Compute Cloud

**What it is:** Virtual servers in the AWS cloud.

**Used in:** Stages 1–5

Key concepts for this project:

- Instance types (t2.micro / t3.micro)
- Security Groups as instance-level firewalls
- User Data for bootstrapping on launch
- Amazon Machine Images (AMIs)

[EC2 Documentation](https://docs.aws.amazon.com/ec2/)

---

## VPC — Virtual Private Cloud

**What it is:** An isolated network environment in AWS where you launch resources.

**Used in:** All stages (pre-provisioned via CloudFormation)

Key concepts for this project:

- Public and private subnets
- Internet Gateway
- Route Tables
- Security Groups

[VPC Documentation](https://docs.aws.amazon.com/vpc/)

---

## EC2 Launch Templates

**What it is:** A reusable configuration for launching EC2 instances, including AMI, instance type, security groups, and User Data.

**Used in:** Stages 2–5

Key concepts for this project:

- User Data scripts for automated WordPress setup
- Versioning of launch templates
- Used by Auto Scaling Groups to launch instances

[Launch Templates Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-templates.html)

---

## RDS — Relational Database Service

**What it is:** A managed relational database service supporting MySQL, PostgreSQL, and others.

**Used in:** Stages 3–5

Key concepts for this project:

- MySQL engine
- DB Subnet Groups (requires subnets in multiple AZs)
- Multi-AZ deployment option
- Security Groups for database access control
- Endpoint DNS name for connection

[RDS Documentation](https://docs.aws.amazon.com/rds/)

---

## EFS — Elastic File System

**What it is:** A managed, scalable NFS file system that can be mounted on multiple EC2 instances simultaneously.

**Used in:** Stages 4–5

Key concepts for this project:

- Mount Targets per Availability Zone
- NFS protocol mounting
- EFS Security Groups
- Persistent storage independent of EC2 instances

[EFS Documentation](https://docs.aws.amazon.com/efs/)

---

## ALB — Application Load Balancer

**What it is:** A Layer 7 (HTTP/HTTPS) load balancer that distributes traffic across multiple targets.

**Used in:** Stage 5

Key concepts for this project:

- Listener rules (port 80 to Target Group)
- Target Groups with health checks
- Integration with Auto Scaling Groups
- DNS name as the public entry point

[ALB Documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/)

---

## Auto Scaling Group (ASG)

**What it is:** A group of EC2 instances that automatically scales based on demand and replaces unhealthy instances.

**Used in:** Stage 5

Key concepts for this project:

- Minimum, desired, and maximum capacity
- Launch Template integration
- Health checks (EC2 and ELB)
- Scaling policies (based on CPU, network, etc.)
- Multi-AZ distribution

[Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)

---

## CloudFormation

**What it is:** AWS Infrastructure-as-Code service for provisioning resources via templates.

**Used in:** Base infrastructure provisioning

Key concepts for this project:

- Stack creation
- Template upload
- Outputs (VPC ID, Subnet IDs, etc.)

[CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/)

---

## Security Groups

**What it is:** Virtual firewalls that control inbound and outbound traffic for AWS resources.

**Used in:** All stages

Key concepts for this project:

- Web tier SG: allows port 80 from internet
- App tier SG: allows traffic from ALB SG
- DB tier SG: allows port 3306 from app tier only
- EFS tier SG: allows NFS (port 2049) from app tier

---

*All documentation links point to the official AWS documentation.*
