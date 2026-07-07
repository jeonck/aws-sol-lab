---
title: "LinkedIn Profile"
weight: 3
---

Recruiters find AWS candidates through LinkedIn keyword search before they ever see a resume. Your profile has one job: match the searches recruiters actually run, then convince the human who clicks through. This page covers both, using your lab portfolio as the substance.

## Headline

The headline is the highest-weighted searchable field and the first thing shown in search results. Do not waste it on "Aspiring Cloud Enthusiast".

Formulas that work:

| Formula | Example |
|---|---|
| Role + core stack | "Cloud Engineer \| AWS \| EC2, ECS, Lambda \| Terraform" |
| Role + certification + focus | "AWS Solutions Architect Associate \| Building HA and serverless architectures" |
| Transitioning + proof | "Systems Engineer moving to AWS \| 6-lab hands-on portfolio \| SAA certified" |

Rules: include the word **AWS** literally, include 2–4 service or tool names, state a role title recruiters search for (Cloud Engineer, DevOps Engineer, Solutions Architect). Certifications belong in the headline only while they are your strongest signal.

## About section

Structure: one paragraph of positioning, one of proof, one of direction. Template — replace the bracketed parts:

```text
I'm a [current role] building toward [target role], focused on designing
and deploying AWS architectures hands-on rather than only studying them.

Over the past [timeframe] I've built a portfolio of self-directed AWS
projects: a highly available three-tier web application (ALB, EC2 Auto
Scaling, RDS Multi-AZ), a serverless API (API Gateway, Lambda, DynamoDB),
containerized microservices on ECS Fargate, an event-driven pipeline
(EventBridge, SNS, SQS), an S3 data lake queried with Athena, and a
cross-region disaster recovery failover with a measured RTO. Each project
is documented with architecture diagrams and CLI-level build steps:
[GitHub link].

I'm looking for [target role] work where I can [one concrete sentence
about what you want to build/operate]. Certifications: [list].
```

Notes on the template: the service names in the middle paragraph are doing keyword work — LinkedIn search indexes the About section. Keep the honest "self-directed" framing; on LinkedIn, unlike a resume, you have room to say it naturally.

## Projects: where labs live

Add each completed lab under the **Projects** section of your profile (Add profile section → Recommended → Add projects). Per project:

- **Name** — the architecture, not the lab number: "Multi-Region DR Failover on AWS (warm standby)".
- **Description** — your [resume bullet](resume-bullets) plus 2–3 sentences of detail: the problem framing, key design decisions, what you measured.
- **Link** — the GitHub repo with your diagram, commands, and README. A repo link is the difference between a claim and evidence.
- **Skills** — attach the relevant skills so the project reinforces your Skills section.

{{< callout type="info" >}}
One well-documented GitHub repo per lab — README with the architecture diagram, the build commands, the verification output, and the teardown — is the single strongest artifact a self-taught candidate can attach. Recruiters may not read it, but the engineers who interview you will.
{{< /callout >}}

## Skills section keywords

Recruiters filter by the Skills field. Add up to 50; order the first three deliberately (they display on your profile card). Prioritize the terms that actually appear in AWS job searches:

| Tier | Skills |
|---|---|
| Always include | AWS, Amazon Web Services, EC2, S3, Lambda, IAM, VPC, RDS |
| Strong signals | ECS, DynamoDB, API Gateway, CloudWatch, CloudFormation, Terraform, Route 53, Auto Scaling |
| Role-dependent | EKS, Kubernetes, Docker, CI/CD, Python, Linux, Serverless Architecture, Disaster Recovery |

Include both "AWS" and "Amazon Web Services" — different recruiters search differently. List Terraform even at *aware* level only if you can discuss it; better, [rebuild one lab in Terraform](../getting-started/tooling#why-the-labs-use-the-plain-cli-not-iac) first, then list it honestly.

## Certifications

Add them under **Licenses & certifications** with the credential ID and the Credly verification link — recruiters do check. Ordering on your profile: certification section for the credential itself, headline while it is your strongest differentiator, and one mention in About. Do not scatter cert acronyms through every section; it reads as compensating.

Certifications and labs multiply each other: the cert proves breadth to the filter, the lab portfolio proves depth to the interviewer. Either alone is weaker.

## Example experience entry for lab work

If your lab portfolio is substantial and current employment is unrelated, you can list it as an experience entry — with truthful fields:

> **Self-Directed AWS Lab Portfolio** — Independent Project
> *Jan 2026 – Present*
>
> Designed, built, and tore down six AWS reference architectures using the AWS CLI, documenting each with diagrams and runbooks on GitHub.
>
> - Built a highly available three-tier web app (ALB, EC2 Auto Scaling across two AZs, RDS Multi-AZ) and verified instance and database failover
> - Executed a cross-region warm-standby DR failover (Route 53 health checks, Aurora replication) with a measured RTO under 15 minutes
> - Deployed serverless and container variants of the same API (Lambda + API Gateway; ECS Fargate) and compared cost and operational trade-offs
> - Enforced cost discipline with AWS Budgets, tagging, and same-day teardown, keeping total portfolio cost under $20

The employer field says "Independent Project" — never a made-up company name. The title says "Portfolio" or "Independent Study" — never "Cloud Engineer" at a company that does not exist.

{{< callout type="warning" >}}
Never fabricate an employer, inflate a title, or backdate lab work into an employment gap as if it were a job. Background checks surface employer claims, and the interview surfaces everything else. "Independent project, here is the repo" is a position of strength.
{{< /callout >}}

Next: prepare to talk about all of this live — [Interview Stories](interview-stories).
