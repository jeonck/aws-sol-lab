---
title: "Account Setup"
weight: 1
---

A dedicated lab account, configured safely, is the foundation for everything on this site. This page covers root account hygiene, creating an administrative identity you will actually use day to day, and getting the AWS CLI working.

{{< callout type="info" >}}
Use a **separate AWS account** for labs if you can — not the account that runs anything you care about. A dedicated account makes teardown trivial ("is this resource mine? yes, delete it") and keeps experiments away from real workloads.
{{< /callout >}}

## Why you never use root for daily work

The root user — the identity created with the email address you signed up with — can do literally anything: close the account, change the payment method, delete every resource, and remove every other user. There is no permission boundary that applies to it.

That power is exactly why you should not use it. If root credentials leak (a saved browser session, a reused password, a phished login), the blast radius is total. AWS's own guidance is unambiguous: use root only for the handful of tasks that require it (initial setup, changing account settings, closing the account), and use an IAM or IAM Identity Center identity for everything else.

An admin *user* can be constrained, monitored via CloudTrail, given a permissions boundary, and deleted if compromised. Root cannot.

## Locking down the account

{{% steps %}}

### Secure the root user

1. Sign in as root and go to **Security credentials**.
2. Set a long, unique password stored in a password manager.
3. Enable **MFA** on the root user — a FIDO2 security key or an authenticator app. This is the single highest-value security action in this entire guide.
4. Confirm the root user has **no access keys**. If any exist, delete them. Root access keys are almost never needed and are a standing liability.
5. Verify the account contact email is one you control long-term and can receive billing alerts.

### Create an admin identity

You have two reasonable options for a lab account:

| Option | Best when | Notes |
|---|---|---|
| **IAM Identity Center** | You want the modern, recommended path | Short-lived credentials via `aws configure sso`; scales to multiple accounts later |
| **Plain IAM user** | You want the fastest possible setup | Long-lived access keys; acceptable for a throwaway lab account, rotate them |

**IAM Identity Center** (recommended): enable it from the console (it requires AWS Organizations, which the wizard sets up for you), create a user for yourself, create a permission set from the `AdministratorAccess` managed policy, and assign the user to your account. You then sign in through the access portal URL and get temporary credentials.

**Plain IAM user** (acceptable for labs): create an IAM user, attach the `AdministratorAccess` managed policy, enable MFA on it, and create one access key for CLI use.

Either way: from this point on, **sign in as this identity, not root**.

### Install AWS CLI v2

macOS:

```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

Linux (x86_64):

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Verify the version:

```bash
aws --version
# aws-cli/2.x.x Python/3.x.x ...
```

### Configure credentials

With IAM Identity Center:

```bash
aws configure sso
# Follow the prompts: SSO start URL, region, account, permission set.
# Give the profile a memorable name, e.g. "lab-admin".
aws sso login --profile lab-admin
```

With an IAM user access key:

```bash
aws configure
# AWS Access Key ID:     <your key>
# AWS Secret Access Key: <your secret>
# Default region name:   us-east-1
# Default output format: json
```

### Verify who you are

```bash
aws sts get-caller-identity
```

Expected output:

```json
{
    "UserId": "AIDAEXAMPLEID",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/lab-admin"
}
```

Check two things: the **Account** is your lab account, and the **Arn** is your admin identity — not `arn:aws:iam::123456789012:root`. If you see `root` in the ARN, stop and reconfigure.

{{% /steps %}}

{{< callout type="warning" >}}
If you ever see credentials in shell history, a Git repo, or a pasted terminal screenshot — treat them as leaked. Deactivate the access key immediately in the IAM console and create a new one. Attackers scan public repos for AWS keys within minutes.
{{< /callout >}}

## Done when

- Root user has MFA and no access keys, and you are signed out of it.
- You have an admin user (Identity Center or IAM) with MFA.
- `aws sts get-caller-identity` returns your admin identity from your lab account.

Next: set up [Cost Guardrails](cost-guardrails) before creating a single resource.
