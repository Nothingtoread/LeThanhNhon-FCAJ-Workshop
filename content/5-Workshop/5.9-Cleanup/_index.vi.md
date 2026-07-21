---
title: "Cleanup"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Mục tiêu

Tài liệu hóa **quy trình teardown** cho báo cáo thực tập — chụp màn hình dialog xác nhận xóa rồi **Cancel** (không xóa thật).

## Thứ tự đề xuất

1. CodeDeploy (Lambda + EC2 apps/groups)
2. ASG `FightingGameServerASG`
3. EC2 instances
4. Launch template
5. API Gateway `FightingGameMatchmakerAPI`
6. Lambda `FightingGameMatchmaker`, `FightingGameMatchAnalytics`
7. DynamoDB `MatchmakingQueue`, `ActiveMatches`, `MatchAnalytics`
8. S3 empty + delete bucket
9. VPC endpoints → subnets → SG → VPC
10. IAM roles (sau khi tài nguyên đã gỡ)

## Checklist screenshot

CodeDeploy, ASG, EC2 terminate, launch template, API GW, Lambda, DynamoDB, S3, VPC, IAM — mỗi mục một ảnh dialog xác nhận.
