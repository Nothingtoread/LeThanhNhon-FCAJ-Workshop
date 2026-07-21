---
title: "Async Processing"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Mục tiêu

Flow E — copy dữ liệu trận đã kết thúc sang `MatchAnalytics` qua DynamoDB Streams.

![Tổng quan async processing](/images/5-Workshop/image30.png)

## DynamoDB

![Thiết lập DynamoDB](/images/5-Workshop/image31.png)

## IAM & Lambda analytics

![Match analytic role](/images/5-Workshop/image34.png)

![Stream reading policy](/images/5-Workshop/image35.png)

![Role MatchAnalytic Lambda](/images/5-Workshop/image36.png)

![Match Analytic Lambda](/images/5-Workshop/image37.png)

## Xác minh

![Finished state trong DynamoDB](/images/5-Workshop/image32.png)

![Chi tiết finished state](/images/5-Workshop/image33.png)

![Dữ liệu DynamoDB](/images/5-Workshop/image38.png)
