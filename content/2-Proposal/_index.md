---
title: "Proposal"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Serverless & Spot Instance Backend Architecture for Live-Service Games on AWS

## High-Performance, Scalable, and Cost-Optimized Cloud Infrastructure for Multiplayer Games

---

### 1. Executive Summary

This project presents a cloud-native backend architecture designed for live-service multiplayer games on Amazon Web Services (AWS). Instead of maintaining an expensive dedicated server fleet running 24/7 regardless of player demand, this architecture provisions compute resources dynamically **only when actually needed**: during player authentication, matchmaking, and active live game sessions.

All metagame components—including authentication, asset distribution, matchmaking, and post-match analytics—operate on a 100% **Serverless** architecture. The live game server sessions run within an **EC2 Spot Fleet** inside a dedicated, isolated VPC network boundary and are spun up dynamically by the Matchmaker service. Deployments and updates strictly follow **GitOps** practices, ensuring automated, zero-downtime releases without manual code execution on production.

---

### 2. Problem Statement

#### What's the Problem?

Traditional multiplayer game server architectures rely on dedicated EC2 instance fleets running continuously 24/7. During off-peak hours or low traffic periods, game studios suffer from massive idle compute costs. Furthermore, manual code deployments present severe operational risks, such as match interruptions, long deployment windows, and complex manual rollbacks. Keeping game server ports permanently open to the internet also exposes infrastructure to security threats and DDoS attacks.

#### The Solution

This architecture follows a core design rule: **Serverless for everything except live game sessions**.

- Low-latency metagame tasks (Auth, Asset Downloads, Matchmaking, Analytics) are handed off to AWS Serverless services (Cognito, API Gateway, Lambda, DynamoDB).
- Live game sessions run on an EC2 Spot Instance fleet (Graviton ARM64) inside a private/public VPC structure.
- Access to game servers is protected by dynamic Security Group rules managed by the Matchmaker Lambda, opening ports only for active players during a match and closing them immediately afterwards.
- Deployment is fully automated via GitHub Actions and AWS CodeDeploy using GitOps principles.

#### Benefits and Return on Investment (ROI)

- **Up to 80% Cost Reduction**: Eliminates idle server expenses by using EC2 Spot Instances combined with ARM64 Graviton processors, running compute only when matches occur.
- **Zero Egress & NAT Costs**: Eliminates NAT Gateway fees by routing internal Lambda traffic to DynamoDB and EC2 APIs via private VPC Endpoints.
- **Automated Zero-Downtime Deployment**: Blue/Green deployment via CodeDeploy allows gradual traffic shifting and instant rollback if a release fails, preventing match disruptions.
- **Enhanced Security**: Enforces strict trust boundaries, short-lived scoped IAM credentials for asset downloads, and dynamic Security Group management for game ports.

---

### 3. Solution Architecture

The architecture is divided into four distinct execution flows, each featuring its own trigger mechanisms and security trust boundaries.

![Live-Service Game Backend Architecture](/images/2-Proposal/architecture.png)

#### Architectural Flow Breakdown

##### **Flow C: GitOps Deployment Loop (CI/CD Pipeline)**

- Runs strictly during deployment and never interferes with live, ongoing game sessions.
- Developers push code and Infrastructure as Code (IaC) to Git. The GitOps pipeline (GitHub Actions) builds artifacts and triggers **AWS CodeDeploy**.
- CodeDeploy gradually shifts traffic to the new **AWS Lambda** version alias and updates AMI/Launch Templates for the **EC2 Auto Scaling Group (ASG)** Spot fleet.
- Simultaneously, the pipeline uploads client builds, patches, and server bundles to an **Amazon S3** asset bucket—serving as the unified artifact repository for both clients and EC2 instances.
- If a deployment error occurs, traffic shifts back automatically without interrupting running matchmaking services.

##### **Flow A: Player Auth & Asset Distribution**

- Players log in via **Cognito User Pool** (A1) and receive a JWT (A2).
- **Cognito Identity Pool** exchanges the JWT for temporary, prefix-scoped IAM credentials (A3).
- Game clients use these temporary credentials to download assets directly from S3 (A4): client builds, patches, and launcher files.
- The JWT token is passed to Flow R (A5)—the single intersection point between Auth and Matchmaking—allowing **API Gateway** to authorize incoming requests.

##### **Flow R: Synchronous Matchmaking & Session Provisioning**

- The client sends a matchmaking request via **Amazon CloudFront** (protected by **AWS WAF**) to **Amazon API Gateway** (R1).
- After Cognito Authorizer validates the JWT, **Matchmaker Lambda** (located in a private subnet) executes (R2):
  1. Writes match state to **Amazon DynamoDB** via a **VPC Gateway Endpoint** (R4).
  2. Calls the EC2 control plane via a private **VPC Interface Endpoint** (R3) to request a warm instance from the ASG Spot fleet (G1).
  3. Assigns a game room and configures dynamic **Security Group** rules specifically for the player's IP address.
- Matchmaker Lambda returns the server IP and port to the client. The client connects directly to the game instance via **Internet Gateway** (G3).
- When ASG launches a new EC2 instance, User Data scripts execute at boot, using an **IAM Instance Profile** to pull the latest server binary, config, and patch from S3 (G4). The instance initializes and immediately accepts assigned players.

##### **Flow E: Asynchronous Post-Match Processing & Analytics**

- Once a match concludes, results are written to DynamoDB.
- **DynamoDB Streams** automatically trigger a background **Lambda function** (E2) to capture post-match logs, calculate player stats, and push events to the analytics store (E3).
- This flow is completely decoupled from Flow R, ensuring post-match processing never impacts matchmaking latency.

#### AWS Services Used

- **Amazon Cognito**: User Pool (Authentication) & Identity Pool (Authorization / Temp IAM Credentials).
- **AWS WAF & Amazon CloudFront**: Edge security, DDoS protection, and global request routing.
- **Amazon API Gateway**: Serverless HTTP API endpoint handling player requests.
- **AWS Lambda**: Executes Matchmaker logic, CodeDeploy traffic management, and background log processing.
- **Amazon DynamoDB & DynamoDB Streams**: Single-table design for match state & real-time log capturing.
- **Amazon EC2 Spot Fleet (Graviton ARM64)**: Cost-effective, high-performance compute fleet for live game sessions.
- **AWS CodeDeploy & GitHub Actions**: Fully automated GitOps deployment pipeline.
- **Amazon S3 & AWS KMS**: Centralized asset repository with data-at-rest encryption.
- **VPC Endpoints (Gateway & Interface)**: Private network connections avoiding public internet egress.

---

### 4. Technical Implementation

#### Implementation Phases

1. **Phase 1: Architecture & Security Boundary Definition (Month 1)**  
   Design VPC subnets, route tables, IAM roles, security group automation, and KMS keys.
2. **Phase 2: Core Serverless Metagame & Auth Setup (Month 1-2)**  
   Implement Cognito User/Identity Pools, S3 asset bucket policies, API Gateway, and DynamoDB single-table schema.
3. **Phase 3: Matchmaker & EC2 Spot Automation (Month 2)**  
   Develop Matchmaker Lambda in private subnets, configure ASG Launch Templates with Graviton ARM64, and create User Data boot scripts.
4. **Phase 4: GitOps CI/CD & Asynchronous Analytics (Month 3)**  
   Set up GitHub Actions workflows, CodeDeploy Blue/Green deployment hooks, DynamoDB Streams for post-match processing, and conduct load testing.

#### Technical Requirements

- **Infrastructure as Code (IaC)**: AWS CDK / Terraform for full environment reproducibility.
- **Game Server Build**: Dockerized / binary game server compiled for Graviton (ARM64 Linux).
- **Security Standards**: TLS 1.3 in transit, KMS encryption at rest, principle of least privilege for IAM instance roles and temp user credentials.

---

### 5. Timeline & Milestones

- **Month 1**: System architecture design, VPC/Network topology setup, and IAM security boundaries.
- **Month 2**: Serverless matchmaking development, Cognito integration, and EC2 Spot ASG automation.
- **Month 3**: GitOps pipeline implementation, load & stress testing, performance tuning, and final deployment.

---

### 6. Budget Estimation & Cost Optimization

#### Cost Breakdown Highlights

- **Zero Idle Compute**: EC2 instances run ONLY during active matches. Matchmaking and Auth cost fractions of a cent via AWS Lambda & DynamoDB On-Demand.
- **70-90% Discount via Spot & Graviton**: Graviton ARM64 Spot Instances provide industry-leading price-to-performance ratio for game servers.
- **Elimination of NAT Gateway Fees**: Matchmaker Lambda communicates with AWS services inside private subnets using free/low-cost VPC Endpoints instead of expensive NAT Gateway data transfer.
- **Thin AMI Maintenance**: Game binaries and patches are pulled dynamically from S3 at boot time, eliminating the overhead and cost of rebaking AMIs for minor game patches.

---

### 7. Risk Assessment

| Risk Item | Impact | Probability | Mitigation Strategy |
| --- | --- | --- | --- |
| **Spot Instance Interruption** | Medium | Low | ASG maintains a small warm pool and uses multi-AZ Spot allocation strategies for instant replacement. |
| **Deployment Failure** | High | Low | AWS CodeDeploy performs gradual traffic shifting with automated rollback if health checks fail. |
| **Unauthorized Game Access** | High | Low | API Gateway validates JWT tokens; dynamic SG rules restrict game server access solely to authenticated player IPs during match windows. |

---

### 8. Expected Outcomes

- **Scalable Architecture**: Seamlessly handles spikes from 10 to 10,000+ concurrent players without manual intervention.
- **Extreme Cost Efficiency**: Reduces operational cloud bills by up to 80% compared to traditional 24/7 dedicated server setups.
- **Enterprise Security & Reliability**: Enforces strict network boundaries, GitOps deployment safety, and automated post-match analytics processing.
