---
title: "Async Processing"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Goal

Implement **Flow E** — when a match ends, copy finished match data from `ActiveMatches` to `MatchAnalytics` asynchronously via **DynamoDB Streams** and a Lambda consumer, without blocking gameplay.

## Step 1 — Enable DynamoDB Streams on ActiveMatches

1. **DynamoDB → Tables → ActiveMatches → Exports and streams**.
2. Enable stream view type: **NEW_AND_OLD_IMAGES** (needed to capture state before delete on rematch).

## Step 2 — Create MatchAnalytics table

1. **Create table** `MatchAnalytics`.
2. Design keys to match analytics queries (e.g. partition by match id or player).
3. On-demand or provisioned capacity per project choice.

## Step 3 — Create MatchAnalytics Lambda role

1. Role: `FightingGameMatchAnalyticsRole`.
2. Policy: `dynamodb:GetRecords`, `DescribeStream`, `ListStreams` on `ActiveMatches` stream ARN.
3. Policy: `dynamodb:PutItem` (and read if needed) on `MatchAnalytics`.

## Step 4 — Deploy FightingGameMatchAnalytics Lambda

1. Upload `backend/lambda-match-analytics.mjs` (or packaged zip from CI).
2. Runtime: Node.js (match project version).
3. Attach `FightingGameMatchAnalyticsRole`.

## Step 5 — Event source mapping

1. **Lambda → Configuration → Triggers → Add trigger**.
2. Source: DynamoDB stream of `ActiveMatches`.
3. Batch size and starting position per ops preference (typically **LATEST**).
4. Enable trigger.

## Step 6 — Application code behavior

**Game server (`server.js`):** On disconnect, `markMatchFinished` updates both player rows in `ActiveMatches`:

- `status = finished`
- `winner`, `endedAt`, `endReason`
- Player id = Cognito `sub`

**Stream consumer (`lambda-match-analytics.mjs`):**

- On **MODIFY** with `status=finished`, copy record to `MatchAnalytics`.
- On **REMOVE** (rematch `clearSession`), still archive if finished state was present (race handling).

**Design choice:** Rematch deletes rows from `ActiveMatches`; analytics land in `MatchAnalytics` before delete.

## Step 7 — Verify end-to-end

1. Play a full match until disconnect.
2. Check `ActiveMatches` rows show `finished`.
3. Confirm corresponding items in `MatchAnalytics`.
4. CloudWatch Logs for analytics Lambda show successful processing.

## Expected outcome

- Post-match analytics decoupled from real-time game loop
- Historical data retained after active session cleanup
- Stream errors visible in Lambda monitoring for replay/debug
