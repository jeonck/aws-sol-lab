---
title: "Core Architecture Styles"
weight: 2
---

Every AWS solution you will design, defend in an interview, or put on a resume is a variation of a small set of canonical architecture styles. Master these six and you can reason about almost any workload: you will know which services belong together, where the failure modes hide, and which trade-offs a reviewer will probe.

Each page in this section follows the same structure — a definition, an architecture diagram, the core components, the design decisions that matter, Well-Architected notes, and interview questions — and links to a hands-on lab where you build it yourself.

{{< callout type="info" >}}
Read the style first, then build the matching lab. The combination of "I understand the trade-offs" and "I have deployed it" is what makes a portfolio entry credible.
{{< /callout >}}

## Choosing a style

| Style | Best for | Key services | Complexity |
|---|---|---|---|
| [Three-Tier Web](three-tier-web) | Traditional web apps, lift-and-shift, predictable traffic | ALB, EC2 Auto Scaling, RDS, ElastiCache, CloudFront | Low–Medium |
| [Serverless](serverless) | Spiky or unpredictable traffic, APIs, minimal ops overhead | API Gateway, Lambda, DynamoDB, Step Functions | Low–Medium |
| [Container Microservices](microservices) | Many independent teams and services, portability | ECS Fargate, EKS, ECR, ALB, Cloud Map | Medium–High |
| [Event-Driven](event-driven) | Decoupled workflows, async processing, integration | EventBridge, SNS, SQS, Kinesis | Medium |
| [Data & Analytics](data-analytics) | Data lakes, BI, batch and streaming analytics | S3, Glue, Athena, Redshift, Kinesis, QuickSight | Medium–High |
| [Multi-Account Landing Zone](multi-account) | Enterprise governance, security boundaries, scale-out of teams | Organizations, Control Tower, IAM Identity Center | High |

## How the styles relate

Real systems mix styles. A typical mature platform runs container microservices for the core product, serverless for glue and edge workloads, an event-driven backbone between domains, a data platform consuming those events, and everything deployed inside a multi-account landing zone. The three-tier pattern remains the baseline vocabulary — most interviewers start there.

## Pages in this section

{{< cards >}}
  {{< card link="three-tier-web" title="Three-Tier Web" icon="server" subtitle="ALB, Auto Scaling EC2, RDS Multi-AZ — the classic baseline" >}}
  {{< card link="serverless" title="Serverless" icon="lightning-bolt" subtitle="API Gateway, Lambda, DynamoDB — pay per request" >}}
  {{< card link="microservices" title="Container Microservices" icon="cube" subtitle="ECS Fargate vs EKS, service discovery, path routing" >}}
  {{< card link="event-driven" title="Event-Driven" icon="switch-horizontal" subtitle="EventBridge, SNS, SQS, fan-out, sagas" >}}
  {{< card link="data-analytics" title="Data & Analytics" icon="chart-bar" subtitle="S3 data lake, Glue, Athena, Redshift, streaming" >}}
  {{< card link="multi-account" title="Multi-Account Landing Zone" icon="office-building" subtitle="Organizations, Control Tower, SCPs, centralized logging" >}}
{{< /cards >}}
