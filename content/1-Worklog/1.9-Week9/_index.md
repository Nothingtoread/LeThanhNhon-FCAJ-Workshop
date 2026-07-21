---
title: "Week 9 Worklog"
date: 2026-06-30
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Implement IAM permission boundaries and secure deploy roles.
* Validate GitHub push triggers and CodeDeploy deployment capability.

**Period:** 30/06/2026 – 06/07/2026

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| 2 | - Study IAM Permission Boundaries and least-privilege deploy patterns | 30/06/2026 | 30/06/2026 | AWS IAM docs |
| 3 | - Register GitHub OIDC identity provider in IAM (no long-lived access keys) | 01/07/2026 | 01/07/2026 | |
| 4 | - Create deploy role with trust policy scoped to the GitHub repo; attach permissions | 02/07/2026 | 02/07/2026 | |
| 5 | - Configure repository secrets (`AWS_ROLE_ARN`, `COGNITO_*`, `ASSETS_BUCKET`, etc.) | 03/07/2026 | 03/07/2026 | |
| 6 | - **Test:** Push to GitHub → verify S3 sync, Lambda update, and CodeDeploy job success | 04/07/2026 | 04/07/2026 | |

### Week 9 Achievements:

* Eliminated static AWS access keys from CI by implementing GitHub OIDC → IAM role authentication.
* Applied IAM permission boundaries to constrain deploy role capabilities.
* Configured `FightingGameServerInstanceRole` and MatchMaker Lambda permissions (DynamoDB, EC2 `DescribeInstances`).
* Verified end-to-end deploy: GitHub push triggers Actions → S3 client sync + CodeDeploy for Lambda and EC2 fleet.
* Tagged game server instances (`Role=FightingGameServer`), baked AMI, and created Spot launch template with ASG warm pool.
* Documented successful CodeDeploy jobs and deployment history for the internship report.
