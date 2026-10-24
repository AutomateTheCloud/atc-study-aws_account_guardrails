# Set up guardrails before you run any lab

A few free settings in a new AWS account stop most beginner mistakes from turning into a large bill or a security problem. This primer walks you through them, once, before your first lab in any Automate the Cloud guide.

## Before you start: your account, your responsibility

This primer is provided as is, without warranty. We work hard to keep it correct and current, but AWS changes often, and its services, prices, and free offers may differ from what is written here. The labs run in your own AWS account. You are responsible for that account, for its security, and for any charges it incurs, including charges from resources you forget to delete. Automate the Cloud Inc. is not liable for any costs, losses, or security incidents that result from following, or failing to follow, this material. Technical guidance here is general information, not advice about your specific systems.

## This primer is for people who are new to AWS

You have just created, or are about to create, your first AWS account. You want to run labs in it without surprise bills or security problems. You don't need any AWS or IT experience.

A **guardrail** here means a setting or habit that limits the damage a mistake can do. You set them up once, and every lab in every Automate the Cloud guide relies on them.

## Two things can go wrong: money and security

**Money.** You create something, forget it, and it keeps running. On a paid account, that becomes a bill. On a free account, it quietly uses up your free credits until the account closes.

**Security.** Someone gets your password or a secret key and runs things in your account. Whatever an attacker creates there costs money, so a security problem can quickly become a money problem too.

Every guardrail in this primer protects against one of these risks, or both.

## The AWS Well-Architected Framework explains the "why"

The **AWS Well-Architected Framework** is AWS's published guidance for building well in the cloud. It groups that guidance into six **pillars**: operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability. Each pillar has a few broad design principles and a numbered list of **best practices**, with IDs such as `SEC02-BP01`. AWS publishes a whitepaper for each pillar.

This primer uses only a few of those best practices. Each guardrail ends with a tag line like this one:

**Well-Architected:** Security · SEC02-BP01 Use strong sign-in mechanisms

Later guides use these tags to point back to what you set up here. Most guardrails serve security and cost optimization; later guides cover the other pillars. Where a guardrail doesn't match any best practice, the tag says so.

## Choose the advanced sign-up and the Free plan

Sign up through AWS's **advanced sign-up** link and choose the **Free plan**. [Page 01](01-create-your-account.md) walks you through every screen. Here is why.

### The Free plan can't bill you

During sign-up, AWS asks you to choose an **account plan** (terms as of 2026-10-23):

- **Free plan.** You get USD $100 in credits at sign-up, and you can earn up to $100 more by completing five short activities ($20 each). A **credit** is money AWS gives you to spend on AWS services. You aren't charged while you stay on this plan. The plan lasts up to 6 months, or until your credits run out, whichever comes first. Then the account closes unless you upgrade, and you lose access to what is in it. AWS's pages disagree on the details after that; [page 09](09-leaving-cleanly.md) explains.
- **Paid plan.** You get the same credits. When they run out, you pay normal prices for what you use. The account doesn't close, and you can use every AWS service; some, such as Amazon GuardDuty, are Paid plan only.

You can move from the Free plan to the Paid plan, but never back.

The Free plan is a guardrail in itself: a forgotten resource uses credits, not your money. Still, running out of credits closes the account, and you lose your work.

### Know what moves you to the Paid plan

**Do:** keep the account on the Free plan for the labs, unless a guide tells you otherwise.

**Don't:** do any of these on a Free plan account. AWS's Free plan guide says each one upgrades the account to the Paid plan automatically (as of 2026-10-23). For joining AWS Organizations, AWS's terms add that you can then no longer use or earn Free Tier credits; for the others, AWS doesn't say what happens to your credits, so assume the worst:

- join or create an organization in AWS Organizations, a service for managing many accounts together;
- set up an AWS Control Tower landing zone;
- turn on IAM Identity Center, AWS's service for central sign-in, in a way that creates an organization ([page 03](03-your-everyday-admin-identity.md) explains this one; the Identity Center page showed no warning when we checked on 2026-10-23);
- business steps a learner rarely meets: joining the AWS Partner Network, a Professional Services contract, an Enterprise Agreement, an AWS Skill Builder Team subscription, or marking the account as HIPAA or SEC compliant.

**Don't:** choose an **Upgrade plan** button unless you have decided to pay. These buttons appear all over the console without saying what upgrading means, and the upgrade can't be undone. (If you do upgrade on purpose, AWS's FAQ says your remaining credits still apply until they expire.)

**Don't:** put real or sensitive data in a Free plan account. AWS's terms say Free plan accounts shouldn't be used for sensitive data. Use made-up data in labs.

**What it costs:** $0. **Free plan:** this choice is what keeps you on it.

**Well-Architected:** Cost optimization · no single best practice covers this; it supports the design principle "Implement Cloud Financial Management". The upgrade triggers themselves are AWS account rules, not part of the framework.

### The new sign-up experience works differently

As of 2026-10-23, the "Create a free account" buttons on AWS's Free Tier page lead to a newer sign-up experience (launched 16 September 2026) that uses a login you already have, such as Google or GitHub. It has no **root user** (the all-powerful sign-in that the advanced sign-up creates). Its **IAM users**, the extra sign-ins you create inside an account, can't use the AWS console website. It also picks your **Region**, the part of the world where your resources run, for you. Only its Paid plan offers spend limits. Our guides are written for the advanced path, so [page 01](01-create-your-account.md) gives you that link directly.

## AWS is a moving target

AWS changes its services, prices, and free offers faster than it updates its own pages, so its pages sometimes disagree. For example, while we wrote this primer, AWS pages gave both 6 months and 12 months for how long the free offer lasts. We settled what we could by creating a real account and watching: the Free plan lasts 6 months, but the credits themselves showed an expiry date 12 months out. Both were true; they are two different clocks.

We work to be accurate. We date every number that can change, and we tell you when AWS's pages disagree. If a screen or price differs from what we wrote, trust the live AWS page. Each page ends with the AWS pages to check.

## How the primer is organized

Work through the pages in order. Pages 01 to 06 change your account. Pages 07 to 10 are habits and reference.

| Page | What it covers |
|---|---|
| [01 Create your account](01-create-your-account.md) | Sign up with the advanced link on the Free plan. |
| [02 Secure the root user](02-secure-the-root-user.md) | Protect the all-powerful sign-in with multi-factor authentication (MFA), then stop using it. |
| [03 Your everyday admin identity](03-your-everyday-admin-identity.md) | Create the sign-in you use every day, with MFA. |
| [04 The command line without access keys](04-command-line-without-access-keys.md) | Run AWS commands without creating long-lived secret keys. |
| [05 Money alarms before you build anything](05-money-alarms.md) | Get an email when something stops being free. |
| [06 Safe defaults](06-safe-defaults.md) | Switch on free settings that block public access and encrypt storage. |
| [07 Habits for every lab](07-habits-for-every-lab.md) | Label, find, delete, and check everything you create. |
| [08 When something goes wrong](08-when-something-goes-wrong.md) | Leaked keys, surprise bills, lost MFA devices. |
| [09 Leaving cleanly](09-leaving-cleanly.md) | The end of the Free plan, and closing an account. |
| [10 Bad practices and checklist at a glance](10-bad-practices-and-checklist.md) | A one-page reference. |

**How long it takes:** plan on roughly two to three hours for pages 01 to 06, in one sitting if you can. Some checks need the next day, because AWS's cost data takes up to 24 hours to appear. Everything in pages 01 to 06 is free on the Free plan.

## Check yourself

**1. Which of these moves a Free plan account to the Paid plan automatically?**

A. Creating a budget
B. Joining AWS Organizations
C. Creating an IAM user (a sign-in for daily work)
D. Opening AWS CloudShell, a command line in the browser

<details><summary>Feedback</summary>

**B is right.** Joining AWS Organizations is one of the automatic upgrade triggers, and AWS's terms say the credits can then no longer be used.

- **A is wrong.** Creating a budget is free on both plans, and it even earns a $20 credit as one of the sign-up activities (as of 2026-10-23).
- **C is wrong.** IAM users are free and don't change the plan. You create one on [page 03](03-your-everyday-admin-identity.md).
- **D is wrong.** CloudShell is available on both plans. You use it on [page 04](04-command-line-without-access-keys.md).

</details>

**2. Name the two risks this primer protects against, and give one example of each.**

<details><summary>Feedback</summary>

**Model answer:** Money: something you forgot keeps running and uses credits or, on the Paid plan, your money. Security: someone steals your password or a key and runs things in your account, which also costs money.

</details>

## Where to check the current details

- [AWS Free Tier](https://aws.amazon.com/free/) (checked 2026-10-23)
- [Free Tier FAQs](https://aws.amazon.com/free/free-tier-faqs/) (checked 2026-10-23)
- [AWS Free Tier Terms](https://aws.amazon.com/free/terms/) (checked 2026-10-23)
- [Choosing a plan](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-plans.html), AWS Billing User Guide (checked 2026-10-23)
- [Compare sign-up options](https://docs.aws.amazon.com/accounts/latest/reference/sign-up-for-aws.html), AWS Account Management Reference Guide (checked 2026-10-23)
- [The pillars of the framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html), AWS Well-Architected Framework (checked 2026-10-23)

---

"Set up guardrails before you run any lab" by Automate the Cloud Inc., licensed under CC BY-NC 4.0 with the Additional Permission for Internal Training from Automate the Cloud Inc.
License: https://creativecommons.org/licenses/by-nc/4.0/
Permission: https://automatethe.cloud/licenses/atc-internal-training-permission.txt
