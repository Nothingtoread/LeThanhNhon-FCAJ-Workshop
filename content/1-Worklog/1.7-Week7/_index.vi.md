---
title: "Worklog Tuần 7"
date: 2026-06-16
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Hoàn thiện mô hình game trên LeopardJS và chạy local.
* Bắt đầu triển khai Authentication tích hợp với netcode.

**Thời gian:** 16/06/2026 – 22/06/2026

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| 2 | - Chuyển logic game từ Scratch sang cấu trúc project LeopardJS | 16/06/2026 | 16/06/2026 | Tài liệu LeopardJS |
| 3 | - Triển khai sprite nhân vật, animation và xử lý input trong LeopardJS | 17/06/2026 | 17/06/2026 | |
| 4 | - Chạy và kiểm thử game local; sửa lỗi render và va chạm | 18/06/2026 | 18/06/2026 | |
| 5 | - Học kiến trúc netcode: WebSocket, player slot, đồng bộ trạng thái | 19/06/2026 | 19/06/2026 | |
| 6 | - **Phác thảo:** Thiết kế luồng auth (login → session → tham gia trận) <br> - Tích hợp hook auth ban đầu với module netcode | 20/06/2026 | 20/06/2026 | |

### Kết quả đạt được tuần 7:

* Chuyển thành công prototype Scratch sang LeopardJS và chạy trên máy phát triển.
* Triển khai gameplay cốt lõi: hai nhân vật, combo tấn công, thanh máu và kết quả ván đấu.
* Thiết kế phác thảo tích hợp authentication + netcode để handoff cho team.
* Hiểu mô hình multiplayer real-time qua WebSocket cho game đối kháng.
* Chuẩn bị codebase client cho cộng tác team và thiết lập CI/CD ở tuần sau.
