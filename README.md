# Cloud & DevOps Journey

Documenting my structured path from backend engineer to cloud-confident developer.

**Background:** ~1.8 YOE. Microservices, Rust, Kafka, MongoDB, React, Redis, etcd. New to provisioning cloud infrastructure from scratch.

---

## Goals

- [ ] AWS Solutions Architect Associate (SAA-C03)
- [ ] AWS Developer Associate (DVA-C02) or SysOps Associate (SOA-C02)
- [ ] Certified Kubernetes Administrator (CKA)
- [ ] Deploy a full production-grade stack on AWS with Terraform and CI/CD

---

## Learning Phases

### Phase 1 — Cloud Fundamentals (2–4 weeks)
Get hands-on with AWS console. EC2, VPC, S3, IAM, RDS, security groups.
> Status: 🔄 In progress

### Phase 2 — Deploy Own Services (4–6 weeks)
Dockerize a Rust service → ECR → ECS Fargate → ALB → ElastiCache / RDS.

### Phase 3 — Infrastructure as Code (3–4 weeks)
Terraform. Rebuild everything from Phase 2 as code. No more clicking.

### Phase 4 — CI/CD & DevOps (3–4 weeks)
GitHub Actions → ECR → ECS/EKS. Secrets Manager, CloudWatch, alerting.

---

## Projects

| # | Project | Status |
|---|---------|--------|
| 01 | [Manual VPC](projects/01-manual-vpc/) | 🔄 |
| 02 | [EC2 + Bastion Host](projects/02-ec2-bastion/) | ⬜ |
| 03 | [Rust Service on ECS](projects/03-rust-service-ecs/) | ⬜ |
| 04 | [Full Stack Infra](projects/04-full-stack-infra/) | ⬜ |

---

## Certifications

| Cert | Target Date | Status |
|------|-------------|--------|
| AWS SAA-C03 | TBD | ⬜ |
| AWS DVA-C02 | TBD | ⬜ |
| CKA | TBD | ⬜ |

---

## Key Principles

1. **Never leave infra as console-only.** If I clicked it, I eventually Terraform it.
2. **Write notes in my own words.** If I can't explain it in 3 sentences, I don't know it.
3. **Document mistakes.** What broke and why is more valuable than what worked.
4. **Commit as I go.** Small, meaningful commits beat big batch dumps.
