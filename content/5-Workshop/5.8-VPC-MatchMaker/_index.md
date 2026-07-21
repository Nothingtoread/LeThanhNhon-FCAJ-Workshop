---
title: "VPC MatchMaker"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

## Goal

Move **MatchMaker Lambda** into **private subnets** and reach DynamoDB + EC2 APIs via **VPC endpoints**—no NAT Gateway for control-plane traffic.

## VPC

Default VPC `vpc-09a82bd7e81714079` (`172.31.0.0/16`) in `ap-southeast-1`.

![VPC overview](/images/5-Workshop/5.8-VPC-MatchMaker/vpc.png)

## Subnets

Private subnets for MatchMaker Lambda across two AZs, plus existing public subnets for the game server ASG.

![Subnet list](/images/5-Workshop/5.8-VPC-MatchMaker/subnets.png)

### FightingGame-Private-1a

`172.31.48.0/24` in `ap-southeast-1a` — associated with **`FightingGame-Private-RT`** (local route + DynamoDB gateway endpoint prefix list).

![FightingGame-Private-1a route table](/images/5-Workshop/5.8-VPC-MatchMaker/subnet-private-1a.png)

### FightingGame-Private-1b

`172.31.49.0/24` in `ap-southeast-1b` — same private route table `FightingGame-Private-RT`.

![FightingGame-Private-1b](/images/5-Workshop/5.8-VPC-MatchMaker/subnet-private-1b.png)

## Security groups

![Security groups overview](/images/5-Workshop/5.8-VPC-MatchMaker/security-groups.png)

### FightingGameMatchmakerSG

MatchMaker Lambda ENIs in private subnets (`sg-0542a9acf546e761e`).

![FightingGameMatchmakerSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-matchmaker-sg.png)

### FightingGameServerSG

Game server — SSH (admin IP) and TCP **9000** for WebSocket gameplay (`sg-096a41cd239e4254a`).

![FightingGameServerSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-server-sg.png)

### FightingGameVpceSG

Interface VPC endpoints — inbound **HTTPS 443** from MatchMaker SG (`sg-0579918ab952df884`).

![FightingGameVpceSG](/images/5-Workshop/5.8-VPC-MatchMaker/fighting-game-vpce-sg.png)

## VPC endpoints

| Endpoint | Type | Service |
|----------|------|---------|
| FightingGame-DDB-Gateway | Gateway | `com.amazonaws.ap-southeast-1.dynamodb` |
| FightingGame-EC2-Interface | Interface | `com.amazonaws.ap-southeast-1.ec2` |
| FightingGame-Logs-Interface | Interface | `com.amazonaws.ap-southeast-1.logs` |

![VPC endpoints](/images/5-Workshop/5.8-VPC-MatchMaker/vpc-endpoints.png)
