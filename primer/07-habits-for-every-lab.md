# Six habits keep every lab cheap and easy to clean up

> **Your account, your responsibility.** Read the [notice](00-read-this-first.md#before-you-start-your-account-your-responsibility) before you follow any step.

Most surprise costs in a lab account come from something you forgot, not from something you did wrong. Six habits, repeated in every lab, make sure you can find everything you created, delete all of it, and see the result the next day. Each lab in our guides then tells you exactly what to tag, find and delete.

**Who this page is for:** you have worked through pages 01 to 06 and are about to start your first lab. No prior AWS experience assumed.

**Before you start:** these habits rely on the guardrails from earlier pages. You should be signed in as your IAM admin user with MFA ([page 03](03-your-everyday-admin-identity.md)), not the root user, and your budgets and alerts should exist ([page 05](05-money-alarms.md)). If you skipped those pages, go back first. The habits catch most leftovers; the alarms catch what the habits miss.

## The six habits follow the life of a lab

| When | Habit | What it protects you from |
|---|---|---|
| While you build | 1. Tag everything you create | Losing track of what belongs to the lab |
| At the end of the lab | 2. Find what you made, in every Region | Resources hiding in a Region you aren't looking at |
| At the end of the lab | 3. Delete, don't just stop | Parts that keep costing after you "turn things off" |
| The next day | 4. Check costs and credits again | Trusting numbers that are still a day old |
| Every lab | 5. Write the cleanup down | Relying on memory when you are tired or interrupted |
| Every session | 6. Sign out, and keep AWS in its own browser profile | Someone else using your open session |

Notice that half the habits happen *after* the interesting part of the lab. That is where beginners lose money.

## Key terms (skip if you know them)

- **Resource**: something you create in AWS that exists on its own, such as a virtual server (an EC2 instance), a disk (an EBS volume) or a storage bucket (an S3 bucket). Many resources are charged for as long as they exist, whether you use them or not.
- **Tag**: a label you attach to a resource, made of a **key** and a **value**, such as `lab` = `07`. Not the everyday "price tag": an AWS tag carries no price and costs nothing.
- **Region**: a geographic area where AWS runs its data centers, such as US East (N. Virginia). Most resources live in one Region, and most console pages show only the Region chosen in the Region selector at the top right.
- **Leftover**: our word for a resource that still exists, and still costs, after a lab has ended.
- **Credits**: on the Free plan, AWS pays for your usage from a credit balance instead of billing you. When the credits run out, the Free plan ends ([page 09](09-leaving-cleanly.md)).

## Habit 1: tag everything you create

**Do:** give everything a lab creates the same two tags: one that names the guide and one that names the lab. For example, `guide` = `clf` and `lab` = `07` for lab 7 of a Cloud Practitioner guide. Many console pages that create a resource have a section for tags; look for it before you choose the final create button. Each lab tells you which tags to use.

**Don't:** rely on remembering what you made, or on names alone. A tag lets a search tool list every resource with that label, across Regions, in one search.

**Why:** a tag turns cleanup into a search instead of a memory test. Later, the same tags can show which lab used which part of your credits.

**What it costs:** $0 (as of 2026-10-23).

**Well-Architected:** Cost optimization · [COST03-BP02 Add organization information to cost and usage](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_monitor_usage_org_information.html); Cost optimization · [COST04-BP01 Track resources over their lifetime](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_decomissioning_resources_track.html)

> **Your turn:** you are about to create a storage bucket for lab 3 of a guide whose short name is `sec`. Write down the two tags you would add.
>
> <details><summary>Feedback</summary>
>
> `guide` = `sec` and `lab` = `03`. Any consistent keys work, as long as you use the same ones for every resource in every lab, so that one search finds them all.
>
> </details>

## Habit 2: find what you made, in every Region

At the end of a lab, list what exists before you delete anything. You can't delete what you can't see, and a resource in another Region is invisible on a console page that shows only your lab Region. Three free places help (as of 2026-10-23):

- **AWS Resource Explorer** searches the resources in your account by name, type or tag. AWS says it has been on by default in accounts since 6 October 2025. In our new test account it worked with no setup ([page 06](06-safe-defaults.md) had you open it). It may not search every Region at first, so check which Regions its results cover before you trust an empty result.
- **Tag Editor** finds resources by type and tag across the Regions you pick. It starts with only your current Region selected, so choose all Regions before you search.
- **Billing and Cost Management** shows what is costing money. On the **Bills** page, look for the view that breaks charges down by service (AWS's help page calls this tab **Charges by service**); expand a service to see the Regions where it charged. **Cost Explorer** can also group costs by service and by Region. Both run about a day behind (habit 4).

**What you'll see the first time:** Resource Explorer lists things you didn't create. In our test account on 2026-10-23 it showed the parts of the **default VPC**, the ready-made network AWS creates in every Region ([page 06](06-safe-defaults.md)); a few IAM roles that AWS creates for its own services (*service-linked roles*); and the guardrails you built on pages 03 to 06, such as your IAM user, budgets, billing alarm and access analyzer.

**Don't:** delete something just because it appears in the list. The default VPC and the service-linked roles belong to the account, and your guardrails must stay. Delete only what carries your lab's tags or what the lab's cleanup list names.

**What it costs:** $0 to search (as of 2026-10-23).

**Well-Architected:** Cost optimization · [COST04-BP01 Track resources over their lifetime](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_decomissioning_resources_track.html)

> **Your turn:** you search Tag Editor for `lab` = `05` and find nothing, yet your zero-spend budget sent an alert after lab 5. Give two reasons the search could have missed the resource.
>
> <details><summary>Feedback</summary>
>
> First, Tag Editor may have searched only your current Region; the resource could be in another one. Second, the resource may never have been tagged, so a tag search can't find it. In both cases, the Bills page or Cost Explorer, grouped by service and Region, tells you where to look, a day later.
>
> </details>

## Habit 3: delete, don't just stop

Stopping a resource pauses part of its cost; deleting it ends the cost. At the end of a lab, delete everything the lab created, unless the lab tells you to keep it. For an EC2 instance, AWS calls deleting **terminating**.

These leftovers keep costing after beginners think they have cleaned up:

| Leftover | Why it keeps costing | What to do |
|---|---|---|
| A **stopped** EC2 instance | You stop paying for server time, but its disk is still stored and charged. | Terminate the instance. |
| An EBS volume (a disk) left behind | Most instances delete their disks when terminated, but an instance can be set to keep them. | Check the volumes list in the EC2 console and delete what the lab made. |
| An EBS snapshot (a saved copy of a disk) | Snapshots are charged on their own, separately from the disk they came from. | Delete the snapshots the lab made. |
| An Elastic IP address (a fixed public internet address) | It is charged even when it isn't attached to anything. | Release it. |
| A public IPv4 address on a resource | AWS charges for each public IPv4 address by the hour: $0.005 per hour as of 2026-10-23, with no free allowance we could find. On the Free plan, credits pay. | Delete the resource that holds it. |
| An S3 bucket with old versions or unfinished uploads | You can't delete a bucket until every object, every older version and every delete marker is gone. Uploads that stopped partway are still stored. | Empty the bucket, then delete it. |
| A database's retained automated backups (Amazon RDS) | They can stay, and keep costing, after the database is deleted. | Delete them as well. |
| Anything in a Region you have turned off | Turning a Region off doesn't delete what is in it; charges continue. | Turn the Region back on, delete, then turn it off again. |

Delete each resource through the service that created it. Some services start other resources for you, and if you delete only the underlying resource, the service may treat that as a failure and start a new one.

**Don't:** stop an instance "to save money" and walk away. **Don't:** delete your guardrails (budgets, alarms, the access analyzer) during cleanup.

**Why:** on the Paid plan, every leftover adds to your bill. On the Free plan you won't be billed, but every leftover spends your credits, and when the credits run out the Free plan ends and the account closes ([page 09](09-leaving-cleanly.md)). A resource nobody uses also wastes power and hardware, which is why the framework's sustainability pillar asks for the same habit.

**What it costs:** deleting is free. What you save depends on the resource.

**Well-Architected:** Cost optimization · [COST04-BP03 Decommission resources](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_decomissioning_resources_decommission.html); Cost optimization · [COST04-BP05 Enforce data retention policies](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_decomissioning_resources_data_retention.html); Sustainability · [SUS02-BP03 Stop the creation and maintenance of unused assets](https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/sus_sus_user_a4.html); Sustainability · [SUS04-BP05 Remove unneeded or redundant data](https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/sus_sus_data_a6.html)

> **Your turn:** a friend says, "I stopped my instance, so it's free now." In two sentences, explain what is still costing and what they should do instead.
>
> <details><summary>Feedback</summary>
>
> A stopped instance still has its disk (EBS volume), which is stored and charged, and any Elastic IP address attached to it is charged too. If they don't need the instance any more, they should terminate it, then check that its volumes, snapshots and Elastic IP addresses are gone.
>
> </details>

## Habit 4: check again the next day

AWS's cost data runs about a day behind, so the real proof that cleanup worked comes the next day. AWS says the Billing console takes about 24 hours to update charges. In our new account, Cost Explorer still said "Please check back in 24 hours" 13 hours after sign-up, and the Credits page said its estimated amounts update about every 24 hours (both on 2026-10-24).

**Do:** the day after each lab, sign in and look at three things:

1. The **Credits** page in the Billing console. On the Free plan your bill stays at $0 because credits pay for usage, so a falling credit balance is the sign that something is running.
2. The **Bills** page or **Cost Explorer**, by service and Region. Look for any service the lab used that is still adding cost.
3. Your **budgets**. Check whether any alert went off.

**Don't:** take a quiet dashboard on the day of the lab as proof that nothing is running.

**Why:** a leftover you catch on day 2 costs one day. A leftover you catch at the end of the month costs a month.

**What it costs:** $0.

**Well-Architected:** Cost optimization · [COST01-BP06 Monitor cost proactively](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_cloud_financial_management_proactive_process.html)

## Habit 5: write the cleanup down

**Do:** keep a short lab log. For each lab, write the date, the Region, the tags, and each resource you created. Tick each one off as you delete it. Every Automate the Cloud lab ends with a cleanup checklist; follow it in order, because some resources must go before others. For example, a bucket must be empty before you can delete it.

**Why:** written steps work when you are tired, interrupted, or coming back a week later; memory doesn't. Professionals call a written, step-by-step procedure a **runbook**.

**What it costs:** $0.

**Well-Architected:** Operational excellence · [OPS07-BP03 Use runbooks to perform procedures](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_ready_to_support_use_runbooks.html)

## Habit 6: sign out, and keep AWS in its own browser profile

**Do:** create a separate profile in your web browser that you use only for AWS. When you finish a session, sign out of the console. This is our advice; AWS doesn't publish it as a rule.

**Don't:** leave a console session open on a shared or unlocked computer.

**Why:** an open console session lets anyone at the keyboard act as you, with no password or MFA needed. A separate profile keeps your AWS sign-in away from everyday browsing and from browser add-ons you installed for other things. It also makes it obvious when you are working in AWS.

**What it costs:** $0.

**Well-Architected:** no single best practice covers this; it supports the security pillar's design principle "[Implement a strong identity foundation](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-design.html)".

## Summary

- **Tag** everything a lab creates with the guide and the lab, so one search finds it all.
- **Find** what you made in every Region, with Tag Editor set to all Regions, Resource Explorer, and the billing pages. Leave the default VPC, AWS's own roles and your guardrails alone.
- **Delete, don't stop.** Stopped instances, disks, snapshots, Elastic IP addresses, bucket versions and retained backups keep costing.
- **Check the next day**, because cost data runs about a day behind. On the Free plan, watch the credit balance.
- **Write the cleanup down** and follow each lab's checklist in order.
- **Sign out**, and use a browser profile just for AWS.

## Check yourself

**1.** You finished a lab yesterday afternoon. Which is the best evidence that your cleanup worked?

- A. Right after you terminated it, the EC2 console in your lab Region showed no running instances.
- B. Tag Editor, searching all Regions, finds nothing with the lab's tag, and today the Credits page and Cost Explorer show no new cost from the lab's services.
- C. You stopped every instance the lab created.
- D. Your budgets showed no alert a few minutes after cleanup.

<details><summary>Feedback</summary>

- **A** is incomplete. It shows only instances, only in one Region, and not disks, snapshots or addresses.
- **B** is correct. It checks every Region by tag and then confirms with cost data that has had a day to catch up.
- **C** is wrong. Stopped instances keep their disks, which are still charged.
- **D** is weak evidence. Budgets work from billing data that runs hours to a day behind, so a quiet budget minutes after cleanup proves little.

</details>

**2.** Which of these keeps costing even when it isn't attached to anything?

- A. A tag
- B. An Elastic IP address
- C. A search in Resource Explorer
- D. A lab log

<details><summary>Feedback</summary>

- **A** is wrong. Tags are free.
- **B** is correct. AWS charges for an Elastic IP address even when it isn't attached to a resource. Release it when the lab ends.
- **C** is wrong. Searching is free (as of 2026-10-23).
- **D** is wrong. A lab log is your own notes and costs nothing.

</details>

**3.** On the Free plan you can't be billed. Explain why leftovers still matter.

<details><summary>Feedback</summary>

Model answer: on the Free plan, leftovers spend your credits instead of your money. When the credits run out, the Free plan ends early and the account closes, so you lose access to your work and your lab account. Leftovers also hide real problems: if credits are falling anyway, you can't tell a forgotten disk from something you didn't create.

</details>

## Where to check the current details

All checked 2026-10-23.

- [What is AWS Resource Explorer?](https://docs.aws.amazon.com/resource-explorer/latest/userguide/welcome.html), AWS Resource Explorer User Guide
- [Finding resources to tag](https://docs.aws.amazon.com/tag-editor/latest/userguide/find-resources-to-tag.html), Tagging AWS Resources and Tag Editor
- [Best Practices for Tagging AWS Resources](https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html), AWS whitepaper
- [Terminate active AWS resources that you no longer need](https://repost.aws/knowledge-center/terminate-resources-account-closure), AWS re:Post Knowledge Center
- [Understanding unexpected charges](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html), AWS Billing User Guide
- [Terminate Amazon EC2 instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html), Amazon EC2 User Guide
- [Emptying a general purpose bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/empty-bucket.html), Amazon S3 User Guide
- [Amazon VPC pricing](https://aws.amazon.com/vpc/pricing/) (public IPv4 addresses)
- [Cost Optimization Pillar](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/cost-optimization-pillar/wellarchitected-cost-optimization-pillar.pdf), AWS Well-Architected Framework

---

"Six habits keep every lab cheap and easy to clean up" by Automate the Cloud Inc., licensed under CC BY-NC 4.0 with the Additional Permission for Internal Training from Automate the Cloud Inc.
License: https://creativecommons.org/licenses/by-nc/4.0/
Permission: https://automatethe.cloud/licenses/atc-internal-training-permission.txt
