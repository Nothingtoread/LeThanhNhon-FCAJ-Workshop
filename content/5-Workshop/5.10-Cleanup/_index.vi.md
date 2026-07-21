---
title: "Cleanup"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

Sau khi triển khai và demo capstone, em ghi lại cách tháo dỡ toàn bộ stack fighting-game theo đúng thứ tự phụ thuộc. Với từng tài nguyên AWS, em mở trang console tương ứng và chọn xóa hoặc terminate.

Các ảnh dưới đây theo thứ tự em thực hiện: lớp ứng dụng và compute trước, tiếp theo API và serverless, lưu trữ, mạng, và cuối cùng là IAM roles.

![Dọn dẹp tài nguyên](/images/5-Workshop/image39.png)

### CodeDeploy

![Xóa CodeDeploy](/images/5-Workshop/image40.png)

### Auto Scaling Group

![Xóa ASG](/images/5-Workshop/image41.png)

### EC2 instances

![Xóa EC2](/images/5-Workshop/image42.png)

### Launch template

![Xóa launch template](/images/5-Workshop/image43.png)

### API Gateway

![Xóa API Gateway](/images/5-Workshop/image44.png)

### Lambda functions

![Xóa Lambda](/images/5-Workshop/image45.png)

### DynamoDB tables

![Xóa DynamoDB](/images/5-Workshop/image46.png)

### S3 bucket

![Empty S3 bucket](/images/5-Workshop/image47.png)

![Xóa S3 bucket](/images/5-Workshop/image48.png)

### VPC

![Xóa VPC](/images/5-Workshop/image49.png)

### IAM roles

![Xóa IAM roles](/images/5-Workshop/delete-iam-roles.png)
