---
title: "Event 3"
date: 2026-06-27
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# FCAJ Community Day — Attendance Report

**Event:** FCAJ Community Day  
**Date:** 27 June 2026  
**Location:** FCAJ venue (floors 26 & 36, with YouTube livestream)  
**Role:** Attendee

## Event overview

A monthly FCAJ community event bringing industry speakers from AWS partners and startups. Sessions covered cloud careers, agentic AI for operations, Vietnamese voice AI, AWS DevOps Agent, Amazon Quick for HR, and secure private MCP integration for enterprise Quick deployments.

## Speakers

| # | Speaker | Role / organization |
|---|---------|---------------------|
| 1 | **Steve Trần** | Founder, **CloudThinker** |
| 2 | **Hiếu Nghị** | **Renova Cloud**; AWS Community Builder |
| 3 | **Kiệt** | **Student Video Group** |
| 4 | **Trung** | Founder & CEO, **R AI** |
| 5 | **Nguyên Nguyễn** | Cloud Engineer, **Cloud Kinetics** |
| 6 | **Bảo** | Cloud Engineer, **Cloud Kinetics** |
| 7 | **Trường Anh (Wayne)** | AI Solutions, **Noventis** |
| 8 | **Minh Anh** | Solutions team, **Noventis** |
| 9 | **Toàn Nguyễn** | **AWS Security Builder** |
| 10 | **Hiếu Nghị** | **Renova Cloud** (closing session, with Toàn Nguyễn) |

---

## Session summaries

### Steve Trần — Career journey & CloudThinker agentic platform

Steve opened by shifting from a product pitch to a career narrative aimed at early-year and final-year students, sharing his path from contact-center IT (physically rebooting on-prem servers at age 19) through failed Azure certification attempts to AWS, where documentation clarity helped him pass Developer and Solutions Architect certifications within roughly a year during the 2020–2021 COVID cloud boom.

His career arc in ~4 years: IT engineer at FPT (airport server projects) → AWS Vietnam Solution Architect. He emphasized predicting where demand would concentrate (cloud) and investing continuously while working.

**AI and hiring today:** Many companies paused junior hiring or hire only seniors who work well with AI; coding speed from AI tools is accelerating dramatically. His recommendation: gain enterprise exposure through internships or early jobs to build experience before graduation.

**The problem CloudThinker solves:** As enterprises migrate to cloud, operational complexity grows—more DevOps/SRE/SOC hires and more observability tools, yet complexity still rises (“technical debt” in legacy systems running millions of users daily). AI should **support** expert engineers on critical cloud infrastructure, not replace them—production outages cost millions per minute.

**CloudThinker agentic platform (four pillars):**

1. **Incident response** — AI investigation in minutes vs. human hours (e.g. bank payment failures).
2. **AI code review** — Coding accelerated by AI but QA/automation testing lagged; leadership invests millions in SDLC yet delivery throughput unchanged. CloudThinker reviews infrastructure and code changes before production.
3. **FinOps** — Cost optimization still heavily manual; CloudThinker uses AI that understands AWS and finance to assist FinOps teams (customers shifting FinOps headcount toward product development).
4. **Security** — Continuous dynamic pentesting vs. quarterly manual tests; assesses infrastructure, code, and logging. Helps dev squads without embedded DevOps provision/debug environments in minutes.

He discussed **single-agent vs. multi-agent** architecture trade-offs (referencing a student’s LangGraph portfolio project) and startup lessons: validate real customer problems, map ideas to enterprise needs, and persist through early failure.

---

### Hiếu Nghị, Kiệt & Trung — Voice AI for Vietnamese enterprise

**Hiếu Nghị (Renova Cloud)** introduced why voice AI matters in Vietnam: scarce Vietnamese speech data and models compared to English; opportunity for students to research, compete, and pursue voice-related roles.

**Two architectures:**
- **Speech-to-speech** — audio in, audio out (common in global models).
- **Three-stage pipeline** — STT → LLM → TTS (used by many production voice bots, e.g. Viettel *098#).

**Kiệt (Student Video Group)** demoed a voice agent on **Amazon Bedrock AgentCore** with knowledge base, answering Apple MacBook product questions in English (live demo had mic issues—a lesson that voice demos are high-risk).

**Trung (Founder & CEO, R AI)** explained production voice for Vietnamese banks (VPBank, VIP):

- Global speech-to-speech models are English-centric; Vietnamese is a **low-resource language**.
- Banks require **controllable text output** before TTS—filter what the AI says, enable **tool calling** (e.g. card lock after collecting ID), which speech-to-speech handles poorly.
- **Production engineering:** full streaming (audio→text→LLM→TTS), gender detection for polite *anh/chị* address in Vietnamese, **turn-taking / barge-in** detection (knowing when the customer paused mid phone number vs. finished speaking), audit logs, prompt versioning, knowledge base, and **human handoff** when AI cannot handle abuse or complexity.
- **Regional accents:** STT/TTS trained with ~10–20% regional voices; standard accent works; heavy dialect vocabulary still challenging; some debt-collection use cases intentionally use mild regional TTS for effectiveness.

---

### Nguyên Nguyễn & Bảo — AWS DevOps Agent (Cloud Kinetics)

**Problem:** Manual incident investigation suffers from fragmented telemetry (CloudWatch, X-Ray, etc.), knowledge silos across teams, constant context switching, higher **MTTD/MTTR**, and context loss linking logs across services.

**AWS DevOps Agent** automates investigation on triggers (CloudWatch alerts, PagerDuty, or chat), proposes mitigations, and learns over time.

**Six pillars:**
1. **Context learning** — Agent space as logical container; learns topology (~300 relationships in demo after ~15 min); skills and memory accumulate across incidents.
2. **Control** — IAM/tag-scoped permissions; private connectivity options.
3. **Integration** — MCP extensions (e.g. custom DB query tools for deeper investigation).
4. **Collaboration** — Web UI, Slack, ServiceNow, PagerDuty; enable from AWS Console.
5. **Cost** — Priced by **runtime** (~$0.0083/second), not tokens.
6. **Workflow** — Classify → investigate (hypothesis loop) → mitigate (recommend only, human executes) → improve (prevent recurrence).

**Live demo (Bảo):** E-commerce on ECS behind ALB; simulated DDoS (~1000 RPS from 10 tasks); DevOps Agent in Vietnamese identified root cause, mitigation steps (stop tasks, remove task definition), integrated chat to run CLI suggestions—app recovered. **MTTR case study:** online university (~200k students) cut incident handling from ~2 hours to ~28 minutes (~77% MTTR reduction) using Datadog + DevOps Agent.

**Prerequisites:** mature observability, large multi-service estates; agent recommends only—humans approve and execute.

---

### Trường Anh & Minh Anh — AI, HR challenges & Amazon Quick (Noventis)

**Trường Anh (Wayne)** shared joining FCAJ in December 2024 knowing little at first, growing to customer-facing solution work through community learning—emphasizing that careers are not only technical but also about people (HR).

**Minh Anh** framed **HR challenges in the AI era:**
- Manual CV screening misses talent; subjective, inconsistent evaluation; slow time-to-hire (1–2 months); burnout; wrong hires delay projects and increase cost.
- Risk of uploading candidate data to public AI without data protection.

**Amazon Quick as HR enabler:** agentic assistant turning answers into actions; connects Microsoft 365, Google Workspace, SharePoint, Outlook, Gmail, Drive, Jira, Salesforce, GitHub, S3, relational DBs, and custom MCP—model choice via Bedrock (Nova, Claude) with governance; Local Zone support in Vietnam.

**Trường Anh — Quick capabilities:** custom agents (recruiting, policy, sales, research); research with internal + web sources and iterative refinement; **Quick Sight/BI** for operators; **flows/automate** for repetitive admin; **spaces** for permissioned knowledge.

**HR hiring workflow demo:** ingest CVs from LinkedIn, TopCV, email, or HR systems via MCP → AI screening against JD → schedule interviews via calendar integration → email candidates → pipeline tracking. Built **HR Talent Review Assistant** skill from markdown spec; auto-scored 6 CVs against a Junior Cloud Engineer JD (technical 40%, problem-solving 25%, communication 15%, etc.) with HTML visualization; demonstrated vi-coded applicant tracking board. Advised students: CVs are increasingly AI-screened—optimize for JD mapping.

---

### Toàn Nguyễn & Hiếu Nghị — Secure private MCP for Amazon Quick

**Hiếu Nghị (Renova Cloud)** continued the Quick theme for **enterprise security**: Quick on the public internet connecting to third parties is risky; enterprises need private paths.

**MCP recap:** protocol connecting Quick to Gmail, AWS resources, Zalo, WhatsApp, Jira, etc., via developer APIs.

**Toàn Nguyễn (AWS Security Builder)** — **private MCP architecture:**
- Public MCP endpoint exposes DDoS and man-in-the-middle risks; violates zero-trust and data-residency requirements.
- **Solution:** MCP server in **private subnet**; **VPC Lattice / VPC connection** + interface endpoint; internal DNS (Route 53 Resolver) not resolvable from internet; **ALB** with TLS (ACM) instead of direct EC2; **Cognito** authentication.
- Demo: public DNS query returned no records; from bastion inside VPC, Quick queried MCP for real-time ECS service/latency data—all traffic on AWS private network.

**Cost transparency (Nghị):** private setup ~$250–350/month baseline (Route 53 Resolver ~$180+, ALB ~$32+, EC2, Secrets Manager, data transfer)—needs per-customer sizing; data transfer usually smaller than infrastructure fixed costs.

---

## Takeaways

- Cloud infrastructure and operations roles remain critical; AI augments senior engineers rather than eliminating production accountability.
- Vietnamese voice AI requires pipeline architecture, streaming, and locale-specific UX (gender, turn-taking, accents).
- AWS DevOps Agent targets observability-mature organizations to compress MTTR with human-in-the-loop execution.
- Amazon Quick spans HR and technical workflows when connected securely via private MCP for regulated enterprises.
- Early internships and community participation (FCAJ) accelerate the transition from student to industry-ready practitioner.

## Personal reflection

This community day connected career strategy (Steve Trần), deep technical agents (voice, DevOps, Quick security), and business-facing HR automation. As an intern building on AWS, the through-line was consistent: understand production constraints—security, cost, human approval—and design AI as an accelerator inside those guardrails.
