---
title: "VPC MatchMaker"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Mục tiêu

Đưa **MatchMaker Lambda** vào **private subnet**, gọi DynamoDB/EC2 qua **VPC endpoints** — không cần NAT Gateway cho traffic điều khiển.

## VPC

VPC mặc định `vpc-09a82bd7e81714079` (`172.31.0.0/16`) tại `ap-southeast-1`.

![Tổng quan VPC](/images/5-Workshop/5.8-VPC-MatchMaker/vpc.png)

## Subnet

Subnet private cho MatchMaker Lambda trên hai AZ; subnet public cho ASG game server.

![Danh sách subnet](/images/5-Workshop/5.8-VPC-MatchMaker/subnets.png)

### FightingGame-Private-1a

`172.31.48.0/24` tại `ap-southeast-1a` — route table **`FightingGame-Private-RT`** (local + prefix list DynamoDB gateway endpoint).

![Route table FightingGame-Private-1a](/images/5-Workshop/5.8-VPC-MatchMaker/subnet-private-1a.png)

### FightingGame-Private-1b

`172.31.49.0/24` tại `ap-southeast-1b` — cùng route table `FightingGame-Private-RT`.

![FightingGame-Private-1b](/images/5-Workshop/5.8-VPC-MatchMaker/subnet-private-1b.png)

## Security group

![Tổng quan security groups](/images/5-Workshop/5.8-VPC-MatchMaker/security-groups.png)

### FightingGameMatchmakerSG

ENI Lambda MatchMaker trong private subnet (`sg-0542a9acf546e761e`).

![FightingGameMatchmakerSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-matchmaker-sg.png)

### FightingGameServerSG

Game server — SSH (IP admin) và TCP **9000** cho WebSocket (`sg-096a41cd239e4254a`).

![FightingGameServerSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-server-sg.png)

### FightingGameVpceSG

Interface VPC endpoints — inbound **HTTPS 443** từ MatchMaker SG (`sg-0579918ab952df884`).

![FightingGameVpceSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-vpce-sg.png)

## VPC endpoints

| Endpoint | Loại | Service |
|----------|------|---------|
| FightingGame-DDB-Gateway | Gateway | `com.amazonaws.ap-southeast-1.dynamodb` |
| FightingGame-EC2-Interface | Interface | `com.amazonaws.ap-southeast-1.ec2` |
| FightingGame-Logs-Interface | Interface | `com.amazonaws.ap-southeast-1.logs` |

![VPC endpoints](/images/5-Workshop/5.8-VPC-MatchMaker/vpc-endpoints.png)
