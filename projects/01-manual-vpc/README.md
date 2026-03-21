# Project 01 — Manual VPC

**Goal:** Create a VPC from scratch in the AWS console. Understand how networking pieces connect before automating any of it.

**Status:** ✅ Complete

---

## What Was Built

- VPC with CIDR `10.0.0.0/16` (65,536 IPs)
- Public subnet `10.0.1.0/24` in `us-east-1a`
- Private subnet `10.0.2.0/24` in `us-east-1a`
- Internet Gateway attached to the VPC
- Route table for public subnet — `0.0.0.0/0` → IGW
- Route table for private subnet — local VPC traffic only
- S3 VPC Endpoint (private S3 access without going through internet)

## Architecture

```
Internet
    │
    ▼
Internet Gateway (igw)
    │
    ▼
Public Subnet (10.0.1.0/24)   ← ALB, bastion hosts live here
    │
    ▼
Private Subnet (10.0.2.0/24)  ← app servers, databases live here
```

---

## What I Learned

**VPC** is your private isolated network on AWS. Everything you deploy lives inside it.

**CIDR block** defines the IP address space. `10.0.0.0/16` means you own all IPs from `10.0.0.0` to `10.0.255.255`.

**Subnets** carve that space into smaller chunks. `/24` gives 256 IPs per subnet.

**Internet Gateway (IGW)** is the door between your VPC and the internet. Without it, nothing in the VPC can reach the internet.

**Route table** is a routing rulebook attached to a subnet. What makes a subnet "public" or "private":
- Public subnet = route table has `0.0.0.0/0 → IGW`
- Private subnet = route table has no IGW route, only local VPC traffic

**Security group** = door lock (controls who can connect to an instance).
**Route table** = road map (controls where traffic can actually go).
These are two different things — opening a port in a security group means nothing if the route table has no path to the destination.

---

## Project 02 — EC2 Bastion + Private Instance

**Status:** ✅ Complete

### What Was Built

- Key pair `sid-personal-key` (ED25519, stored at `~/.ssh/`)
- Bastion EC2 (`t2.micro`, Amazon Linux 2023) in public subnet `10.0.1.25`
  - Security group `sid-bastion-sg`: inbound SSH port 22 from My IP only
  - Auto-assign public IP enabled
- Private EC2 (`t2.micro`, Amazon Linux 2023) in private subnet `10.0.2.138`
  - Security group `sid-private-app-sg`: inbound SSH port 22 from `sid-bastion-sg` only
  - No public IP

### SSH Flow

```
Local machine
    │  ssh -A -i ~/.ssh/sid-personal-key.pem ec2-user@44.195.90.57
    ▼
Bastion (ip-10-0-1-25, public subnet)
    │  ssh ec2-user@10.0.2.138
    ▼
Private EC2 (ip-10-0-2-138, private subnet) — no public IP, unreachable from internet
```

Commands used:
```bash
# Add key to agent (enables forwarding)
ssh-add ~/.ssh/sid-personal-key.pem

# SSH into bastion with agent forwarding (-A)
ssh -A -i ~/.ssh/sid-personal-key.pem ec2-user@44.195.90.57

# From inside bastion, hop to private EC2
ssh ec2-user@10.0.2.138
```

### Key Observations

**Private EC2 cannot reach the internet.** Running `curl https://google.com` from the private EC2 hangs indefinitely. The route table has no path to the IGW, so packets have nowhere to go.

**Bastion CAN reach the internet.** Same `curl` from the bastion works fine — it has a public IP and its route table points to the IGW.

**The fix for private outbound access is NAT Gateway** — it sits in the public subnet and lets private instances make outbound requests without exposing them to inbound connections. NAT Gateway costs ~$0.045/hour so it was skipped for this exercise.

### What Broke and Why

- Initially created `sid-bastion-sg` with no inbound rules — deleted and recreated with correct SSH rule.
- Key learning: always check security group has the right inbound rule AND the subnet has the right route table entry. Both must be correct independently.

---

## Cleanup

Both EC2 instances terminated after the exercise to avoid free tier usage.
VPC, subnets, IGW, and route tables left in place (no cost).

> **Rule:** Terminate EC2 instances when not actively using. t2.micro is free tier but capped at 750 hours/month total.
