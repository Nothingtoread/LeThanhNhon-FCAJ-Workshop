---
title: "Cleanup"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Goal

Document the **teardown procedure** for the internship report. Screenshots were captured at the **delete confirmation** step; **Cancel** was clicked—no resources were actually deleted.

## Workflow for each resource

1. Navigate to the AWS console resource.
2. Choose **Delete** / **Terminate** / **Empty**.
3. Screenshot the confirmation dialog showing resource names.
4. Click **Cancel** (do not confirm deletion).

## Teardown order (recommended)

Delete dependencies before foundations:

| Order | Service | Resources |
|-------|---------|-----------|
| 1 | CodeDeploy | `FightingGameMatchmakerDeploy`, `FightingGameServerDeploy`, deployment groups |
| 2 | Auto Scaling | `FightingGameServerASG` (disable warm pool first if needed) |
| 3 | EC2 | Terminate remaining game server instances |
| 4 | EC2 | Delete launch template |
| 5 | API Gateway | `FightingGameMatchmakerAPI` |
| 6 | Lambda | `FightingGameMatchmaker`, `FightingGameMatchAnalytics` (remove triggers first) |
| 7 | DynamoDB | `MatchmakingQueue`, `ActiveMatches`, `MatchAnalytics` |
| 8 | S3 | Empty bucket objects → delete bucket |
| 9 | VPC | Delete interface/gateway endpoints → subnets → security groups → VPC |
| 10 | IAM | Delete roles created for deploy, Lambda, EC2 instance profile (after resources released) |

## Screenshot checklist

- [ ] CodeDeploy applications and deployment groups
- [ ] ASG and warm pool
- [ ] EC2 instances (terminate dialog)
- [ ] Launch template delete
- [ ] API Gateway API delete
- [ ] Lambda functions delete
- [ ] DynamoDB tables delete
- [ ] S3 empty bucket + delete bucket
- [ ] VPC delete
- [ ] IAM roles delete

## Report usage

Include screenshots in the internship appendix to demonstrate awareness of full stack lifecycle and cost hygiene. For the live demo account, resources may remain running until the internship ends—this section proves documented cleanup capability only.
