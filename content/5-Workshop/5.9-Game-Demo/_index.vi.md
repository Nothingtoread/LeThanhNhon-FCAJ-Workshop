---
title: "Game Demo"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Game trực tiếp

**Chơi client đã deploy:** [http://fighting-game-assets-508768431157.s3-website-ap-southeast-1.amazonaws.com/](http://fighting-game-assets-508768431157.s3-website-ap-southeast-1.amazonaws.com/)

Browser client được host trên S3 static website. Người chơi đăng nhập qua **Cognito**, xếp trận qua **API Gateway + MatchMaker Lambda**, rồi kết nối tới **EC2 Spot** game server cổng **9000**.

## Luồng xác thực

### Đăng nhập

![Màn hình đăng nhập](/images/5-Workshop/5.9-Game-Demo/game-login.png)

### Đăng ký

![Màn hình đăng ký](/images/5-Workshop/5.9-Game-Demo/game-signup.png)

### Xác minh email

Cognito gửi mã xác nhận tới email đã đăng ký.

![Email xác minh trong Gmail](/images/5-Workshop/5.9-Game-Demo/game-email-verification.png)

![Nhập mã xác nhận trong game](/images/5-Workshop/5.9-Game-Demo/game-confirmation-code.png)

## Matchmaking & gameplay

### Tìm trận

![Đang tìm trận](/images/5-Workshop/5.9-Game-Demo/game-finding-match.png)

### Trong trận

![PvP trong game](/images/5-Workshop/5.9-Game-Demo/in-game.png)

### Màn hình chiến thắng

![Màn hình chiến thắng](/images/5-Workshop/5.9-Game-Demo/victory.png)
