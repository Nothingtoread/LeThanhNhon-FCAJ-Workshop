---
title: "Blog 2"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# TRIỂN KHAI ORACLE DATABASE@AWS BẰNG TERRAFORM

Bài viết giới thiệu **Oracle Database@AWS** — dịch vụ co-location đưa OCI database vào datacenter AWS, cho phép chạy Exadata với độ trễ dưới millisecond tới EC2.

### Khái niệm kiến trúc:

- **Customer VPC:** Ứng dụng chạy trên EC2.
- **ODB Network VPC:** Subnet client/backup, kết nối Customer VPC qua ODB Peering.
- **OCI Child Site:** Exadata Infrastructure trong datacenter AWS.
- **Control Plane:** OCI Automation quản lý vòng đời tài nguyên.

### Infrastructure as Code với Terraform:

1. Tạo VPC, Subnet, Route Table trên AWS.
2. Provision Exadata qua OCI provider.
3. Cấu hình peering giữa AWS và OCI tự động.

![Oracle Database@AWS Architecture](/images/3-BlogsPosted/blog2.png)

### Liên kết tham khảo:

- [Bài đăng Facebook](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2198792150885745/)
- [Bài viết AWS](https://aws.amazon.com/vi/blogs/database/provision-oracle-databaseaws-resources-using-terraform/)
