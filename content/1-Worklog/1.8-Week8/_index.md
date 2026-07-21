---
title: "Week 8 Worklog"
date: 2026-06-23
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Hand off the client with login flow to the team (netcode + auth sketch complete).
* Begin CI/CD implementation using GitHub and GitHub Actions.

**Period:** 23/06/2026 – 29/06/2026

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| 2 | - Finalize client login UI and session handling for team integration | 23/06/2026 | 23/06/2026 | |
| 3 | - Hand off client codebase with documented auth + netcode interfaces | 24/06/2026 | 24/06/2026 | |
| 4 | - Set up GitHub repository structure (`Nothingtoread/fighting-game`) | 25/06/2026 | 25/06/2026 | |
| 5 | - **CI/CD:** Create initial GitHub Actions workflow for build and deploy | 26/06/2026 | 26/06/2026 | GitHub Actions docs |
| 6 | - Configure S3 static website hosting for the browser client <br> - Test first automated deploy pipeline | 27/06/2026 | 27/06/2026 | |

### Week 8 Achievements:

* Delivered a working client handoff package with login flow and netcode stubs for the team.
* Created the project repository and established branching conventions.
* Implemented the first GitHub Actions workflow (`deploy.yml`) for automated client builds.
* Created the S3 assets bucket with static website hosting, public-read policy, and CORS configuration.
* Verified that CI can sync the built client bundle (including generated `config.js`) to S3 on each push.
