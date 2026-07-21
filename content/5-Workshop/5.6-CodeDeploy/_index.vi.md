---
title: "CodeDeploy"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Mục tiêu

Deploy tự động **Lambda MatchMaker** (canary alias `live`) và **fleet EC2** qua CodeDeploy + GitHub Actions.

## Phần A — Lambda

1. Publish version mới, trỏ alias **`live`**.
2. CodeDeploy app `FightingGameMatchmakerDeploy` — config kiểu linear 10%/phút.
3. CI upload zip, tạo deployment, chờ hoàn tất.

## Phần B — EC2

1. Cài **CodeDeploy agent** trên Ubuntu 24.04 — patch `.deb` `ruby3.2` → `ruby3.3` (xem lệnh đầy đủ bản EN).
2. Cập nhật launch template và warm pool có agent.
3. App `FightingGameServerDeploy`, group `FightingGameServer-fleet`, tag `Role=FightingGameServer`.
4. `appspec.yml` + hooks: BeforeInstall, AfterInstall, ApplicationStart (health-check retry), ValidateService.
5. CI đóng gói `fighting-game.env` trong zip; sửa CRLF `application_start.sh`.

## Xác minh

Deployment **Succeeded** trên console; game server chạy binary mới cổng 9000.
