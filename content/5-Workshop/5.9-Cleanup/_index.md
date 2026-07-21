---
title: "Cleanup"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

## Goal

Document the **teardown procedure** for the internship report. Screenshots were captured at the **delete confirmation** step; **Cancel** was clicked—no resources were actually deleted.

## Workflow for each resource

1. Navigate to the AWS console resource.
2. Choose **Delete** / **Terminate** / **Empty**.
3. Screenshot the confirmation dialog showing resource names.
4. Click **Cancel** (do not confirm deletion).

![Cleaning up resources](/images/5-Workshop/image39.png)

## Teardown order (recommended)

Delete dependencies before foundations:

### 1. CodeDeploy

![Delete CodeDeploy application](/images/5-Workshop/image40.png)

### 2. Auto Scaling Group

![Delete ASG](/images/5-Workshop/image41.png)

### 3. EC2 instances

![Delete EC2 instances](/images/5-Workshop/image42.png)

### 4. Launch template

![Delete launch template](/images/5-Workshop/image43.png)

### 5. API Gateway

![Delete API from API Gateway](/images/5-Workshop/image44.png)

### 6. Lambda functions

![Delete Lambda functions](/images/5-Workshop/image45.png)

### 7. DynamoDB tables

![Delete DynamoDB tables](/images/5-Workshop/image46.png)

### 8. S3 bucket

![Emptying S3 bucket](/images/5-Workshop/image47.png)

![Delete S3 bucket](/images/5-Workshop/image48.png)

### 9. VPC

![Delete VPC](/images/5-Workshop/image49.png)

### 10. IAM roles

Delete deploy roles, Lambda roles, and EC2 instance profile role after all dependent resources are removed.

![Delete IAM roles](/images/5-Workshop/delete-iam-roles.png)
