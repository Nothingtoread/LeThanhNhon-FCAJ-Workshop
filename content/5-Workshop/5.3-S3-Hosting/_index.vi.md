---
title: "S3 Hosting"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Mục tiêu

Host **browser client** (HTML, JS, asset) qua S3 static website; CI sync mỗi lần deploy.

## Các bước

1. Tạo bucket `fighting-game-assets-508768431157` tại `ap-southeast-1`.
2. Bật **static website hosting** — index `index.html`.
3. **Bucket policy** public read (demo).
4. **CORS** cho origin website và API/Cognito từ browser.
5. Upload bundle client; kiểm tra endpoint website.
6. GitHub Actions `deploy.yml` sync build + sinh `src/config.js` từ secrets.

## Lưu ý

S3 website là HTTP; cần CloudFront nếu demo yêu cầu HTTPS/`wss://`.
