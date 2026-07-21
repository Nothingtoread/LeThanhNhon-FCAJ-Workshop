---
title: "GitHub OIDC"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Mục tiêu

Xác thực GitHub Actions qua **OIDC** — không dùng access key tĩnh.

## Các bước

1. IAM **OIDC provider**: `https://token.actions.githubusercontent.com`, audience `sts.amazonaws.com`.
2. Tạo role `GitHubActionsFightingGameDeploy` — trust policy giới hạn repo `Nothingtoread/fighting-game`.
3. Gắn policy deploy (S3, Lambda, CodeDeploy) — xem [5.4](5.4-IAM/).
4. Thêm secrets GitHub: `AWS_ROLE_ARN`, `AWS_REGION`, `ASSETS_BUCKET`, `COGNITO_*`, `MATCHMAKER_API_BASE`, `WS_SERVER`.
5. Workflow dùng `aws-actions/configure-aws-credentials@v4` với `role-to-assume`.
6. Push commit, xác minh workflow thành công.
