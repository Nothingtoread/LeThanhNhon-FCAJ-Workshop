---
title: "IAM"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Mục tiêu

Cấu hình IAM cho MatchMaker Lambda, EC2 game server, GitHub Actions và CodeDeploy.

## Các bước

1. **MatchMaker Lambda role** — DynamoDB (`MatchmakingQueue`, `ActiveMatches`), EC2 `DescribeInstances`, (tùy chọn) security group động, VPC access sau này.
2. **`FightingGameServerInstanceRole`** — S3 đọc assets, DynamoDB ghi `ActiveMatches` khi match kết thúc, gắn instance profile vào launch template.
3. **`GitHubActionsFightingGameDeploy`** — trust OIDC GitHub repo `Nothingtoread/fighting-game`; quyền S3, Lambda, CodeDeploy.
4. **CodeDeploy service roles** — riêng cho Lambda vs EC2 (`CodeDeployServiceRoleForEC2` + `AWSCodeDeployRole`).
5. **`FightingGameMatchAnalyticsRole`** — đọc DynamoDB stream `ActiveMatches`, ghi `MatchAnalytics`.
