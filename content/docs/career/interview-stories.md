---
title: "Interview Stories"
weight: 4
---

Resume bullets get you into the room; stories get you through it. Lab work converts into two interview assets: **STAR-format stories** for behavioral and hybrid questions, and **whiteboard fluency** for design questions. Both are prepared, not improvised.

## STAR, adapted for lab projects

| Element | What it means | Lab-project adaptation |
|---|---|---|
| **Situation** | The context | What you set out to learn and why — self-directed framing, stated plainly |
| **Task** | Your specific goal | The concrete target: architecture, constraint, success criterion |
| **Action** | What *you* did | The build, the decisions, and especially the things that went wrong |
| **Result** | Measurable outcome | What you measured, what you learned, what you would do differently |

For lab stories, the strongest material is almost always in **Action**, at the moments things broke. "I followed the steps and it worked" is not a story. "Failover didn't happen and here is how I found out why" is.

## Worked example: the DR failover lab

Question: *"Tell me about a challenging technical project you worked on."*

> **Situation** — "I've been building a portfolio of AWS architectures as self-directed projects, and disaster recovery was the area where I had the least practical intuition — I understood RTO and RPO on paper but had never actually failed anything over."
>
> **Task** — "I set out to build a warm-standby architecture across two regions — primary in us-east-1, scaled-down standby in us-west-2 — and to actually execute a failover and measure the real RTO, not just diagram it."
>
> **Action** — "I built the stack in both regions with Aurora cross-region replication for data and Route 53 health checks with failover routing for traffic. The interesting part was the failover test. When I simulated the primary failure, DNS failed over quickly, but my measured RTO was much worse than expected — clients kept hitting the dead region. I dug in and found two issues: my health check interval and threshold were too conservative, and I'd left a high TTL on the record, so resolvers cached the old answer. I tuned the health check, dropped the TTL, promoted the Aurora replica, and re-ran the whole exercise from scratch."
>
> **Result** — "Second run, end-to-end RTO came in under 15 minutes, and I could account for every minute of it — detection, DNS propagation, replica promotion. The bigger lesson was that DR is a rehearsal problem, not an architecture problem: the design was right the first time, but the untested parameters would have sunk a real failover. If I ran it again I'd script the whole failover so it's a runbook, not a memory."

Why this works: it is honest about being a lab, the failure is the centerpiece, the numbers are measured, and it ends with a judgment ("DR is a rehearsal problem") that sounds like an engineer, not a student.

## Story template

Build one story per lab, written down, using this skeleton:

```text
Question types it answers: [challenging project / failure / learning fast / ...]

Situation: I was building [architecture] as a self-directed lab project
           because [honest motivation].
Task:      The goal was [specific target with a success criterion].
Action:    I [built X with services Y]. The key decision was [trade-off].
           What went wrong: [the error]. I diagnosed it by [method] and
           fixed it by [fix].
Result:    [Measured outcome]. I learned [transferable lesson].
           Next time I would [improvement].
```

Aim for 90 seconds spoken. Rehearse out loud — twice is enough to stop it sounding memorized while keeping the structure.

## Hybrid questions to prepare for

AWS interviews mix behavioral and technical in single questions. Map each to a lab story before the interview:

| Question | Feed it with |
|---|---|
| "Tell me about a time you debugged a difficult problem" | Any lab error story — target group health checks, IAM denials, DNS caching |
| "Describe a technical decision where you weighed trade-offs" | Serverless vs containers for the same API ([Lab 02](../labs/lab-02-serverless-api) vs [Lab 03](../labs/lab-03-microservices-ecs)); warm standby vs pilot light ([Lab 06](../labs/lab-06-dr-failover)) |
| "Tell me about a time you had to learn something quickly" | The domain you were weakest in when you started its lab |
| "How do you make sure something you built actually works?" | The verification-and-teardown discipline: failover tests, load tests, tag-based cleanup audits |
| "Tell me about a failure" | The lab run that went wrong — with the diagnosis and the re-run |
| "How would you design X? Have you built anything like it?" | The whiteboard section below, plus "yes — in a lab, here is what I measured" |

That last question is where lab work pays off most: nearly every candidate can produce a design; very few can follow it with "and when I built this, the thing that surprised me was...".

## Whiteboarding the architectures

The [architecture pages](../architectures) on this site are your whiteboard curriculum. For each style you have built, practice drawing it from memory in under five minutes, in this order:

1. **Boundaries first** — region, VPC, AZs as boxes. Interviewers read structure from boundaries.
2. **Request path second** — user → DNS/CDN → load balancer → compute → data, left to right. Narrate as you draw.
3. **Supporting cast third** — security groups, IAM roles, monitoring, backups. Mentioning these unprompted is a seniority signal.
4. **Failure modes last, unprompted** — "if this AZ dies, the ALB stops routing there and Auto Scaling replaces capacity; if the primary DB dies, Multi-AZ promotes the standby". This is the step that separates candidates.

Then rehearse the standard probes per diagram: *where does this break under 10x load? what does this cost? what would you change for multi-region?* Your lab evidence answers the first two with measurements, and [Lab 06](../labs/lab-06-dr-failover) answers the third.

{{< callout type="info" >}}
Practice on a real whiteboard or paper, not a diagramming tool. Drawing while talking is a distinct physical skill, and the first time you do it should not be in the interview.
{{< /callout >}}

{{< callout type="warning" >}}
Never let a story drift into implying production stakes that did not exist. If an interviewer asks "how many users did this serve?", the answer is "it was a lab — the traffic was synthetic load I generated, and here is what it showed". Delivered without apology, that answer builds trust; delivered evasively, it ends the interview.
{{< /callout >}}

## Preparation checklist

- One written STAR story per completed lab, rehearsed out loud.
- Each hybrid question above mapped to a specific story.
- Each built architecture drawable from memory in under five minutes.
- Your measured numbers — RTO, request rates, costs — memorized, because they will be asked about.
