---
title: "Hands-on Labs"
weight: 4
---

Labs are the heart of this site. Reading about architectures builds understanding; building them yourself creates **evidence** — screenshots, metrics, and working endpoints you can point to in interviews and on LinkedIn.

## Lab philosophy

Every lab follows the same four-phase loop:

1. **Build** — provision real resources with the AWS CLI, step by step, so you understand every moving part.
2. **Verify** — prove the system works with concrete checks: `curl` an endpoint, run a query, trigger a failover.
3. **Capture evidence** — screenshot the architecture, the console, and the verification output. This is your portfolio raw material.
4. **Teardown** — delete everything, in reverse order, and confirm nothing billable remains.

The teardown step is not optional. It is part of the skill: production engineers clean up after experiments, and your AWS bill will thank you.

{{< callout type="warning" >}}
**Labs cost real money.** Every lab lists an estimated cost assuming you tear down promptly. If you leave resources running — especially RDS instances, NAT gateways, and load balancers — costs accumulate hourly. Set up a budget alarm in [Getting Started](../getting-started/) before your first lab, and always finish a session with the Teardown section.
{{< /callout >}}

## Lab catalog

| Lab | Difficulty | Est. time | Est. cost | Key services |
|---|---|---|---|---|
| [Lab 1 — Three-Tier Web Application](lab-01-three-tier-web) | Intermediate | 2–3 h | $1–3 | VPC, ALB, EC2 Auto Scaling, RDS MySQL |
| [Lab 2 — Serverless REST API](lab-02-serverless-api) | Beginner | 1–1.5 h | < $0.25 | API Gateway, Lambda, DynamoDB, IAM |
| [Lab 3 — Microservices on ECS Fargate](lab-03-microservices-ecs) | Intermediate | 2–3 h | $1–2 | ECS Fargate, ECR, ALB, VPC |
| [Lab 4 — Event-Driven Pipeline](lab-04-event-driven) | Intermediate | 1.5–2 h | < $0.50 | S3, EventBridge, SQS, Lambda, DLQ |
| [Lab 5 — Mini Data Lake](lab-05-data-pipeline) | Beginner | 1–1.5 h | < $0.50 | S3, Glue, Athena |
| [Lab 6 — DR Failover with Route 53](lab-06-dr-failover) | Intermediate | 1.5–2 h | < $1.50 | S3 CRR, Route 53, CloudWatch |

Estimates assume the **us-east-1** region and prompt teardown. Times include reading, building, verifying, and tearing down.

## How to work through the labs

- **Do Lab 2 or Lab 5 first** if you are new to the CLI — they are the cheapest and most forgiving.
- **Pair each lab with its architecture page** in [Core Architecture Styles](../architectures/) — build the mental model before the resources.
- **One sitting per lab.** Half-built labs left overnight are how surprise bills happen.
- **After each lab**, visit the [Career Toolkit](../career/) to turn your evidence into a resume bullet while it is fresh.
