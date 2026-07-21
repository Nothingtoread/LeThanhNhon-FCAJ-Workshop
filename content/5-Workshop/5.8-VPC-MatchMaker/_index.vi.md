---
title: "VPC MatchMaker"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Mục tiêu

Đưa **MatchMaker Lambda** vào **private subnet**, gọi DynamoDB/EC2 qua **VPC endpoints** — không cần NAT Gateway.

## Các bước

1. Ghi nhận layout subnet: public (game server), private (Lambda).
2. Tạo private subnet + route table (chỉ local, không 0.0.0.0/0 NAT).
3. Security group Lambda và endpoint (443 từ Lambda SG).
4. **Endpoints:** DynamoDB (gateway), EC2 + CloudWatch Logs (interface, bật private DNS).
5. Cấu hình VPC cho MatchMaker Lambda; role `AWSLambdaVPCAccessExecutionRole`.
6. Publish version mới, cập nhật alias `live`.
7. Smoke test matchmaking; xác minh không cần NAT cho traffic điều khiển.

## Kết quả

Traffic điều khiển Lambda ở mạng private AWS; game server vẫn public cho client cổng 9000.
