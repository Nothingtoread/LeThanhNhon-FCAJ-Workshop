---
title: "CodeDeploy"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Goal

Automate **zero-downtime deployments** for MatchMaker **Lambda** (alias traffic shifting) and **EC2 game servers** (fleet rolling deploy) via AWS CodeDeploy and GitHub Actions.

---

## Part A — Lambda (MatchMaker)

### Step 1 — Publish versions and `live` alias

1. After each code change, **publish a new Lambda version**.
2. Point the **`live` alias** at the new version for production traffic.
3. Use CodeDeploy deployment configuration (e.g. `CodeDeployDefault.LambdaLinear10PercentEvery1Minute`) for gradual shift (~10 minutes for full cutover).

![Publishing new version](/images/5-Workshop/image20.png)

### Step 2 — API Gateway stage management

- During canary deploys, manage **active vs dormant** API stages so traffic follows the `live` alias without breaking in-flight matchmaking.

![Dormant prod stage](/images/5-Workshop/image22.png)

![Dormant prod stage (continued)](/images/5-Workshop/image23.png)

![Redeploy for live versioning](/images/5-Workshop/image21.png)

### Step 3 — CodeDeploy application (Lambda)

1. **CodeDeploy → Create application** → Compute platform: **AWS Lambda**.
2. Name: `FightingGameMatchmakerDeploy`.
3. Deployment group linked to MatchMaker function + `live` alias.
4. Service role: Lambda CodeDeploy service role (from [5.4](5.4-IAM/)).

![Create role for CodeDeploy](/images/5-Workshop/image24.png)

### Step 4 — CI trigger

GitHub Actions packages `lambda-matchmaker` zip, uploads to S3, registers revision, creates CodeDeploy deployment, waits for success (helper scripts: `codedeploy-create-with-retry.sh`, `codedeploy-wait-idle.sh`).

---

## Part B — EC2 (game server fleet)

### Step 1 — Install CodeDeploy agent on Ubuntu 24.04

Ruby 3.3 requires patching the agent `.deb` (`ruby3.2` → `ruby3.3` in control file):

```bash
sudo apt-get update && sudo apt-get install -y ruby-full ruby-webrick wget gdebi-core
cd /tmp
wget https://aws-codedeploy-ap-southeast-1.s3.ap-southeast-1.amazonaws.com/releases/codedeploy-agent_1.8.1-26_all.deb
dpkg-deb -R codedeploy-agent_1.8.1-26_all.deb /tmp/codedeploy-extracted
sed -i 's/ruby3.2/ruby3.3/g' /tmp/codedeploy-extracted/DEBIAN/control
dpkg-deb -b /tmp/codedeploy-extracted /tmp/codedeploy-agent_fixed.deb
sudo dpkg -i /tmp/codedeploy-agent_fixed.deb
sudo systemctl enable codedeploy-agent && sudo systemctl start codedeploy-agent
sudo systemctl status codedeploy-agent
```

### Step 2 — Bake agent into AMI / launch template

1. Update **launch template** so new Spot instances include the agent.
2. Refresh **warm pool** instances (terminate old, let ASG replace) or run install on each warm instance.

![Update launch template with CodeDeploy agent](/images/5-Workshop/image25.png)

![Warm pool and Spot instances with CodeDeploy agent](/images/5-Workshop/image26.png)

### Step 3 — CodeDeploy EC2 application

1. **CodeDeploy → Create application** → Compute platform: **EC2/On-premises**.
2. Name: `FightingGameServerDeploy`.
3. **Deployment group:** `FightingGameServer-fleet`.
4. Target: EC2 instances tagged `Role=FightingGameServer`.
5. Service role: `CodeDeployServiceRoleForEC2` with `AWSCodeDeployRole` (not the Lambda deploy role).

![Create CodeDeploy EC2 application](/images/5-Workshop/image27.png)

![EC2 deployment group config](/images/5-Workshop/image28.png)

### Step 4 — AppSpec and lifecycle scripts

Repository includes `appspec.yml` and scripts:

| Hook | Purpose |
|------|---------|
| `BeforeInstall` | Stop old process, prep directories |
| `AfterInstall` | Place new server files |
| `ApplicationStart` | Start game server, health-check loop |
| `ValidateService` | Confirm port 9000 / process health |

**Fixes applied:** CRLF stripping in `application_start.sh`; retry loop on health check; CI generates `fighting-game.env` inside zip with Cognito/DynamoDB env vars for EC2.

### Step 5 — Run deployment

1. CI builds `game-server.zip`, registers revision, creates deployment.
2. Monitor **CodeDeploy → Deployments** until **Succeeded**.
3. Verify new binary on fleet and successful match on port 9000.

![Successful CodeDeploy job](/images/5-Workshop/image29.png)

---

## Verification

- [ ] Lambda `live` alias points to new version after canary
- [ ] EC2 deployment group shows **Succeeded** in history
- [ ] Game server process restarts with new code without manual SSH

## Troubleshooting

| Issue | Action |
|-------|--------|
| ApplicationStart failed | Check `application_start.sh` line endings, port 9000, env file in zip |
| Agent not running | Re-run patched `.deb` install; check `systemctl status codedeploy-agent` |
| Wrong CodeDeploy role on EC2 group | Use `CodeDeployServiceRoleForEC2`, not Lambda role |
