---
title: "Cleanup"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

After the capstone was deployed and demonstrated, I recorded how the fighting-game stack would be taken down in the correct dependency order. For each AWS resource, I opened the relevant console page and selected delete or terminate.

The screenshots below follow the sequence I used: application and compute layers first, then API and serverless components, storage, networking, and IAM roles last.

![Cleaning up resources](/images/5-Workshop/image39.png)

### CodeDeploy

![Delete CodeDeploy application](/images/5-Workshop/image40.png)

### Auto Scaling Group

![Delete ASG](/images/5-Workshop/image41.png)

### EC2 instances

![Delete EC2 instances](/images/5-Workshop/image42.png)

### Launch template

![Delete launch template](/images/5-Workshop/image43.png)

### API Gateway

![Delete API from API Gateway](/images/5-Workshop/image44.png)

### Lambda functions

![Delete Lambda functions](/images/5-Workshop/image45.png)

### DynamoDB tables

![Delete DynamoDB tables](/images/5-Workshop/image46.png)

### S3 bucket

![Emptying S3 bucket](/images/5-Workshop/image47.png)

![Delete S3 bucket](/images/5-Workshop/image48.png)

### VPC

![Delete VPC](/images/5-Workshop/image49.png)

### IAM roles

![Delete IAM roles](/images/5-Workshop/delete-iam-roles.png)
