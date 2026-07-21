---
title: "Blog 1"
date: 2026-05-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# HOW ALS GEOANALYTICS' LITHOLENS REVOLUTIONIZES CORE LOGGING THROUGH MACHINE LEARNING WITH AMAZON EKS

ALS Geoanalytics developed **LithoLens**, a cloud-native platform utilizing computer vision and machine learning (ML) to automate and optimize the process of geological core logging. The system automates the ingestion, classification, and analysis of drill core photographs, significantly speeding up geological evaluations for mining and resource exploration.

### Key Architectural Components:

- **Client Access & API Layer:**  
  The client applications connect securely through **Amazon API Gateway** and **AWS Lambda** (API Layer), with user authentication managed via **Amazon Cognito**.

- **Compute & Processing Layer:**  
  **Amazon EKS (Elastic Kubernetes Service)** orchestrates the containerized machine learning inference workloads. Running models on EKS allows ALS to scale container instances dynamically based on the volume of images being processed.

- **Storage & Database Layer:**
  - **Amazon S3** stores the massive volume of high-resolution drill core images.
  - **Amazon RDS** manages metadata, user accounts, and structural geological records.
  - **Amazon CloudWatch** monitors application performance and stores operational logs.

### Benefits of the Architecture:

- **Scalability:** Auto-scaling Kubernetes clusters in EKS efficiently handle spikes in machine learning workloads.
- **Cost Efficiency:** Serverless APIs (API Gateway & Lambda) combined with scalable containers ensure ALS only pays for active computing resource usage.
- **Performance:** GPU-optimized instances in EKS speed up deep learning image inference.

---

### Architecture Diagram:

![LithoLens Architecture](/images/3-BlogsPosted/blog1.png)

---

### Links and References:

- **Facebook Post:** [AWS Study Group Facebook Post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2199204024177891/)
- **Reference Article:** [How ALS Geoanalytics' LithoLens revolutionizes core logging through machine learning with Amazon EKS](https://aws.amazon.com/vi/blogs/architecture/how-als-geoanalytics-litholens-revolutionizes-core-logging-through-machine-learning-with-amazon-eks/)
