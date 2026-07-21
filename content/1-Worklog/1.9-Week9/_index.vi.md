---
title: "Worklog Tuần 9"
date: 2026-06-30
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Triển khai IAM Permission Boundaries và role deploy an toàn.
* Kiểm tra push lên GitHub và khả năng deploy của CodeDeploy.

**Thời gian:** 30/06/2026 – 06/07/2026

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| 2 | - Học IAM Permission Boundaries và mô hình deploy least-privilege | 30/06/2026 | 30/06/2026 | Tài liệu AWS IAM |
| 3 | - Đăng ký GitHub OIDC identity provider trong IAM (không dùng access key cố định) | 01/07/2026 | 01/07/2026 | |
| 4 | - Tạo deploy role với trust policy giới hạn theo repo GitHub; gắn permissions | 02/07/2026 | 02/07/2026 | |
| 5 | - Cấu hình repository secrets (`AWS_ROLE_ARN`, `COGNITO_*`, `ASSETS_BUCKET`, v.v.) | 03/07/2026 | 03/07/2026 | |
| 6 | - **Kiểm thử:** Push lên GitHub → xác minh S3 sync, Lambda update và CodeDeploy thành công | 04/07/2026 | 04/07/2026 | |

### Kết quả đạt được tuần 9:

* Loại bỏ AWS access key tĩnh khỏi CI bằng GitHub OIDC → IAM role.
* Áp dụng IAM Permission Boundaries để giới hạn quyền deploy role.
* Cấu hình `FightingGameServerInstanceRole` và quyền MatchMaker Lambda (DynamoDB, EC2 `DescribeInstances`).
* Xác minh deploy end-to-end: push GitHub → Actions → S3 client sync + CodeDeploy cho Lambda và EC2 fleet.
* Gắn tag instance game server (`Role=FightingGameServer`), bake AMI, tạo Spot launch template và ASG warm pool.
* Ghi nhận CodeDeploy job thành công và lịch sử deployment cho báo cáo thực tập.
