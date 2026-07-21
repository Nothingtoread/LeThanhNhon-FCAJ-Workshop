---
title: "Worklog Tuần 10"
date: 2026-07-07
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Hoàn thành dự án capstone (xử lý bất đồng bộ, củng cố VPC).
* Bắt đầu viết báo cáo thực tập và handoff tài liệu workshop.

**Thời gian:** 07/07/2026 – 14/07/2026

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| 2 | - Triển khai xử lý sau trận bất đồng bộ: DynamoDB Streams → MatchAnalytics Lambda | 07/07/2026 | 07/07/2026 | |
| 3 | - Cài CodeDeploy agent trên EC2 fleet (Ubuntu 24.04 / patch Ruby 3.3) | 08/07/2026 | 08/07/2026 | |
| 4 | - Chuyển MatchMaker Lambda sang private subnet với VPC endpoints (không NAT) | 09/07/2026 | 09/07/2026 | |
| 5 | - Kiểm thử tích hợp cuối: matchmaking → gameplay → kết thúc trận → analytics | 10/07/2026 | 10/07/2026 | |
| 6 | - Hoàn thành deliverable capstone; lập dàn ý báo cáo thực tập <br> - Handoff tài liệu lab workshop cho team | 11/07/2026 | 11/07/2026 | |

### Kết quả đạt được tuần 10:

* Triển khai pipeline **Flow E**: DynamoDB Stream `ActiveMatches` → Lambda `FightingGameMatchAnalytics` → bảng `MatchAnalytics`.
* Cài và cấu hình CodeDeploy agent trên game server; tạo deployment group `FightingGameServer-fleet`.
* Publish phiên bản Lambda và alias `live` cho canary rollout qua CodeDeploy.
* Cấu hình lại MatchMaker trong private subnet với DynamoDB gateway và EC2/CloudWatch interface endpoints.
* Xác minh vòng đời game đầy đủ: login → hàng đợi → trận → WebSocket gameplay → ghi nhận trận kết thúc trong DynamoDB.
* Viết hướng dẫn `PROJECT.md` end-to-end và bắt đầu cấu trúc báo cáo Hugo.
* Chuẩn bị tài liệu handoff workshop lab VPC endpoints.
