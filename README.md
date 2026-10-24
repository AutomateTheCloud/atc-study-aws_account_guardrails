# Setting Up a Safe Account on AWS: Guardrails Before Your First Lab

What to set up in a new AWS account before you run any lab, so a mistake
can't turn into a large bill or a security problem. It covers cost alerts,
basic account hardening, and the habits that keep an account safe, and it
names the common bad practices and explains why each is dangerous.

Every Automate the Cloud guide that has you work in your own AWS account
starts here. The primer is written for people who are new to AWS and
doesn't depend on any one course.

**Status:** first draft, in review. Nothing here is published yet.

## Contents

Work through the pages in order.

0. [Read this first](primer/00-read-this-first.md): the notice, the two risks, the AWS Well-Architected Framework, and choosing the Free plan
1. [Create your account](primer/01-create-your-account.md)
2. [Secure the root user](primer/02-secure-the-root-user.md)
3. [Your everyday admin identity](primer/03-your-everyday-admin-identity.md)
4. [The command line without access keys](primer/04-command-line-without-access-keys.md)
5. [Money alarms before you build anything](primer/05-money-alarms.md)
6. [Safe defaults](primer/06-safe-defaults.md)
7. [Habits for every lab](primer/07-habits-for-every-lab.md)
8. [When something goes wrong](primer/08-when-something-goes-wrong.md)
9. [Leaving cleanly](primer/09-leaving-cleanly.md)
10. [Bad practices and checklist at a glance](primer/10-bad-practices-and-checklist.md)

## Editions

The primer is written once, in Markdown, and built into three editions:

- **Markdown** in this repository, readable on the hosting platform.
- **Website**, on an Automate the Cloud learning site.
- **PDF**.

## Your account, your responsibility

You follow this primer in your own AWS account. You are responsible for
that account, its security, and any charges it incurs. The primer reduces
risk; it can't remove it. See the notice in each edition before you start.

## Trademarks

Automate the Cloud is not affiliated with, endorsed by, or sponsored by
Amazon Web Services. AWS and Amazon Web Services are trademarks of
Amazon.com, Inc. or its affiliates. They are used here only to identify the
service this primer is about.

## Licensing and permitted use

Our educational materials are licensed under **CC BY-NC 4.0**, with
**additional permission for internal training**, including at for-profit
companies.

You may:

- Use the materials for personal learning and noncommercial education.
- Copy and adapt them to train your own employees and contractors.
- Host them on an internal learning platform, subject to the additional
  permission.

Selling the educational materials, incorporating them into paid training
offerings, or bundling them into commercial training products requires
separate written permission from Automate the Cloud Inc.

Software in `source/` and `infrastructure/` is separately licensed under
**Apache 2.0** and may be used commercially.

Screenshots of AWS websites and consoles are AWS material used as limited
fair use, and are not covered by these licenses.

See [License scope](LICENSE.md), the
[educational-materials license](LICENSE-CC-BY-NC-4.0.txt), and the
[internal-training permission](INTERNAL-TRAINING-PERMISSION.md) for the
applicable terms.
