---
title: "EC2 Fleet"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Mục tiêu

Triển khai **fleet EC2 Spot** với **warm pool** để MatchMaker gán người chơi vào host đã chạy sẵn, tránh cold-start mỗi trận.

## Các bước

1. **Gắn tag** instance game server: `Role=FightingGameServer`.
2. **Bake AMI** từ instance đang chạy game (port 9000).
3. **Tạo launch template Spot** — AMI, instance type Graviton, security group cổng 9000, instance profile `FightingGameServerInstanceRole`.
4. **Tạo ASG** `FightingGameServerASG` với **warm pool** (instance ở trạng thái running).
5. **Kiểm tra** warm pool InService, port 9000 phản hồi, MatchMaker `DescribeInstances` thấy host.

## Kết quả mong đợi

AMI tái sử dụng, capacity ấm cho matchmaking latency thấp, tag thống nhất cho discovery.
