---
title: "Skill Matrix"
weight: 1
---

Before you write a resume or answer "rate your AWS skills from 1 to 10", you need an honest inventory. A skill matrix does two jobs: it tells *you* where the gaps are, and it gives you calibrated language for interviews — "practiced with ECS, aware of EKS" lands far better than a vague "I know containers".

## Proficiency levels

Use three levels. Resist the temptation to invent a fourth level between practiced and production — that gray zone is where resume inflation lives.

| Level | Definition | You can honestly claim it when |
|---|---|---|
| **Aware** | You understand the concepts, trade-offs, and where the service fits | You have read the docs/architecture pages and can explain it to someone else |
| **Practiced** | You have built it yourself, end to end, at least once | You completed a lab, hit at least one real error, and can rebuild it without the instructions |
| **Production** | You have run it for real users, with the operational scar tissue that implies | You have been paged for it, sized it under real load, or owned it through an incident |

{{< callout type="warning" >}}
Completing every lab on this site gets a domain to **practiced**, never to **production**. Production means real traffic, real stakes, real on-call. Claiming it without that is the fastest way to fail a technical screen — interviewers probe production claims with operational questions ("what did you monitor?", "what broke?") that lab experience cannot answer.
{{< /callout >}}

## The matrix

Copy this into your own notes and fill in the **Your level** column honestly. The last column shows which labs on this site move that domain to *practiced*.

| Domain | Core services | Your level | Labs that demonstrate it |
|---|---|---|---|
| Compute | EC2, Auto Scaling, ALB | | [Lab 01](../labs/lab-01-three-tier-web) |
| Networking | VPC, subnets, NAT, Route 53, security groups | | [Lab 01](../labs/lab-01-three-tier-web), [Lab 06](../labs/lab-06-dr-failover) |
| Storage | S3, EBS, lifecycle policies, replication | | [Lab 05](../labs/lab-05-data-pipeline), [Lab 06](../labs/lab-06-dr-failover) |
| Databases | RDS, Aurora, DynamoDB | | [Lab 01](../labs/lab-01-three-tier-web), [Lab 02](../labs/lab-02-serverless-api), [Lab 06](../labs/lab-06-dr-failover) |
| Serverless | Lambda, API Gateway, Step Functions | | [Lab 02](../labs/lab-02-serverless-api), [Lab 04](../labs/lab-04-event-driven) |
| Containers | ECS Fargate, ECR, service discovery | | [Lab 03](../labs/lab-03-microservices-ecs) |
| Security | IAM, least privilege, KMS, security groups | | Every lab; IAM roles feature in [Lab 02](../labs/lab-02-serverless-api) and [Lab 03](../labs/lab-03-microservices-ecs) |
| Observability | CloudWatch metrics, logs, alarms, dashboards | | Verification steps of every lab, alarms in [Lab 01](../labs/lab-01-three-tier-web) and [Lab 06](../labs/lab-06-dr-failover) |
| Cost | Budgets, Cost Explorer, tagging, right-sizing | | [Cost Guardrails](../getting-started/cost-guardrails) plus per-lab cost tracking |
| IaC | CloudFormation, Terraform, CDK | | Not covered by the CLI-first labs — rebuild a lab in Terraform to claim *practiced* |

## How to self-assess honestly

Three tests, applied per domain:

1. **The rebuild test** — could you rebuild the lab from a blank account without the instructions? If not, you are still *aware*, not *practiced*. Rebuilding once from memory is the cheapest upgrade available.
2. **The follow-up test** — for each claim, imagine the obvious second question. "You built a three-tier architecture — why is the database subnet private?" If the follow-up scares you, mark yourself down a level and go re-read the [architecture page](../architectures).
3. **The error test** — *practiced* people have debugging stories ("my target group health checks failed because..."). If a lab went perfectly and you learned nothing from an error, run it again and break something on purpose.

## Using the matrix

- **Gap-driven learning** — sort by target-job relevance, not by what is fun. If your target roles all list containers and Terraform, [Lab 03](../labs/lab-03-microservices-ecs) plus a Terraform rebuild beats a third pass at serverless.
- **Resume calibration** — your resume's skills section should contain only *practiced* and *production* items. *Aware* items belong in conversation, not in writing.
- **Interview language** — state the level out loud: "I have production experience with EC2 and RDS from my current role, and practiced hands-on with ECS from self-directed lab work." This calibration reads as senior behavior.

Re-assess after every lab and every few months. The matrix is a living document; the first version exists to be embarrassing.

Next: turn *practiced* rows into [resume bullets](resume-bullets).
