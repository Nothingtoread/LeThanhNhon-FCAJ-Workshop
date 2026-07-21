---
title: "GitHub OIDC"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Mục tiêu

Xác thực GitHub Actions qua OIDC — không dùng access key tĩnh.

![GitHub OIDC → AWS](/images/5-Workshop/image9.png)

## Bước 1 — OIDC provider

![Thêm GitHub OIDC provider](/images/5-Workshop/image10.png)

## Bước 2 — IAM role

![Gắn permissions policy](/images/5-Workshop/image11.png)

![Trust policy](/images/5-Workshop/image12.png)

## Bước 3 — Repository secrets

![Secrets repository](/images/5-Workshop/image13.png)

![Secrets repository (tiếp)](/images/5-Workshop/image14.png)

## Bước 5 — Xác minh deploy

1. Push commit để chạy workflow.
2. Xác nhận bước **Configure AWS credentials (OIDC)** thành công.
3. Xác nhận pipeline hoàn tất — deploy MatchMaker Lambda, sync client S3, deploy game-server qua SSM (**CI/CD đầu tiên trước khi thêm CodeDeploy** ở [5.6](5.6-CodeDeploy/)).

![Pipeline CI/CD đầu tiên thành công qua OIDC (trước CodeDeploy)](/images/5-Workshop/image18.png)

![Alias `live` MatchMaker sau deploy](/images/5-Workshop/image19.png)
