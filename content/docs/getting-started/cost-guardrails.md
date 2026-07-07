---
title: "Cost Guardrails"
weight: 2
---

Set up billing protection **before** you create your first resource, not after your first surprise bill. Every horror story about a $2,000 AWS bill from a learning account has the same root cause: something was left running and nothing was configured to say so.

The guardrails on this page do not prevent spend — AWS Budgets alerts you, it does not stop resources. Your real protection is the combination of alerts plus the **teardown habit**.

{{< callout type="warning" >}}
Budgets alert, they do not block. A budget email at 80% of $10 means "go look now", not "AWS handled it". The teardown section of every lab on this site is as mandatory as the build section.
{{< /callout >}}

## Create a budget with an email alert

The fastest path is the console (**Billing and Cost Management → Budgets → Create budget**, use the "Monthly cost budget" template with a $10 limit). But since the labs are CLI-first, here is the same thing as a CLI call.

Save the budget definition:

```json
// budget.json
{
    "BudgetName": "lab-monthly-budget",
    "BudgetLimit": {
        "Amount": "10",
        "Unit": "USD"
    },
    "TimeUnit": "MONTHLY",
    "BudgetType": "COST"
}
```

Save the notification definition (alerts at 80% actual spend):

```json
// notifications.json
[
    {
        "Notification": {
            "NotificationType": "ACTUAL",
            "ComparisonOperator": "GREATER_THAN",
            "Threshold": 80,
            "ThresholdType": "PERCENTAGE"
        },
        "Subscribers": [
            {
                "SubscriptionType": "EMAIL",
                "Address": "you@example.com"
            }
        ]
    },
    {
        "Notification": {
            "NotificationType": "FORECASTED",
            "ComparisonOperator": "GREATER_THAN",
            "Threshold": 100,
            "ThresholdType": "PERCENTAGE"
        },
        "Subscribers": [
            {
                "SubscriptionType": "EMAIL",
                "Address": "you@example.com"
            }
        ]
    }
]
```

Create the budget (replace the account ID and email):

```bash
aws budgets create-budget \
  --account-id 123456789012 \
  --budget file://budget.json \
  --notifications-with-subscribers file://notifications.json
```

Verify:

```bash
aws budgets describe-budgets --account-id 123456789012
```

This gives you two triggers: an email when **actual** spend passes $8, and an email when **forecasted** month-end spend passes $10. For a lab account that should normally cost a few dollars a month, either email means "something is running that should not be".

## Enable billing alerts and CloudWatch billing alarms

Two supporting settings, both under **Billing and Cost Management → Billing preferences**:

1. Enable **Receive AWS Free Tier alerts** — AWS emails you when you approach a free tier limit.
2. Enable **Receive CloudWatch billing alerts** — this unlocks the `EstimatedCharges` metric in CloudWatch (us-east-1 only), which you can alarm on independently of Budgets if you want a second layer.

## Use Cost Explorer weekly

Enable **Cost Explorer** from the billing console (first activation takes up to 24 hours to populate). Make a habit of one check per week and after every lab session:

- Group by **Service** — is anything charging that you did not expect?
- Group by **Tag → Project** — this is why the [tagging convention](tooling#tagging-convention) matters; `Project=aws-sol-lab` lets you see exactly what the labs cost.
- Filter to the last 7 days with daily granularity — a flat non-zero daily line is the signature of a forgotten resource.

## The teardown habit

Every lab on this site ends with a teardown section. Treat it as part of the lab, not an appendix. Three rules:

1. **Tear down the same day you build.** Nothing on this site needs to run overnight. If you want to continue tomorrow, the build steps are repeatable — that repetition is also how the material sticks.
2. **Verify, do not assume.** After teardown, list resources by tag and confirm the list is empty. Deleting a CloudFormation-free lab by memory is how NAT gateways survive.
3. **Know your expensive suspects.** In these labs the resources that keep billing after you close the terminal are: NAT gateways (~$32/month each), RDS/Aurora instances, ALBs (~$16/month), Elastic IPs not attached to anything, and EC2 instances outside the free tier.

## Free tier: what it covers and where it bites

The free tier is genuinely useful for these labs, but it is three different programs and people conflate them:

| Type | Duration | Examples | Watch out for |
|---|---|---|---|
| **12 months free** | First 12 months after signup | 750 hrs/month t2.micro or t3.micro EC2, 750 hrs RDS db.t3.micro, 5 GB S3 standard | Hours are per month across *all* instances — two micro instances burn it in half a month |
| **Always free** | Forever | 1M Lambda requests/month, 25 GB DynamoDB, 10 CloudWatch custom metrics | Generous for serverless labs; easy to stay inside |
| **Free trials** | Fixed period per service | Some services offer 30–90 day trials | The clock starts when you first use the service, not when you signed up |

Things the free tier does **not** cover that appear in these labs: NAT gateways, ALBs beyond the 750-hour/15-LCU allowance, Multi-AZ RDS, ElastiCache beyond t-micro nodes, and inter-region data transfer for the DR lab. Each lab calls out its expected cost up front — most are under $1 if you tear down the same day, and the DR lab is the most expensive at a few dollars.

{{< callout type="info" >}}
Budget $10–20/month for working through this entire site with same-day teardowns. That is the cost of a portfolio; treat it as such. What you are protecting against is not the planned spend — it is the unplanned week of a forgotten Multi-AZ database.
{{< /callout >}}

## Done when

- `aws budgets describe-budgets` shows your budget with two notifications.
- Free tier alerts and CloudWatch billing alerts are enabled.
- Cost Explorer is activated.

Next: [Tooling Baseline](tooling).
