---
title: "Worklog Tuần 8"
date: 2026-06-23
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Handoff client kèm luồng login cho team (netcode + auth đã phác thảo).
* Bắt đầu triển khai CI/CD qua GitHub và GitHub Actions.

**Thời gian:** 23/06/2026 – 29/06/2026

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| 2 | - Hoàn thiện UI login client và xử lý session cho tích hợp team | 23/06/2026 | 23/06/2026 | |
| 3 | - Handoff codebase client kèm tài liệu interface auth + netcode | 24/06/2026 | 24/06/2026 | |
| 4 | - Thiết lập cấu trúc repository GitHub (`Nothingtoread/fighting-game`) | 25/06/2026 | 25/06/2026 | |
| 5 | - **CI/CD:** Tạo workflow GitHub Actions ban đầu cho build và deploy | 26/06/2026 | 26/06/2026 | Tài liệu GitHub Actions |
| 6 | - Cấu hình S3 static website hosting cho browser client <br> - Kiểm thử pipeline deploy tự động đầu tiên | 27/06/2026 | 27/06/2026 | |

### Kết quả đạt được tuần 8:

* Bàn giao gói client hoạt động với luồng login và stub netcode cho team.
* Tạo repository dự án và thiết lập quy ước nhánh.
* Triển khai workflow GitHub Actions đầu tiên (`deploy.yml`) cho build tự động.
* Tạo S3 assets bucket với static website hosting, bucket policy public-read và CORS.
* Xác minh CI sync bundle client (kèm `config.js` sinh từ secrets) lên S3 mỗi lần push.
