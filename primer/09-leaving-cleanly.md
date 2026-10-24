# Leave your account cleanly, whether the Free plan ends or you close it yourself

> **Your account, your responsibility.** Read the [notice](00-read-this-first.md#before-you-start-your-account-your-responsibility) before you follow any step.

Every lab account ends in one of two ways: the Free plan runs out, or you close the account yourself. Either way the goal is the same: nothing you need is left inside, nothing is left running, and nothing surprises you later. This page explains what happens at the end of the Free plan, then gives one card for each way out.

## Unless you upgrade, your account closes when the Free plan ends

The Free plan ends 6 months after you sign up, or sooner if your credits run out (as of 2026-10-23). You wrote the end date down on [page 01](01-create-your-account.md); Console Home shows it in the **Cost and usage** box. Trust the date, not the count of days remaining, which didn't change from one day to the next in our account.

What happens then is clear in outline. On 2026-10-23, the sign-up page said: "After the 6 month free period or when all credits are used, you can choose to upgrade to a paid plan. Otherwise, your account closes automatically."

What happens *after* that is less clear, because AWS's own pages disagree on the details (as of 2026-10-23):

- **The word.** Most AWS pages say the account *closes*. AWS's Free Tier FAQ says AWS *suspends* it.
- **The 90 days.** Every AWS page that mentions it gives you 90 days to upgrade to the Paid plan and get your account back, after which AWS deletes the account and everything in it. But they disagree on when those 90 days start: when the plan ends, or when AWS notifies you that it has ended.
- **Getting your data out.** The FAQ says that to download your data after the plan ends, you first have to upgrade to the Paid plan.
- **Charges.** One general AWS billing page says that when free eligibility ends you pay standard rates. It seems to be written for the Paid plan, but it doesn't say so.

AWS changes these rules and pages often, and they don't always change together. So plan as if the end date is final: get out what you want and clean up before it, and don't count on the 90 days.

AWS says it emails you when 50, 25 and 10 percent of your credits remain, and 15, 7 and 2 days before the plan ends. We haven't yet been able to confirm these emails ourselves, so don't rely on them alone.

## Get ready for the end of the Free plan

**Use this when:** about two weeks before your end date, or as soon as your credits run low.

**Goal:** decide whether to let the account close or to upgrade, get out anything you want to keep, and leave nothing running.

1. **Check the date and the credits.** On Console Home, read the end date in the **Cost and usage** box. In the Billing console, open **Credits** to see what is left. Put the end date in your calendar if it isn't there already.
2. **Decide: let it close, or upgrade.** Upgrading moves you to the Paid plan for good; you can't go back to the Free plan. On the Paid plan, AWS bills you standard prices for anything your credits don't cover. If you upgrade yourself, AWS's FAQ says your remaining credits still apply to your bills until they expire, 12 months after sign-up (as of 2026-10-23). Upgrade only as a deliberate decision, never by clicking one of the many **Upgrade plan** buttons in passing.
3. **Copy out anything you want to keep.** Lab notes, code, and files in S3 buckets: download them to your own computer now. After the plan ends, you may have to upgrade and pay to get them back.
4. **Delete everything the labs created.** Use the habits on [page 07](07-habits-for-every-lab.md): find everything with Tag Editor across all Regions, delete it, and check the next day. If you plan to let the account close, this protects you if you ever change your mind and upgrade: nothing old starts costing again.
5. **If you upgrade, keep your guardrails.** Your budgets, billing alarm and alerts from [page 05](05-money-alarms.md) matter more on the Paid plan, because now the money is yours. Don't start free trials of paid services without a calendar reminder ([page 06](06-safe-defaults.md)).

**Confirm:** Tag Editor, searching all Regions, finds nothing with your lab tags. The next day, the credit balance on the Credits page is no longer falling. The end date is in your calendar.

**Well-Architected:** Cost optimization · COST04-BP02 Implement a decommissioning process

## Close your account early

**Use this when:** you have finished with AWS and don't want to wait for the Free plan to end.

**Before you start:** you need the root user's password and MFA device. An IAM user can't close the account.

1. **Copy out anything you want to keep.** After closing, you can sign in only to view past bills, change account settings, or contact AWS Support.
2. **Delete your resources first.** AWS doesn't require this, but if you reopen the account later, anything still in it starts costing again. Use [page 07](07-habits-for-every-lab.md). If you created a CloudTrail trail, delete it too: AWS says trails can keep delivering logs after an account closes unless you delete them.
3. **Decide about the email address and alias.** After you close the account, its root email address can't be used for any other AWS account, and neither can its account alias. If you want to reuse the address, change the root email to a different address before you close. If you want to reuse the alias, delete it first.
4. **Keep your MFA devices.** Closing doesn't remove MFA. For the next 90 days you may need to sign in, to view a bill or to reopen the account. Keep the root user's passkey and backup device until then.
5. **Close the account.** Sign in as the root user. Open the account page from the account menu at the top right, and look for the option to close the account (AWS's instructions call the button **Close account**). AWS asks you to type your account ID to confirm.

**Confirm:** within a few minutes, an email confirms that the account is closed. A final bill arrives early the next month for the part of the month you used; on the Free plan it should be $0. You can reopen the account within 90 days; after that AWS closes it for good, deletes what is left in it, and never reuses its account ID.

**Well-Architected:** Cost optimization · COST04-BP02 Implement a decommissioning process

## Check yourself

**1.** Your Free plan ends next week. You want to keep the files from your labs. When should you download them?

- A. Now, before the end date.
- B. Any time in the 90 days after the end date.
- C. After AWS emails you to say the plan has ended.
- D. You don't need to; AWS keeps Free plan data forever.

<details><summary>Feedback</summary>

- **A** is correct. Before the end date you can still reach your data at no cost.
- **B** is risky. AWS's pages disagree about when the 90 days start, and the FAQ says you would first have to upgrade to the Paid plan to get your data back.
- **C** is risky for the same reason, and AWS's emails may not reach you.
- **D** is wrong. After the 90 days, AWS deletes the account and everything in it.

</details>

**2.** You want to use the same email address for a new AWS account after you close this one. What must you do, and when?

<details><summary>Feedback</summary>

Model answer: before you close, change this account's root email address to a different address. AWS won't accept the email address of a closed account as the root email of another account, so once you have closed it, it is too late.

</details>

**3.** Why delete your resources before closing, if AWS says you don't have to?

<details><summary>Feedback</summary>

Model answer: if you reopen the account during the 90 days, anything still in it starts costing again. Deleting first also means the final bill covers only what you have already used, and any trail you created stops delivering logs.

</details>

## Where to check the current details

All checked 2026-10-23.

- [AWS Free Tier](https://aws.amazon.com/free/), including the current plan terms
- [AWS Free Tier FAQs](https://aws.amazon.com/free/free-tier-faqs/)
- [AWS Free Tier Terms](https://aws.amazon.com/free/terms/)
- [Choosing a plan](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-plans.html), AWS Billing User Guide
- [Tracking your AWS Free Tier usage](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/tracking-free-tier-usage.html), AWS Billing User Guide
- [AWS Free Tier update: New customers can get started and explore AWS with up to $200 in credits](https://aws.amazon.com/blogs/aws/aws-free-tier-update-new-customers-can-get-started-and-explore-aws-with-up-to-200-in-credits/), AWS News Blog, 15 July 2025
- [Close an AWS account](https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-closing.html), AWS Account Management Reference Guide
- [Understanding unexpected charges](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html), AWS Billing User Guide
- [Cost Optimization Pillar](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/cost-optimization-pillar/wellarchitected-cost-optimization-pillar.pdf), AWS Well-Architected Framework

---

"Leave your account cleanly, whether the Free plan ends or you close it yourself" by Automate the Cloud Inc., licensed under CC BY-NC 4.0 with the Additional Permission for Internal Training from Automate the Cloud Inc.
License: https://creativecommons.org/licenses/by-nc/4.0/
Permission: https://automatethe.cloud/licenses/atc-internal-training-permission.txt
