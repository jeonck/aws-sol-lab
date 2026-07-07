---
title: "Tooling Baseline"
weight: 3
---

The labs assume a small, boring toolchain. Install these once and every lab's commands will paste and run.

## Required tools

| Tool | Purpose | Verify with |
|---|---|---|
| AWS CLI v2 | Every lab step | `aws --version` |
| Session Manager plugin | Shell into EC2 without SSH keys or open port 22 | `session-manager-plugin` |
| jq | Parse JSON output in verification steps | `jq --version` |

### AWS CLI v2

Installed in [Account Setup](account-setup). Confirm you are on v2 — v1 lacks SSO support and some output modes the labs use:

```bash
aws --version
```

### Session Manager plugin

Several labs connect to EC2 instances through SSM Session Manager instead of SSH — no key pairs, no bastion, no inbound security group rule. The CLI needs a plugin for this.

macOS:

```bash
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/mac/sessionmanager-bundle.zip" -o "sessionmanager-bundle.zip"
unzip sessionmanager-bundle.zip
sudo ./sessionmanager-bundle/install -i /usr/local/sessionmanagerplugin -b /usr/local/bin/session-manager-plugin
```

Linux (Debian/Ubuntu):

```bash
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
sudo dpkg -i session-manager-plugin.deb
```

Verify:

```bash
session-manager-plugin
# The Session Manager plugin was installed successfully. ...
```

### jq

Lab verification steps pipe CLI output through jq so you can check one field instead of scanning a JSON wall.

```bash
# macOS
brew install jq

# Debian/Ubuntu
sudo apt-get install -y jq
```

Quick check that both CLI and jq work together:

```bash
aws sts get-caller-identity | jq -r .Account
```

## Why the labs use the plain CLI, not IaC

In real work you would define most of what these labs build in **CloudFormation**, **Terraform**, or **CDK**:

- **CloudFormation** — AWS-native, declarative JSON/YAML, no extra tooling.
- **Terraform** — the multi-cloud industry standard, huge module ecosystem, most common in job postings.
- **CDK** — define infrastructure in TypeScript/Python, synthesizes to CloudFormation.

The labs deliberately use raw CLI commands instead, for one reason: **transparency**. When you run `aws ec2 create-nat-gateway` yourself, you learn that a NAT gateway is a resource with an allocation ID, a subnet, and a price — knowledge that `resource "aws_nat_gateway"` hides behind a one-liner. Interviewers probe exactly this layer.

{{< callout type="info" >}}
A strong portfolio move after finishing a lab: rebuild it in Terraform and put that repo on GitHub. You will have learned the resources by hand first, and the [Career Toolkit](../career) shows how to present the repo. IaC skill is a hiring signal; the labs give you the understanding underneath it.
{{< /callout >}}

## Region convention

All labs assume **us-east-1** (N. Virginia) unless a lab explicitly needs a second region (the DR failover lab uses us-west-2 as the recovery region).

Why us-east-1:

- Every service and instance type is available there first.
- The CloudWatch billing metric only exists in us-east-1.
- Consistency — copy-pasted commands and console screenshots match.

Set it as your default so you never create resources in a region you forget to check:

```bash
aws configure set region us-east-1
aws configure get region
```

{{< callout type="warning" >}}
Orphaned resources in a region you never look at are the classic source of surprise bills. If you ever suspect you created something elsewhere, check the **EC2 Global View** in the console, or loop over regions with the CLI during cleanup.
{{< /callout >}}

## Tagging convention

Every resource you create in a lab gets the same project tag, plus a per-lab tag:

| Key | Value | Purpose |
|---|---|---|
| `Project` | `aws-sol-lab` | One filter that finds *everything* the labs created |
| `Lab` | e.g. `lab-01` | Scope teardown and cost to a single lab |

Most `create-*` commands accept `--tag-specifications` or `--tags`; lab instructions include them. The payoff comes in two places:

**Cleanup** — find anything that survived a teardown:

```bash
aws resourcegroupstaggingapi get-resources \
  --tag-filters Key=Project,Values=aws-sol-lab \
  --query 'ResourceTagMappingList[].ResourceARN' \
  --output table
```

An empty table after teardown means you are done. A non-empty table is a to-do list.

**Cost tracking** — activate `Project` as a cost allocation tag (**Billing → Cost allocation tags**, takes up to 24 hours to appear), then group by it in Cost Explorer to see precisely what your lab work costs.

## Done when

- `aws --version` shows v2, `session-manager-plugin` responds, `jq --version` responds.
- Default region is us-east-1.
- `Project` is activated as a cost allocation tag.

Setup complete. Pick an architecture in [Core Architecture Styles](../architectures) and start building.
