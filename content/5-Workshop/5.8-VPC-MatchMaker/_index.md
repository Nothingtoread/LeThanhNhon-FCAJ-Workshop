---
title: "VPC MatchMaker"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Goal

Move **MatchMaker Lambda** into **private subnets** and reach DynamoDB + EC2 APIs via **VPC endpoints**—eliminating **NAT Gateway** cost for control-plane traffic.

## Architecture summary

| Component | Placement |
|-----------|-----------|
| Game server ASG | Public subnet (clients connect via IGW on port 9000) |
| MatchMaker Lambda | Private subnets (no public IP) |
| DynamoDB | Gateway VPC endpoint |
| EC2 API, CloudWatch Logs | Interface VPC endpoints |

## Step 1 — Document subnet layout

Record CIDRs for:

- Public subnets (game servers)
- Private subnets (Lambda)
- Route tables per tier

## Step 2 — Create private subnets & route table

1. Create private subnets in two AZs (Lambda HA).
2. Private route table: **local VPC routes only**—no `0.0.0.0/0` to NAT.
3. Associate private subnets with this route table.

## Step 3 — Security groups

1. **Lambda SG:** outbound to VPC endpoints and (if required) internal services only.
2. **Endpoint SG:** allow inbound HTTPS (443) from Lambda SG.
3. Game server SG unchanged for player traffic.

## Step 4 — Create VPC endpoints

| Endpoint | Type | Service |
|----------|------|---------|
| DynamoDB | **Gateway** | `com.amazonaws.ap-southeast-1.dynamodb` — attach to private route table |
| EC2 | **Interface** | `com.amazonaws.ap-southeast-1.ec2` |
| CloudWatch Logs | **Interface** | `com.amazonaws.ap-southeast-1.logs` |

Enable **private DNS** on interface endpoints so Lambda SDK resolves regional hostnames inside the VPC.

## Step 5 — Update Lambda VPC config

1. **MatchMaker Lambda → Configuration → VPC**.
2. Select VPC, **private subnets**, Lambda security group.
3. Attach **`AWSLambdaVPCAccessExecutionRole`** to Lambda execution role if not already present.

## Step 6 — Publish new version & update alias

1. Publish new Lambda version after VPC change (cold start / ENI setup).
2. Point **`live` alias** to new version.
3. Run matchmaking smoke test from client.

## Step 7 — Verify (no NAT)

1. Confirm **no NAT Gateway** required for MatchMaker → DynamoDB / `DescribeInstances`.
2. CloudWatch Logs still receive Lambda output via logs endpoint.
3. Match assignment and security group updates still succeed.

## Expected outcome

- MatchMaker control traffic stays on AWS private network
- Zero NAT data-processing charges for Lambda metadata calls
- Game servers remain publicly reachable for WebSocket gameplay

## Troubleshooting

| Issue | Check |
|-------|--------|
| Lambda timeout in VPC | Subnets must route to endpoints; SG rules on endpoints |
| `DescribeInstances` fails | EC2 interface endpoint + IAM permissions |
| No logs | Logs interface endpoint + DNS enabled |
