---
title: "Blog 1"
date: 2026-05-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# ALS GEOANALYTICS' LITHOLENS VÀ MACHINE LEARNING VỚI AMAZON EKS

ALS Geoanalytics phát triển **LithoLens** — nền tảng cloud-native dùng computer vision và ML để tự động hóa quy trình core logging địa chất, tăng tốc đánh giá tài nguyên khoáng sản.

### Thành phần kiến trúc chính:

- **Client & API Layer:** API Gateway, Lambda, Cognito.
- **Compute Layer:** Amazon EKS điều phối container ML inference, scale theo lượng ảnh xử lý.
- **Storage & Database:** S3 lưu ảnh core, RDS metadata, CloudWatch giám sát.

### Lợi ích:

- **Khả năng mở rộng** với auto-scaling trên EKS.
- **Tiết kiệm chi phí** nhờ serverless API + container scale theo nhu cầu.
- **Hiệu năng cao** với GPU instance cho deep learning inference.

![LithoLens Architecture](/images/3-BlogsPosted/blog1.png)

### Liên kết tham khảo:

- [Bài đăng Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2199204024177891/)
- [Bài viết AWS](https://aws.amazon.com/vi/blogs/architecture/how-als-geoanalytics-litholens-revolutionizes-core-logging-through-machine-learning-with-amazon-eks/)
