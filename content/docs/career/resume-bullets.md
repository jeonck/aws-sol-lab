---
title: "Resume Bullets"
weight: 2
---

A lab you cannot describe in one strong resume line might as well not have happened. This page gives you the formula, a good and bad example for each of the six labs, and the honesty rules that keep your bullets defensible under interview pressure.

## The formula

> **Action verb** + **what you built** + **named services** + **measurable outcome**

- **Action verb** — built, designed, deployed, automated, implemented, configured. Not "worked on", "helped with", "was exposed to".
- **What you built** — the architecture, not the tutorial. "A highly available three-tier web application", not "the Lab 01 exercise".
- **Named services** — recruiters and ATS software search for service names. "AWS" alone matches nothing; "ALB, EC2 Auto Scaling, RDS Multi-AZ" matches searches.
- **Measurable outcome** — a number you actually observed: failover time, request rate handled, cost, resource count. Labs produce real numbers if you [capture them before teardown](./#the-pipeline).

Where these bullets live: under a resume section called **Projects** or **Self-Directed AWS Lab Portfolio** — with a GitHub link — not interleaved with employment history.

## Good vs bad, per lab

| Lab | Bad bullet | Why it fails |
|---|---|---|
| 01 | "Learned about EC2 and load balancers by following a tutorial" | Passive verb, no services named searchably, no outcome, "tutorial" undersells real work |
| 02 | "Responsible for serverless technologies" | Job-description language for a project; says nothing you *did* |
| 03 | "Managed production container infrastructure on AWS" | Dishonest — implies production experience a lab does not give; collapses under follow-up |
| 04 | "Used SQS and SNS" | Two service names with no architecture, problem, or result |
| 05 | "Big data analytics with AWS" | Buzzword with no content |
| 06 | "Implemented enterprise disaster recovery for multi-region systems" | "Enterprise" implies scale and stakes that did not exist |

The same six labs, written to the formula:

| Lab | Good bullet |
|---|---|
| 01 | "Built a highly available three-tier web application in a personal AWS lab: ALB across two AZs, EC2 Auto Scaling group, and RDS MySQL Multi-AZ; verified automatic recovery by terminating instances and forcing a database failover" |
| 02 | "Designed and deployed a serverless REST API using API Gateway, Lambda, and DynamoDB with least-privilege IAM roles; load-tested to 1,000+ requests at a total cost under $0.01" |
| 03 | "Deployed two containerized microservices to ECS Fargate behind an ALB with path-based routing, images in ECR and inter-service discovery via Cloud Map, in a self-directed lab project" |
| 04 | "Implemented an event-driven order pipeline with EventBridge, SNS fan-out, and SQS queues including a dead-letter queue; demonstrated retry and failure isolation by injecting poison messages" |
| 05 | "Built an S3-based data lake with Glue-cataloged partitions queried through Athena, reducing scanned data per query by 90%+ via partitioning and columnar formats" |
| 06 | "Designed and executed a warm-standby DR failover between us-east-1 and us-west-2 using Route 53 health checks and Aurora cross-region replication, measuring an end-to-end RTO of under 15 minutes in a lab environment" |

Adjust every number to what *you* measured — the specific values above are illustrations, and an interviewer will ask where your numbers came from. That question should be one you want.

## Honesty rules

{{< callout type="warning" >}}
Every bullet must survive the follow-up question "tell me more about that". Write nothing you cannot expand on for five minutes. Interviewers do not penalize lab projects; they penalize discovering that "managed" meant "watched a tutorial".
{{< /callout >}}

1. **Label the context once, clearly.** Say "in a personal AWS lab", "self-directed project", or put the bullets under a Projects heading that says it. You do not need the disclaimer in every line — the section heading carries it — but the reader must never be able to *reasonably* conclude it was production work.
2. **Never imply scale you did not have.** "Highly available" is true — you built two AZs and tested failover. "High-traffic" or "enterprise" is not. Describe the architecture's properties, not imaginary users.
3. **Use verbs that match reality.** You *built*, *designed*, *deployed*, *tested* — all true. You did not *operate*, *maintain*, or *support* — those verbs imply time-in-service and on-call.
4. **Numbers must be measured, not decorated.** "RTO under 15 minutes" is defensible if you timed it. Never borrow impressive-sounding numbers from the lab writeup itself.
5. **Frame labs as an asset, not an apology.** A self-directed portfolio signals initiative, current skills, and the ability to learn without hand-holding. Present it with the same confidence as job experience — just labeled accurately.

## Workflow

1. Finish a lab and capture evidence (outputs, diagram, timing numbers) before teardown.
2. Same week, draft the bullet with the formula.
3. Apply the follow-up test: talk for two minutes about the bullet, out loud. If you stall, either trim the claim or redo the lab.
4. Store all bullets in one document; tailor which 3–4 appear per application based on the job description's service keywords.

Next: put the same material on your [LinkedIn profile](linkedin-profile), where the format and audience differ.
