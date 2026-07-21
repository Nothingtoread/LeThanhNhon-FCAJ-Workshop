---
title: "S3 Hosting"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Mục tiêu

Host browser client qua S3 static website.

## Bước 1 — Tạo bucket

![Tạo và cấu hình S3 bucket](/images/5-Workshop/image6.png)

## Bước 2 — Static website hosting

![Static website hosting](/images/5-Workshop/image7.png)

## Bước 3 — Bucket policy

![Bucket policy (public read)](/images/5-Workshop/image8.png)

## Bước 4 — CORS

Cấu hình CORS cho origin website và API/Cognito từ browser.

## Bước 5–6 — Upload bundle & CI

Upload client; GitHub Actions sync qua `deploy.yml`.
