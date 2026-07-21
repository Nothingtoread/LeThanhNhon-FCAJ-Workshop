---
title: "Game Demo"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Live game

**Play the deployed client:** [http://fighting-game-assets-508768431157.s3-website-ap-southeast-1.amazonaws.com/](http://fighting-game-assets-508768431157.s3-website-ap-southeast-1.amazonaws.com/)

The browser client is hosted on S3 static website hosting. Players sign in with **Cognito**, queue for a match through **API Gateway + MatchMaker Lambda**, then connect to an **EC2 Spot** game server on port **9000**.

## Authentication flow

### Login

![Game login screen](/images/5-Workshop/5.9-Game-Demo/game-login.png)

### Sign up

![Game sign-up screen](/images/5-Workshop/5.9-Game-Demo/game-signup.png)

### Email verification

Cognito sends a confirmation code to the registered email.

![Verification email in Gmail](/images/5-Workshop/5.9-Game-Demo/game-email-verification.png)

![Enter confirmation code in game](/images/5-Workshop/5.9-Game-Demo/game-confirmation-code.png)

## Matchmaking & gameplay

### Find match

![Finding match](/images/5-Workshop/5.9-Game-Demo/game-finding-match.png)

### In-game

![In-game PvP session](/images/5-Workshop/5.9-Game-Demo/in-game.png)

### Victory screen

![Victory screen](/images/5-Workshop/5.9-Game-Demo/victory.png)
