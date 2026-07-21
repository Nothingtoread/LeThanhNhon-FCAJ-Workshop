---
title: "IAM"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Mục tiêu

Cấu hình IAM cho MatchMaker Lambda, EC2, GitHub Actions và CodeDeploy.

## Bước 1 — MatchMaker Lambda role

Quyền DynamoDB, EC2 `DescribeInstances`, CloudWatch Logs, VPC (sau này).

## Bước 2 — FightingGameServerInstanceRole

![Role FightingGameServerInstanceRole](/images/5-Workshop/image15.png)

![Policies instance role](/images/5-Workshop/image16.png)

### Chỉnh sửa IAM role

![Modify IAM role](/images/5-Workshop/image17.png)

## Bước 3–5

GitHub deploy role, CodeDeploy service roles, `FightingGameMatchAnalyticsRole` — xem bản tiếng Anh cho chi tiết.
