---
title: "Bản đề xuất"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Kiến trúc Backend Serverless & Spot Instance cho Game Live-Service trên AWS

## Hạ tầng Cloud hiệu năng cao, mở rộng linh hoạt và tối ưu chi phí cho game multiplayer

---

### 1. Tóm tắt điều hành

Dự án trình bày kiến trúc backend cloud-native cho game multiplayer live-service trên Amazon Web Services (AWS). Thay vì duy trì fleet server chạy 24/7 bất kể nhu cầu người chơi, kiến trúc này cấp phát tài nguyên tính toán **chỉ khi thực sự cần**: xác thực, matchmaking và phiên chơi trực tiếp.

Các thành phần metagame—xác thực, phân phối asset, matchmaking và phân tích sau trận—vận hành hoàn toàn trên kiến trúc **Serverless**. Phiên game server chạy trên **EC2 Spot Fleet** trong VPC riêng biệt, được khởi tạo động bởi dịch vụ Matchmaker. Triển khai tuân thủ **GitOps** qua GitHub Actions và AWS CodeDeploy.

---

### 2. Tuyên bố vấn đề

#### Vấn đề là gì?

Kiến trúc game server truyền thống dùng fleet EC2 chạy liên tục 24/7, gây lãng phí chi phí khi ít người chơi. Deploy thủ công có rủi ro gián đoạn trận đấu, thời gian triển khai dài và rollback phức tạp. Mở port server ra internet cũng tăng rủi ro bảo mật và DDoS.

#### Giải pháp

Nguyên tắc thiết kế: **Serverless cho mọi thứ trừ phiên chơi trực tiếp**.

- Metagame (Auth, tải asset, Matchmaking, Analytics) dùng Cognito, API Gateway, Lambda, DynamoDB.
- Phiên chơi chạy trên EC2 Spot (Graviton ARM64) trong VPC public/private.
- Security Group động do Matchmaker Lambda quản lý, chỉ mở port khi có trận.
- CI/CD tự động qua GitHub Actions và CodeDeploy.

#### Lợi ích và ROI

- **Giảm đến 80% chi phí** nhờ Spot + Graviton, chỉ chạy compute khi có trận.
- **Không phí NAT/Egress** nhờ VPC Endpoints cho Lambda private subnet.
- **Deploy zero-downtime** với CodeDeploy Blue/Green và rollback tự động.
- **Bảo mật cao** với IAM credential tạm thời và Security Group động.

---

### 3. Kiến trúc giải pháp

![Live-Service Game Backend Architecture](/images/2-Proposal/architecture.png)

#### Các luồng kiến trúc

- **Flow C – GitOps CI/CD:** GitHub Actions build artifact → CodeDeploy cập nhật Lambda alias và EC2 ASG → sync client lên S3.
- **Flow A – Auth & Asset:** Cognito User Pool → Identity Pool → tải asset từ S3 bằng IAM credential tạm thời.
- **Flow R – Matchmaking:** API Gateway + WAF → Matchmaker Lambda (private subnet) → DynamoDB + EC2 warm pool → client kết nối WebSocket tới game server.
- **Flow E – Analytics:** DynamoDB Streams → Lambda xử lý bất đồng bộ → bảng analytics sau trận.

#### Dịch vụ AWS sử dụng

Cognito, WAF, CloudFront, API Gateway, Lambda, DynamoDB, EC2 Spot, CodeDeploy, S3, KMS, VPC Endpoints.

---

### 4. Triển khai kỹ thuật

1. **Tháng 1:** Thiết kế VPC, IAM, security group, KMS.
2. **Tháng 1–2:** Cognito, S3, API Gateway, DynamoDB schema.
3. **Tháng 2:** Matchmaker Lambda, ASG Spot, launch template Graviton.
4. **Tháng 3:** GitHub Actions, CodeDeploy, DynamoDB Streams, load test.

---

### 5. Timeline & Milestone

- **Tháng 1:** Thiết kế kiến trúc và network.
- **Tháng 2:** Matchmaking serverless và EC2 Spot automation.
- **Tháng 3:** GitOps pipeline, kiểm thử và triển khai.

---

### 6. Ước tính ngân sách

- EC2 chỉ chạy khi có trận; Lambda/DynamoDB on-demand chi phí thấp.
- Spot + Graviton giảm 70–90% so với On-Demand.
- VPC Endpoints loại bỏ phí NAT Gateway.
- Binary game pull từ S3 lúc boot, không cần rebake AMI thường xuyên.

---

### 7. Đánh giá rủi ro

| Rủi ro | Tác động | Xác suất | Giảm thiểu |
| --- | --- | --- | --- |
| Spot bị thu hồi | Trung bình | Thấp | Warm pool + multi-AZ Spot |
| Deploy thất bại | Cao | Thấp | CodeDeploy canary + rollback |
| Truy cập trái phép | Cao | Thấp | JWT + Security Group theo IP người chơi |

---

### 8. Kết quả mong đợi

- Mở rộng từ 10 đến 10.000+ người chơi đồng thời.
- Giảm hóa đơn cloud đến 80% so với server 24/7.
- Bảo mật enterprise, GitOps an toàn, analytics tự động sau trận.
