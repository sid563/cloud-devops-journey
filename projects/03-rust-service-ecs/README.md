# Project 03 — Rust Service on ECS Fargate

**Goal:** Containerize a Rust service, push to ECR, deploy on ECS Fargate behind an ALB. Add a data store.

**Status:** ⬜ Not started

---

## What to Build

- [ ] Dockerfile for Rust service (multi-stage build)
- [ ] ECR repository
- [ ] Push image to ECR
- [ ] ECS cluster + task definition
- [ ] ECS Fargate service
- [ ] ALB in public subnet, targets in private subnet
- [ ] ElastiCache (Redis) or RDS in private subnet
- [ ] Security groups wiring it all together

## Architecture

```
Internet
    │
    ▼
ALB (public subnet)
    │
    ▼
ECS Fargate Tasks (private subnet)
    │
    ▼
ElastiCache / RDS (private subnet)
```

## Files

_Add Dockerfile, task definition JSON, etc. here as you build._

## What I Learned

_Write here in your own words after completing._

## What Broke and Why

_Document any mistakes and how you fixed them._
