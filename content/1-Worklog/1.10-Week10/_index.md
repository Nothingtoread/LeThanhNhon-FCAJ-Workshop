---
title: "Week 10 Worklog"
date: 2026-07-07
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Complete the capstone project (async processing, VPC hardening).
* Begin writing the internship report and hand off workshop documentation.

**Period:** 07/07/2026 – 14/07/2026

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| 2 | - Implement async post-match processing: DynamoDB Streams → MatchAnalytics Lambda | 07/07/2026 | 07/07/2026 | |
| 3 | - Install CodeDeploy agent on EC2 fleet (Ubuntu 24.04 / Ruby 3.3 patch) | 08/07/2026 | 08/07/2026 | |
| 4 | - Move MatchMaker Lambda to private subnets with VPC endpoints (no NAT) | 09/07/2026 | 09/07/2026 | |
| 5 | - Final integration testing: matchmaking → gameplay → match finish → analytics | 10/07/2026 | 10/07/2026 | |
| 6 | - Complete capstone deliverables; begin internship report outline <br> - Hand off workshop lab documentation to team | 11/07/2026 | 11/07/2026 | |

### Week 10 Achievements:

* Deployed the **Flow E** async pipeline: `ActiveMatches` DynamoDB Stream → `FightingGameMatchAnalytics` Lambda → `MatchAnalytics` table.
* Installed and configured CodeDeploy agent on game server instances; created EC2 deployment group `FightingGameServer-fleet`.
* Published Lambda versions with `live` alias for canary rollouts via CodeDeploy.
* Reconfigured MatchMaker into private subnets with DynamoDB gateway and EC2/CloudWatch interface endpoints.
* Verified full game lifecycle: login → queue → match → WebSocket gameplay → finished match recorded in DynamoDB.
* Wrote `PROJECT.md` end-to-end guide and began structuring the Hugo internship report.
* Prepared workshop handoff materials for the AWS VPC endpoints lab.
