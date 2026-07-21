---
title: "Blog 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# XÂY DỰNG INNOVATION SANDBOX TRÊN AWS VỚI DASHBOARD PHÂN TÍCH REAL-TIME

Bài viết mô tả cách xây dựng môi trường **Innovation Sandbox** an toàn, có thể mở rộng trên AWS kết hợp dashboard real-time với **Amazon Q Business** — phục vụ hackathon, bootcamp và R&D.

### Tính năng kiến trúc:

1. **Dashboard & Amazon Q Business:** CloudFront + S3 host dashboard; API Gateway + Lambda gọi Q Business trả URL trải nghiệm AI.
2. **Account Provisioning:** Control Tower + Organizations tự động tạo account trong OU `InnovationSandbox`.
3. **Deploy tự động:** AWS CDK, Git pipeline, Python script sync S3 và invalidate CloudFront.

### Lợi ích:

- Quản trị tập trung qua Control Tower guardrails.
- Trợ lý AI real-time cho người tham gia.
- Tự động hóa provisioning, giảm tải vận hành.

![Innovation Sandbox Architecture](/images/3-BlogsPosted/blog3.png)

### Liên kết tham khảo:

- [Bài đăng Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2192030984895195/)
- [Bài viết AWS](https://aws.amazon.com/vi/blogs/mt/innovation-sandbox-on-aws-with-real-time-analytics-dashboard/)
