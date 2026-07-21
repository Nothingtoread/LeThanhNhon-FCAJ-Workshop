---
title: "EC2 Fleet"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Mục tiêu

Triển khai **fleet EC2 Spot** với **warm pool** để MatchMaker gán người chơi vào host đã chạy sẵn.

## Bước 1 — Gắn tag game server

1. **EC2 → Instances** tại `ap-southeast-1`.
2. Chọn instance game server (cổng **9000**).
3. **Actions → Manage tags:** `Role=FightingGameServer`.

![Gắn tag game server](/images/5-Workshop/image2.png)

## Bước 2 — Bake AMI

1. **Actions → Image and templates → Create image**.
2. Đợi AMI **available**.

![Bake AMI](/images/5-Workshop/image3.png)

## Bước 3 — Launch template Spot

1. Tạo launch template với AMI đã bake, Spot, instance profile `FightingGameServerInstanceRole`.

![Launch template Spot](/images/5-Workshop/image4.png)

## Bước 4 — ASG warm pool

1. Tạo ASG `FightingGameServerASG` với warm pool.

![ASG warm pool](/images/5-Workshop/image5.png)

## Bước 5 — Kiểm tra fleet

1. Xác nhận instance warm pool ở trạng thái **InService**.
2. Kiểm tra cổng **9000** phản hồi từ client test hoặc `telnet`/`nc`.
3. Xác nhận MatchMaker (sau khi deploy) liệt kê được instance qua `DescribeInstances`.
