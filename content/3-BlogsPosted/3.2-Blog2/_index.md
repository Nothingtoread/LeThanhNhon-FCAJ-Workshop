---
title: "Blog 2"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# PROVISIONING ORACLE DATABASE@AWS RESOURCES USING TERRAFORM

This blog explores **Oracle Database@AWS**, a co-location service that brings Oracle Cloud Infrastructure (OCI) database services directly into AWS data centers. This solution allows companies to run enterprise-grade Oracle Exadata database workloads inside AWS with sub-millisecond latency connection to AWS services like Amazon EC2.

### Key Architectural Concepts:

- **Customer VPC & Application Layer:**  
  The client applications run on **Amazon EC2** instances inside a standard AWS Customer VPC.

- **Oracle Database (ODB) Network:**  
  An ODB Network VPC is established inside the AWS Region, housing client and backup subnets. It connects to the Customer VPC via **ODB Peering**.

- **OCI Child Site (Co-located inside AWS Datacenter):**  
  The OCI Child site contains the actual physical **Exadata Infrastructure** running OCI Virtual Cloud Network (VCN) client and backup subnets mapped directly to AWS subnets.

- **Control Plane & Automation:**  
  Resource orchestration and lifecycle management are automated via **OCI Automation** connected to the **OCI Control Plane** in the OCI Parent Region.

### Infrastructure as Code (IaC) with Terraform:

By using the **Terraform** OCI and AWS providers, cloud engineers can provision this entire cross-cloud infrastructure in a unified workflow:

1. Create VPCs, Subnets, and Route Tables in AWS.
2. Initialize OCI provider to provision the Exadata Infrastructure.
3. Configure the private connectivity and network peering between AWS and OCI child sites automatically.

---

### Architecture Diagram:

![Oracle Database@AWS Architecture](/images/3-BlogsPosted/blog2.png)

---

### Links and References:

- **Facebook Post:** [AWS Study Group Facebook Post](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2198792150885745/)
- **Reference Article:** [Provision Oracle Database and AWS resources using Terraform](https://aws.amazon.com/vi/blogs/database/provision-oracle-databaseaws-resources-using-terraform/)
