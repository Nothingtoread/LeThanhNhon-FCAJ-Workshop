---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# FCAJ Community Day / AWS Community Day — Attendance Report

**Event:** FCAJ Community Day (AWS Community Day)  
**Date:** 23 May 2026  
**Location:** FCAJ venue (main hall + floor 36 streaming)  
**Role:** Attendee

## Event overview

A full-day FCAJ community event with technical and career sessions on AI adoption, platform engineering, Amazon Quick agents, CloudFront pricing, hackathon product building, LLM determinism, and enterprise multi-agent systems for banking credit assessment.

## Speakers

| # | Speaker | Role / organization |
|---|---------|---------------------|
| 1 | **Nguyễn Gia Hưng** | Head of Solution Architect, **Amazon Web Services Vietnam**; Founder, **FCAJ** |
| 2 | **Tịnh Trương** | Platform Engineer, **GothamX** |
| 3 | **Hải Anh** | **Pacific Vietnam** |
| 4 | **Nguyễn Hấn Thịnh** | DevOps Engineer (FCAJ alumni) |
| 5 | **Uyển** | Hackathon winner — **UTMorph** (with teammates **Thảo**, **MCH**) |
| 6 | **Thảo** | Co-presenter, **UTMorph** |
| 7 | **Đức Đào** | Engineer |
| 8 | **Vy Lâm** | Engineer, **VPBank** (~2 years) |

---

## Session summaries

### Nguyễn Gia Hưng — AI, careers & building what employers need

Hưng framed AI as lowering the cost of software production, which increases total demand for software (similar to LEDs increasing electricity use)—creating more work for engineers who can ship, operate, and fix AI-assisted systems, not fewer jobs.

Near-term hiring is difficult due to macro AI investment cycles, but long-term demand for builders in Vietnam remains strong given global outsourcing hubs. **University alone is insufficient:** graduates need (1) solid technical foundation, (2) real industry use cases for their target sector, and (3) **products**, not demos—something a director can evaluate on day one. AI capability advances roughly every four months; delaying skill-building widens the gap. Banks still hire large development teams but increasingly need platform/operations engineers to run what developers deliver.

---

### Tịnh Trương — Context engineering & platform engineering (GothamX)

As a platform engineer, Tịnh explained evolving from ticket-based DevOps to self-service platforms that let developers provision safely at scale.

**Core message — context is everything:** Mixing unrelated topics in one chat (travel + career + coding) degrades results. For fintech/banking work, feed **company-specific context** (blueprints, internal standards) rather than generic knowledge the model already has. Maintain ~70% of a session focused on one problem; continue context across turns instead of restarting cold.

**Career angle:** In cohorts of 120–140 graduates, engineers who apply AI with **domain context** stand out—even for non-AI roles. Mentioned AI second-brain workflows (e.g. Obsidian) for long-term knowledge retention.

---

### Hải Anh — Amazon Quick & agentic BI (Pacific Vietnam)

Hải Anh shared presenting at AWS Summit Singapore (age 22) and Silicon Valley (age 23), emphasizing solving real user problems over seniority.

**Problem:** Managers spend excessive time compiling weekly reports from scattered files across Microsoft 365, Google, Teams, Gmail, etc.

**Amazon Quick / Quick Desktop:** Ingests data from connected ecosystems so non-BI experts can ask agents to analyze spreadsheets, build dashboards, summarize meetings, and automate follow-ups. Demo flows included Excel → dashboard and meeting transcription/summary. **Agent = LLM + actions (MCP/tools).** Enterprise adoption requires shared responsibility for security and data governance.

---

### Nguyễn Hấn Thịnh — Amazon CloudFront flat-rate pricing

Thịnh focused on **CloudFront flat-rate pricing** as a response to unpredictable classic CDN bills when traffic spikes (viral content, DDoS) cause catastrophic monthly costs.

**Flat-rate tiers** (Free / Pro / Business / Premium) bundle WAF, Route 53, S3 credits; **overage throttles bandwidth** instead of unlimited extra charges. One distribution per plan per website; Terraform/CDK may default to classic pricing—console enablement may be required initially.

**Technical depth covered:** Global PoPs and backbone, faster DDoS/volumetric protection than default Shield observation windows, cost optimization with S3/ALB origins, compression, HTTPS/ACM, VPC origins, multi-tier caching, HTTP/3 multiplexing, TCP connection reuse, and **CloudFront Functions** at the edge for lightweight logic.

---

### Uyển & Thảo — UTMorph hackathon journey (36 hours)

Team **UTMorph** (Uyển, Thảo, MCH + *morphē* = new form) won a national 36-hour hackathon (~2 months before this event).

**Problem:** AI UI generators force full regeneration when tweaking colors/spacing—they built direct on-canvas editing (drag components, edit CSS, version history, publish HTML link).

**Process lessons:**
- Start from daily pain, not abstract “save the world” ideas.
- Scope ruthlessly under fixed time (12h ideation + ~16h build in their timeline).
- Token limits, AI over-generation, and fatigue near deadline are real risks.
- Colleagues who know each other’s strengths ship faster under pressure.

**Architecture (Thảo):** Serverless on AWS; **3-agent pipeline**—vision analysis → layout/CSS generation → design-system-aware code generation; live demo of dashboard generation + visual editor.

**Team dynamics:** Split work by strengths (UI/frontend vs. backend/agents), sync periodically to avoid duplicate effort. Managed health (food, rest) across 36 hours to survive final pitch.

---

### Đức Đào — LLM temperature, determinism & production design

Đức Đào presented research shared internally at his company on why **temperature = 0 does not guarantee identical LLM outputs** on hosted APIs.

**How LLMs choose tokens:** Models score vocabulary (logits), rank candidates, and sample—temperature, top-p, and top-k control randomness vs. creativity. Low temperature narrows choice toward highest-probability tokens; high temperature flattens the distribution for more diverse outputs.

**The myth:** Teams assume T=0 means deterministic automation-compatible output. In practice, **inference optimization** (kernels, batching, provider-side behavior) introduces variance even at T=0—demonstrated on **Amazon Bedrock** with two models at temperature zero producing different outputs for the same prompt.

**Mitigation strategies:**
- Multi-run voting / consensus for critical extractions.
- Self-hosted models for full control when regulation requires it.
- Provider modes (e.g. JSON mode) where available.
- Design downstream services to tolerate format variation (defensive parsing).
- Prefer T≈0.1 over exactly 0 to avoid repetition loops; use `repeat_penalty` cautiously for code generation.
- **Read official model documentation** (e.g. Claude 3.x guidance) before tuning hyperparameters—prompt engineering may matter more than parameter fiddling on documented models.

**Takeaway:** Treat LLMs as **probabilistic engines**—design for variance, test extensively, and never assume fixed strings in production pipelines.

---

### Vy Lâm — Enterprise multi-agent startup credit assessment (VPBank)

Vy Lâm shifted from pure technology to **business mindset**, opening with four questions before architecture: **Who uses it? What problem? Why your solution? When is it appropriate?** (How was covered by earlier sessions.)

**Use case:** Credit assessment for **startups** in Vietnam’s growing startup economy (government push 2024–2026). Traditional bank models require multi-year financial statements, credit history, and physical collateral—startups often have only traction, team, IP, and pitch decks.

**Why multi-agent (not single agent):**
- Many document types and expert perspectives.
- Context window limits.
- One agent cannot credibly play financial analyst, market researcher, team evaluator, and risk officer simultaneously.

**Agent roles proposed:**
- **Orchestrator** — “credit committee host” coordinating specialists.
- **Financial analyst** — statements and metrics where available.
- **Market researcher** — industry and competitive context.
- **Team/founder evaluator** — leadership and execution signals.
- **Risk & compliance agent** — critical in banking; regulatory guardrails.

**Enterprise realities from 2 years at VPBank:**
- **MCP expands attack surface**—tools must be approved; even local Ollama may be blocked to prevent data leakage.
- **Guardrails:** prompt injection defense, input/output filtering, API key rotation, **audit trails** for human decisions on AI recommendations.
- **Knowledge transfer** from senior credit officers matters as much as RAG over documents—context engineering over naive “index everything.”
- Real incident: chatbot output pasted into production without code review caused operational issues.
- Hiring bias: **backend/software engineering fundamentals** + safe AI application; warns against Ctrl+C from ChatGPT into production.

**Production path:** POC → core build → SIT → UAT → pilot → scale; present **ROI** to leadership (e.g. time saved reading 200-page credit packs). Deployment sketch: local dev → containerize → **AgentCore runtime** on AWS; Cognito/JWT/OIDC for real auth.

---

## Takeaways

- **Context engineering** and production thinking separate hobby AI usage from employable skills.
- **CloudFront flat-rate** is a practical enterprise cost-control pattern for public-facing workloads.
- **Hackathon delivery** (scope, teamwork, demo-first pitching) mirrors startup pressure.
- **Enterprise AI** is constrained by compliance, auditability, and business ROI—not only model capability.
- LLM workflows must assume **non-determinism** even at temperature zero.

## Personal reflection

The event connected FCAJ’s community spirit with deeply practical sessions—from CloudFront billing predictability to VPBank’s frank view of multi-agent systems under banking regulations. The repeated theme was clear: build real products, understand what you ship, and learn to articulate business value—not only service names.
