# aws-cloudformation-templates

Production-tested AWS CloudFormation templates built from real infrastructure work across SaaS and HRTech products. All templates are standalone, parameterised, and ready to deploy via AWS CLI or the CloudFormation console.

> These templates were used in live production environments — not created for demo purposes.

---

## 📁 Templates in this repo

| File | What it creates |
|---|---|
| `vpc-with-subnets.yml` | VPC with public/private subnets, IGW, route tables |
| `ec2-instance.yml` | EC2 instance with security group, key pair, and IAM profile |
| `alb-load-balancer.yml` | Application Load Balancer with listener, target group, and health check |
| `rds-database.yml` | RDS database instance with subnet group, SG, and automated backups |
| `lambda-function.yml` | Lambda function with IAM execution role and basic configuration |
| `lambda-with-trigger.yml` | Lambda with event trigger (S3 or CloudWatch Events) |
| `s3-bucket.yml` | S3 bucket with versioning, encryption, and access policy |
| `full-stack-template.yml` | Full application stack — VPC + EC2 + ALB + RDS in one template |
| `ec2-vpc-full-stack.yml` | Complete EC2 deployment inside a VPC with networking components |

---

## 🚀 How to deploy

All templates accept parameters. Deploy via AWS CLI:

```bash
# Example: Deploy VPC stack
aws cloudformation deploy \
  --template-file vpc-with-subnets.yml \
  --stack-name my-vpc-stack \
  --parameter-overrides \
    Environment=production \
  --region ap-south-1

# Example: Deploy RDS stack
aws cloudformation deploy \
  --template-file rds-database.yml \
  --stack-name my-rds-stack \
  --parameter-overrides \
    Environment=production \
    DBInstanceClass=db.t3.micro \
    DBName=myappdb \
  --capabilities CAPABILITY_IAM \
  --region ap-south-1
```

Or deploy via the AWS Console:
1. Go to CloudFormation → Create stack → Upload a template file
2. Select the `.yml` file → Next
3. Fill in the parameters → Next → Create stack

---

## 🔍 Template highlights

### vpc-with-subnets.yml
Creates a complete VPC networking foundation:
- VPC with configurable CIDR block
- Public and private subnets
- Internet Gateway with route table
- Outputs: VPC ID, Subnet IDs (used as inputs for other stacks)

---

### alb-load-balancer.yml
Application Load Balancer setup including:
- ALB with internet-facing scheme
- HTTP/HTTPS listener configuration
- Target group with health check path and interval
- Security group allowing inbound 80/443

---

### rds-database.yml
Production-ready RDS instance:
- Configurable engine (MySQL/PostgreSQL)
- DB subnet group for VPC placement
- Security group restricted to app-tier only
- Automated backup retention
- Parameters: `DBInstanceClass`, `DBName`, `DBUsername`, `MultiAZ`

---

### full-stack-template.yml
Single template that provisions a complete application environment:
- VPC + subnets + IGW
- EC2 instance with Auto Scaling ready configuration
- ALB with target group
- RDS database
- All resources wired together with cross-references

Useful for spinning up a complete environment in one command — used for staging environment provisioning.

---

### lambda-function.yml + lambda-with-trigger.yml
Two Lambda templates:
- `lambda-function.yml` — basic Lambda with IAM execution role and configurable runtime/handler
- `lambda-with-trigger.yml` — Lambda wired to an event source (S3 bucket notification or scheduled CloudWatch Events rule)

Used in production to replace cron-based jobs and manual processes.

---

## ✅ Tested on

- AWS CLI v2
- Regions: `ap-south-1` (Mumbai — primary), `us-east-1`
- Real production use at BizmerlinHR (ClayHR) and E-Soft Communication

---

## 📌 Related repos

- [docker-compose-stacks](https://github.com/aniketchanna/docker-compose-stacks) — Docker Compose setups for Prometheus, ELK, Rails
- [cicd-pipeline-examples](https://github.com/aniketchanna/cicd-pipeline-examples) — Jenkins and GitHub Actions pipelines
- [linux-automation-scripts](https://github.com/aniketchanna/linux-automation-scripts) — Bash scripts for server automation

---

## 👤 Author

**Aniket Channa** — Senior DevOps Engineer  
8 years experience · AWS (70%) · Azure/GCP (30%) · Open to remote worldwide  
[LinkedIn](https://linkedin.com/in/aniketchanna) · [GitHub](https://github.com/aniketchanna) · IST (UTC+5:30)
