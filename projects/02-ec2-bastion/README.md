# Project 02 — EC2 + Bastion Host

**Goal:** Launch an EC2 instance in the private subnet and access it via a bastion host in the public subnet. Learn real-world network topology.

**Status:** ⬜ Not started

---

## What to Build

- [ ] Bastion host EC2 in public subnet (t2.micro, free tier)
- [ ] App EC2 in private subnet
- [ ] Security group for bastion — allow SSH (port 22) from your IP only
- [ ] Security group for app — allow SSH from bastion's security group only
- [ ] SSH hop: local → bastion → private EC2

## Architecture

```
Your machine
    │  SSH
    ▼
Bastion EC2 (public subnet)
    │  SSH
    ▼
App EC2 (private subnet)
```

## What I Learned

_Write here in your own words after completing._

## What Broke and Why

_Document any mistakes and how you fixed them._
