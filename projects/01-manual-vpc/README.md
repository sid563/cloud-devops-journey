# Project 01 — Manual VPC

**Goal:** Create a VPC from scratch in the AWS console. Understand how networking pieces connect before automating any of it.

**Status:** 🔄 In progress

---

## What to Build

- [ ] VPC with CIDR block (e.g. `10.0.0.0/16`)
- [ ] 1 public subnet (e.g. `10.0.1.0/24`)
- [ ] 1 private subnet (e.g. `10.0.2.0/24`)
- [ ] Internet Gateway — attach to VPC
- [ ] Route table for public subnet — route `0.0.0.0/0` → IGW
- [ ] Route table for private subnet — no IGW route

## Architecture

```
Internet
    │
    ▼
Internet Gateway
    │
    ▼
Public Subnet (10.0.1.0/24)
    │
    ▼
Private Subnet (10.0.2.0/24)
```

## What I Learned

_Write here in your own words after completing._

## What Broke and Why

_Document any mistakes and how you fixed them._
