---
title: "Scenario Playbooks"
weight: 3
---

Real projects rarely start with "build me a three-tier architecture." They start with a business requirement: *"we cannot afford more than an hour of downtime"*, *"we need to connect our data center to AWS"*, *"our audit is in six months"*. Interviews are framed the same way — you are given a constraint and asked to design toward it.

Each playbook in this section starts from a realistic client requirement, breaks it down into technical requirements, and walks through a recommended design with trade-offs, pitfalls, and interview-ready phrasing.

{{< callout type="info" >}}
Pair each scenario with the matching [hands-on lab](../labs/) so you can back the design conversation with something you actually built.
{{< /callout >}}

## Scenario map

| Scenario | Business requirement | Key AWS services |
|---|---|---|
| [High Availability & DR](high-availability-dr) | "Survive a Region outage within our RTO/RPO" | Route 53, Aurora Global Database, S3 CRR, AWS Backup |
| [Hybrid Networking](hybrid-networking) | "Connect our data center to AWS reliably and privately" | Direct Connect, Site-to-Site VPN, Transit Gateway, Route 53 Resolver |
| [Migration to AWS](migration) | "Move 200 servers to AWS with minimal downtime" | MGN, DMS, Migration Hub, Control Tower |
| [Security & Compliance](security-compliance) | "Pass SOC 2 / HIPAA / ISMS-P audits on AWS" | IAM, GuardDuty, Security Hub, CloudTrail, KMS, WAF |
| [Cost Optimization](cost-optimization) | "Cut our AWS bill 30% without hurting reliability" | Savings Plans, Spot, Compute Optimizer, Cost Explorer, S3 lifecycle |
| [Global-Scale Applications](global-scale) | "Serve users on three continents with low latency" | CloudFront, Global Accelerator, Route 53, DynamoDB Global Tables |
| [CI/CD on AWS](cicd) | "Deploy daily with zero downtime and no stored credentials" | GitHub Actions OIDC, ECR, CodeDeploy, CodePipeline, CloudWatch |

## How to use these playbooks

1. **Read the scenario framing** and try to sketch a design yourself before reading the walkthrough.
2. **Study the options table** — interviewers care more about why you rejected alternatives than the final answer.
3. **Build the related lab** to turn the design into demonstrable experience.
4. **Practice the interview paragraph** out loud; it is written to be adapted into your own words.

## Playbooks

- [High Availability & Disaster Recovery](high-availability-dr) — RTO/RPO tiers from backup-and-restore to multi-site active-active.
- [Hybrid Networking](hybrid-networking) — VPN vs Direct Connect, Transit Gateway, and hybrid DNS.
- [Migration to AWS](migration) — the 7 Rs, wave planning, and cutover strategies.
- [Security & Compliance](security-compliance) — organization-wide guardrails and audit readiness.
- [Cost Optimization](cost-optimization) — commitment strategy, right-sizing, and a FinOps operating model.
- [Global-Scale Applications](global-scale) — edge delivery, multi-Region data, and residency constraints.
- [CI/CD on AWS](cicd) — pipelines with OIDC federation, blue/green deployments, and alarm-gated rollback.
