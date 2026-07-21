---
title: "Worklog Tuần 11"
date: 2026-07-15
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Hoàn thành nội dung workshop lab AWS.
* Deploy thành công website báo cáo thực tập.

**Thời gian:** 15/07/2026 – 21/07/2026

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| 2 | - Hoàn thành các phần workshop: S3 VPC endpoints, mô phỏng on-prem, cleanup | 15/07/2026 | 15/07/2026 | Template workshop FCAJ |
| 3 | - Ghi lại quy trình dọn tài nguyên kèm screenshot (hủy trước khi xóa) | 16/07/2026 | 16/07/2026 | |
| 4 | - Thiết lập site báo cáo Hugo từ template FCAJ; tùy chỉnh `config.toml` | 17/07/2026 | 17/07/2026 | |
| 5 | - Điền nội dung worklog, proposal và workshop vào Hugo | 18/07/2026 | 18/07/2026 | |
| 6 | - Cấu hình GitHub Actions (`hugo.yml`) deploy GitHub Pages <br> - Xác minh site build và publish lên nhánh `gh-pages` | 19/07/2026 | 19/07/2026 | |

### Kết quả đạt được tuần 11:

* Hoàn thành toàn bộ bài lab workshop gồm VPC Gateway endpoints, PrivateLink interface endpoints và mô phỏng DNS.
* Ghi lại screenshot teardown cho CodeDeploy, ASG, Lambda, DynamoDB, S3, VPC và IAM (chỉ màn hình xác nhận, không xóa thật).
* Fork và tùy chỉnh template báo cáo thực tập Hugo cho cá nhân.
* Trỏ repository về `Nothingtoread/LeThanhNhon-FCAJ-Workshop` với `baseURL` và author đúng.
* Deploy thành công website báo cáo qua GitHub Actions lên GitHub Pages.
* Site truy cập tại: `https://nothingtoread.github.io/LeThanhNhon-FCAJ-Workshop/`
