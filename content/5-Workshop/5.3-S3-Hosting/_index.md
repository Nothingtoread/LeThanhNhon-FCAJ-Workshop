---
title: "S3 Hosting"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Goal

Host the **browser game client** (HTML, JS, sprites, sounds) from S3 static website hosting. CI later syncs built assets on each deploy.

## Step 1 — Create the assets bucket

1. **S3 → Create bucket**.
2. Name: `fighting-game-assets-508768431157` (or your account-scoped name).
3. Region: `ap-southeast-1`.
4. Block Public Access: adjust as needed for static website demo (see policy below).

## Step 2 — Enable static website hosting

1. Open bucket → **Properties → Static website hosting → Enable**.
2. Index document: `index.html`.
3. Error document (optional): `index.html` for SPA-style routing.
4. Note the **website endpoint** URL.

## Step 3 — Bucket policy (public read for demo)

1. **Permissions → Bucket policy** — allow `s3:GetObject` for `arn:aws:s3:::fighting-game-assets-508768431157/*` with principal `*` (demo only; tighten for production).
2. Save and verify no policy errors.

## Step 4 — Configure CORS

1. **Permissions → Cross-origin resource sharing (CORS)**.
2. Allow origins for your S3 website URL and local dev if needed.
3. Allow methods: `GET`, `HEAD`; headers needed for Cognito/API calls from browser.
4. Without CORS, login and API calls from the browser origin will fail.

## Step 5 — Upload client bundle

1. Build the client locally or via CI artifact.
2. Upload `index.html`, JS bundles, `src/config.js`, assets (sprites, sounds).
3. Open the website endpoint and confirm the game loads.

## Step 6 — CI integration (GitHub Actions)

The repo `deploy.yml` syncs the built client to this bucket on each deploy and generates `src/config.js` from repository secrets (`COGNITO_*`, `MATCHMAKER_API_BASE`, `WS_SERVER`, etc.).

## Expected outcome

- Public S3 website serves the game client
- Browser can call Cognito and MatchMaker API without CORS errors
- Each CI run refreshes static assets

## Note on HTTPS

S3 website endpoints are **HTTP**. For production demos requiring `wss://`, use CloudFront in front of S3 or serve from a HTTPS-capable endpoint.
