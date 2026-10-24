---
id: guardrails-08
type: page
title: "When something goes wrong, work through the steps in order"
---

# When something goes wrong, work through the steps in order

> **Your account, your responsibility.** Read the [notice](00-read-this-first.md#before-you-start-your-account-your-responsibility) before you follow any step.

Three things go wrong most often in a lab account: a secret leaks, a charge appears that you didn't expect, or you lose an MFA device. Each card below gives the goal, the steps in order, and how to confirm you are done. Read them once now, so you know they exist, and come back when you need one.

AWS's help is free for all three. Every account can open account and billing cases with AWS Support at no charge, and AWS's security incident team helps with a suspected compromise whatever your Support plan (as of 2026-10-23).

## Lock down a leaked key or activity you didn't do

**Use this when:** an access key (a long-lived secret that lets programs act as you) appeared somewhere others can see it, such as a code repository, a chat or a screenshot; AWS emailed you about unusual activity; or you see users, resources or charges you didn't create. If you followed [page 04](04-command-line-without-access-keys.md), you have no access keys, but activity you didn't do can still happen if a password leaks.

**Goal:** stop the access, remove what someone else created, and get AWS's help.

**If at any point you are unsure, open the support case in step 6 first, then keep going while you wait.**

1. **Turn off the leaked key, then delete it.** Sign in as your IAM admin user, open IAM, open the user that owns the key, and find its access keys on the security credentials tab. Deactivate the key, then delete it. If the key belongs to the root user, sign in as root and do the same on the root user's security credentials page. A key whose ID starts with `AKIA` never expires on its own, so it works until you act.
2. **Look at what happened.** Open CloudTrail and choose **Event history**. It is free and keeps 90 days of account activity, Region by Region. Look for actions you didn't take, especially new users, new access keys, new roles and new policies. Check your lab Region and any Region where you see unfamiliar charges.
3. **Remove what you didn't create, in every Region.** Delete or deactivate IAM users, access keys, roles and policies you don't recognize. Then look for resources you didn't launch in every Region, including Regions you have never used: use Tag Editor with all Regions selected, and the Bills page by service and Region ([page 07](07-habits-for-every-lab.md)).
4. **Change your passwords and check MFA.** Change the root password and your IAM user's password. On each identity's security credentials page, check that every MFA device listed is one you own. Remove any that isn't.
5. **Check your account details.** Make sure the account name, the root email address, the primary contact and the alternate contacts are still the ones you set on [page 02](02-secure-the-root-user.md).
6. **Open a support case from the affected account.** Describe what you saw and what you have done. If AWS sent you a notice about the activity, reply to it in the Support Center with the steps you completed. AWS's security incident response team helps at no extra charge, whatever your Support plan (as of 2026-10-23).

**Confirm:** IAM lists no access keys or users you didn't create, and the IAM dashboard still says the root user has no active access keys. Event history shows nothing new that you don't recognize after your fix. The next day, the Credits page and the Bills page show no new cost from services you didn't use. AWS has answered your case.

**Well-Architected:** Security · [SEC10-BP02 Develop incident management plans](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_incident_response_develop_management_plans.html). This card is a small incident plan; the security pillar's design principle "[Prepare for security events](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-design.html)" asks you to have one before you need it.

## Track down an unexpected charge

**Use this when:** a budget or anomaly alert arrives, your credit balance falls faster than your labs explain, or a bill is higher than you expected.

**Goal:** find what is costing, stop it, and get AWS's help if you can't explain it.

1. **Find the service and the Region.** In the Billing and Cost Management console, open **Bills** and look for the breakdown by service (AWS's help page calls this tab **Charges by service**). Expand the service to see which Regions charged. Cost Explorer, grouped by service and then by Region, shows the same from another angle. Remember that this data runs about a day behind.
2. **Go to that Region and find the resource.** Switch the Region selector at the top right to the Region you found. Use Tag Editor or that service's console to find the resource.
3. **Delete it, and its companions.** Delete the resource through the service that created it. Then check for the parts that outlive it: disks, snapshots, Elastic IP addresses and retained database backups ([page 07](07-habits-for-every-lab.md), habit 3).
4. **If you can't find it or explain it, open a support case.** Choose the **account and billing** type. Every AWS account can open these cases free of charge. The free Basic Support plan can't open technical cases, but billing questions don't need one.

**Confirm:** the next day, the service's daily cost in Cost Explorer has stopped growing. On the Free plan, the credit balance has stopped falling faster than expected.

**Well-Architected:** Cost optimization · [COST01-BP06 Monitor cost proactively](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_cloud_financial_management_proactive_process.html); Cost optimization · [COST04-BP03 Decommission resources](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/cost_decomissioning_resources_decommission.html)

## Get back in after losing an MFA device

**Use this when:** the phone, security key or password manager that holds one of your MFA devices is lost, broken or reset.

**Goal:** sign in again, remove the lost device, and register a replacement, so you are back to two devices.

**If you still have your backup device** (this is why [page 02](02-secure-the-root-user.md) and [page 03](03-your-everyday-admin-identity.md) had you register two):

1. Sign in with the backup device.
2. On that identity's security credentials page, remove the lost device.
3. Register a replacement device. You can add one only while you are signed in with MFA, which you now are.

**If your IAM user has lost all of its MFA devices:**

1. Sign in as the root user, with the root user's MFA.
2. Open IAM, open your IAM user, and remove the lost devices from its security credentials tab.
3. Sign out. Sign in as your IAM user with its password, and register a new device right away.
4. Sign out and back in with the new device, then add a backup. Adding a second device fails until you have signed in with the first (as we saw on 2026-10-23).

**If the root user has lost all of its MFA devices:**

1. On the root sign-in page, after your password, look for the option to sign in another way. AWS then checks that you control both the account's email address and its phone number. You need both.
2. Once you are in, remove the lost devices and register two new ones, following [page 02](02-secure-the-root-user.md).

In a company, AWS advises that no one person should control both the root email inbox and the phone number, because together they can recover the root user. In a personal lab account you hold both. That makes your email password and your phone's lock the real keys to your AWS account, so protect them as carefully as the account itself.

**Confirm:** you can sign in with the new device. Each identity's list of MFA devices shows only devices you have. The IAM dashboard says the root user has MFA.

**Well-Architected:** Security · [SEC01-BP02 Secure account root user and properties](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/sec_securely_operate_aws_account.html)

## Check yourself

**1.** You notice that an access key for your IAM user is in a public code repository. What do you do first?

- A. Delete the repository.
- B. Deactivate the key in IAM.
- C. Change your IAM user's password.
- D. Wait for AWS to email you.

<details><summary>Feedback</summary>

- **A** is wrong as a first step. Anyone who already copied the key can still use it; deleting the repository doesn't turn the key off.
- **B** is correct. Deactivating the key stops it working at once. Then delete it and continue with the card.
- **C** is wrong as a first step. A password and an access key are separate; changing one doesn't affect the other.
- **D** is wrong. Every minute the key works, someone else can use your account. Act first; AWS's help comes in step 6.

</details>

**2.** Your zero-spend budget alerted this morning, but the Bills page shows nothing for the service you suspect. Why might that be, and what do you do?

<details><summary>Feedback</summary>

Model answer: billing data runs about a day behind, so the charge may not show yet, or it may be in a different service or Region than you think. Check every Region with Tag Editor for anything the lab left behind, delete it, and look at the Bills page and Cost Explorer again tomorrow. If you still can't explain the charge, open a free account and billing case.

</details>

**3.** Why does it matter that you registered a second MFA device for the root user before you lost the first?

<details><summary>Feedback</summary>

Model answer: with a backup device you simply sign in with it, remove the lost device and add a new one. Without one, you must recover through the account's email address and phone number, and you need both. If either has changed or is lost, getting back in becomes much harder.

</details>

## Where to check the current details

All checked 2026-10-23.

- [Resolve issues with unauthorized activity in AWS accounts](https://repost.aws/knowledge-center/potential-account-compromise), AWS re:Post Knowledge Center
- [Security incident response and resources](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-startup-security-baseline/security-incident-response-and-resources.html), AWS Startup Security Baseline
- [Working with CloudTrail event history](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html), AWS CloudTrail User Guide
- [Getting help with your bills and payments](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-get-answers.html), AWS Billing User Guide
- [Case management](https://docs.aws.amazon.com/awssupport/latest/user/case-management.html), AWS Support User Guide
- [Terminate active AWS resources that you no longer need](https://repost.aws/knowledge-center/terminate-resources-account-closure), AWS re:Post Knowledge Center
- [Root user best practices for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-best-practices.html), IAM User Guide
- [Multi-factor authentication for AWS account root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/enable-mfa-for-root.html), IAM User Guide
- [AWS Multi-factor authentication in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html), IAM User Guide
- [Security Pillar](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/security-pillar/wellarchitected-security-pillar.pdf), AWS Well-Architected Framework

---

"When something goes wrong, work through the steps in order" by Automate the Cloud Inc., licensed under CC BY-NC 4.0 with the Additional Permission for Internal Training from Automate the Cloud Inc.
License: https://creativecommons.org/licenses/by-nc/4.0/
Permission: https://automatethe.cloud/licenses/atc-internal-training-permission.txt
