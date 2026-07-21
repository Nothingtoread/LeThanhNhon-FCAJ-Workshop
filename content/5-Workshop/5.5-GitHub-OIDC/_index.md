---
title: "GitHub OIDC"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Goal

Authenticate **GitHub Actions** to AWS using **OIDC**—no long-lived `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY` in repository secrets.

## Step 1 — Add GitHub as OIDC identity provider

1. **IAM → Identity providers → Add provider**.
2. Provider type: **OpenID Connect**.
3. Provider URL: `https://token.actions.githubusercontent.com`
4. Audience: `sts.amazonaws.com`
5. Create provider.

## Step 2 — Create IAM role for GitHub Actions

1. **IAM → Roles → Create role**.
2. Trusted entity: **Web identity** → select the GitHub OIDC provider.
3. Condition (example):

```json
"StringEquals": {
  "token.actions.githubusercontent.com:aud": "sts.amazonaws.com"
},
"StringLike": {
  "token.actions.githubusercontent.com:sub": "repo:Nothingtoread/fighting-game:*"
}
```

4. Role name: `GitHubActionsFightingGameDeploy` (or your chosen name).
5. Attach permissions policy from [5.4 IAM](5.4-IAM/).

## Step 3 — Configure repository secrets

In **GitHub → Settings → Secrets and variables → Actions**, add:

| Secret | Purpose |
|--------|---------|
| `AWS_ROLE_ARN` | ARN of the OIDC role |
| `AWS_REGION` | `ap-southeast-1` |
| `ASSETS_BUCKET` | S3 bucket name |
| `COGNITO_*` | User pool / client IDs for generated `config.js` |
| `MATCHMAKER_API_BASE` | API Gateway base URL |
| `WS_SERVER` | WebSocket server hint for client |

Do **not** store static AWS access keys.

## Step 4 — Update GitHub Actions workflow

In `.github/workflows/deploy.yml`:

```yaml
permissions:
  id-token: write
  contents: read

- uses: aws-actions/configure-aws-credentials@v4
  with:
    role-to-assume: ${{ secrets.AWS_ROLE_ARN }}
    aws-region: ap-southeast-1
```

## Step 5 — Verify OIDC login

1. Push a commit to trigger the workflow.
2. Confirm **Configure AWS credentials** step succeeds.
3. Confirm S3 sync and Lambda/CodeDeploy steps run without key errors.

## Expected outcome

- CI uses short-lived credentials via `AssumeRoleWithWebIdentity`
- No static AWS keys in GitHub secrets
- Same role can be rotated or scoped by updating IAM only
