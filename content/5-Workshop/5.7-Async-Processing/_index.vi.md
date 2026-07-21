---
title: "Async Processing"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Mục tiêu

**Flow E** — copy dữ liệu trận đã kết thúc từ `ActiveMatches` sang `MatchAnalytics` qua **DynamoDB Streams** + Lambda.

## Các bước

1. Bật stream `ActiveMatches` — view **NEW_AND_OLD_IMAGES**.
2. Tạo bảng `MatchAnalytics`.
3. Role `FightingGameMatchAnalyticsRole` — đọc stream, ghi analytics.
4. Deploy Lambda `FightingGameMatchAnalytics`.
5. Event source mapping từ stream.
6. **Game server:** `markMatchFinished` — `status=finished`, winner, `endedAt`, player id = Cognito `sub`.
7. **Consumer:** copy khi MODIFY finished; xử lý REMOVE khi rematch.
8. Chơi trận test → kiểm tra `MatchAnalytics` và CloudWatch Logs.

## Thiết kế

Rematch xóa `ActiveMatches`; analytics lưu ở bảng riêng trước khi xóa.
