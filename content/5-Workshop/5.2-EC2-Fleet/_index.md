---
title: "EC2 Fleet"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Goal

Provision a **Spot EC2 fleet** with a **warm pool** so MatchMaker can assign players to already-running game hosts instead of cold-starting every match.

## Step 1 — Tag the running game server

1. Open **EC2 → Instances** in `ap-southeast-1`.
2. Select the instance running the game server (port **9000**).
3. **Actions → Manage tags → Add tag:**
   - Key: `Role`
   - Value: `FightingGameServer`
4. Save. MatchMaker discovers hosts via `ec2:DescribeInstances` filtered on this tag.

![Tag the current game server](/images/5-Workshop/image2.png)

## Step 2 — Bake an AMI

1. With the game server instance **stopped or running** (prefer stopped for consistency), select it.
2. **Actions → Image and templates → Create image**.
3. Name: e.g. `FightingGameServer-v1`.
4. Wait until AMI status is **available** in **AMIs**.

![Bake AMI from that instance](/images/5-Workshop/image3.png)

## Step 3 — Create Spot launch template

1. **EC2 → Launch Templates → Create launch template**.
2. **AMI:** select the baked AMI from Step 2.
3. **Instance type:** ARM Graviton class used by the project (as in proposal).
4. **Key pair / security group:** allow inbound **9000** from MatchMaker-managed rules; SSH for admin if needed.
5. **IAM instance profile:** `FightingGameServerInstanceRole` (configured in [5.4 IAM](5.4-IAM/)).
6. **Purchase option:** Request **Spot** instances.
7. **User data:** script to pull server bundle from S3 on boot (if not already in AMI).
8. Create template.

![Create launch template (Spot)](/images/5-Workshop/image4.png)

## Step 4 — Create Auto Scaling Group with warm pool

1. **EC2 → Auto Scaling Groups → Create ASG**.
2. Name: `FightingGameServerASG`.
3. Launch template: Spot template from Step 3.
4. **VPC / subnet:** public subnet where game clients reach instances via Internet Gateway.
5. **Capacity:** set min/desired per project needs; enable **warm pool** so instances stay **running** and ready.
6. **Health checks:** EC2 status + optional custom (port 9000).
7. Create ASG and verify instances launch with tag `Role=FightingGameServer`.

![Create ASG warm pool](/images/5-Workshop/image5.png)

## Step 5 — Verify fleet health

1. Confirm warm pool instances are **InService**.
2. From a test client or `telnet`/`nc`, verify **port 9000** responds on an instance private/public IP as designed.
3. Confirm MatchMaker (once deployed) can list instances via `DescribeInstances`.

## Expected outcome

- Repeatable AMI-based Spot launches
- ASG maintains warm capacity for low-latency match assignment
- All game hosts uniformly tagged for discovery

## Troubleshooting

| Issue | Check |
|-------|--------|
| ASG instances terminate immediately | Spot capacity, launch template IAM profile, subnet routing |
| Port 9000 unreachable | Security group, game process not started, wrong subnet |
| MatchMaker finds no hosts | Tag `Role=FightingGameServer` missing or wrong region |
