---
title: "Getting Started"
weight: 1
---

Before you build anything on this site, spend one hour on setup. Every lab assumes three things are already in place: a safely configured AWS account, cost guardrails that alert you before a forgotten resource becomes an expensive lesson, and a small set of command-line tools.

This is not optional ceremony. The single most common way a hands-on learner gets hurt is skipping this section: running labs as the root user, with no budget alarm, and no consistent way to find and delete what they created.

{{< callout type="warning" >}}
Do not start any lab until you have a budget alert configured and you can run `aws sts get-caller-identity` as a non-root user. Both take under 30 minutes total.
{{< /callout >}}

## Setup checklist

| Step | Page | Time | Outcome |
|---|---|---|---|
| 1 | [Account Setup](account-setup) | ~30 min | Root account locked down, admin user with MFA, working CLI |
| 2 | [Cost Guardrails](cost-guardrails) | ~15 min | Budget with email alert, billing alerts enabled, teardown habit |
| 3 | [Tooling Baseline](tooling) | ~15 min | CLI plugins, jq, region and tagging conventions |

## Pages in this section

{{< cards >}}
  {{< card link="account-setup" title="Account Setup" icon="shield-check" subtitle="Root hygiene, MFA, an admin identity, and AWS CLI v2" >}}
  {{< card link="cost-guardrails" title="Cost Guardrails" icon="currency-dollar" subtitle="Budgets and alarms before you build anything" >}}
  {{< card link="tooling" title="Tooling Baseline" icon="terminal" subtitle="CLI plugins, jq, region and tagging conventions" >}}
{{< /cards >}}

Once all three pages are done, head to [Core Architecture Styles](../architectures) to pick your first pattern, then build it in the matching [lab](../labs).
