# Working rules

Rules for anyone writing or changing this primer, people and AI assistants
alike. This repository is publishable and will become public, so everything
committed here must be fit to publish.

## Purpose and scope

- The primer is topic-independent: what a brand-new learner sets up in an
  AWS account before running labs for any Automate the Cloud guide. Keep
  course- or exam-specific material out; guides link here instead.
- It must work for the sign-up path and plan our guides teach (advanced
  sign-up, Free plan), and say clearly where the Paid plan or the newer
  sign-up experience behaves differently.
- For each step, say what to do, what not to do, why, what it costs, and
  whether it changes the account's plan (for example, creating an
  organization upgrades a Free plan account and forfeits its credits).
- Teach the "why" through the AWS Well-Architected Framework. Every
  guardrail names the pillar or pillars it serves (operational excellence,
  security, reliability, performance efficiency, cost optimization,
  sustainability) and the Well-Architected best practice behind it, so
  learners meet the framework early and later guides can build on it. Take
  every opportunity to teach, not just instruct.
- Start learners out with professional practice: an IAM user with MFA for
  daily work, never the root user. Name the bad practices and explain the
  harm.

## Where the facts come from

- Research for the first version lives in the private repo
  `study-aws-certified_cloud_practitioner` (`docs/12`, `docs/13`, `docs/14`,
  `docs/15`), checked out beside this repository. Every fact must trace to
  an official AWS page; cite it.
- Learning-design evidence lives in the private repo `study-learning-design`.
- AWS changes faster than its documentation. Date-stamp anything that moves
  (prices, Free plan terms, defaults), and tell learners to check the live
  AWS page.

## Writing

- **Original words only.** Never copy or closely paraphrase AWS
  documentation (CC BY-SA 4.0, whose share-alike conflicts with our CC BY-NC
  4.0) or third-party material. Cite AWS for facts; explain in our own words.
- Every edition carries the approved liability notice (research repo
  `docs/13`, word for word, with "This guide" read as "This primer") before
  the first step.
- American English. "Automate the Cloud" in prose, "Automate the Cloud Inc."
  in legal text.

## AWS trademarks and images

- AWS names in plain text only, for true factual statements. No AWS logos,
  badges, or trade dress. Never imply AWS endorsement.
- AWS service icons only from the AWS Icons for PlantUML set (CC BY-ND 2.0),
  unmodified and credited. Generic icons from openly licensed sets.
- Screenshots come from our own test accounts, redacted (email addresses,
  people's names, phone numbers, postal addresses, card details, MFA QR codes
  and secrets, keys, IP addresses, user IDs and credit IDs), and are marked as
  AWS material used as limited fair use, outside our licenses. For the
  `atc-test-01` test account the owner decided (2026-10-23) that its account
  ID, alias and company name may show, including inside ARNs. Only screenshots
  the owner has approved in the private redaction log may enter `images/`.

## Licensing

- Follow `LICENSING-PLAYBOOK.md` in the `atc-brand_kit` repo. Fetch a fresh
  copy before any licensing change.
- Every lesson ends with the attribution line from the playbook, section 7.
- Scripts and infrastructure files carry the two-line SPDX header; code
  examples meant to be Apache-2.0 are marked so.

## Commits

- Commit with `git commit -s`, using `55336416+david-singer@users.noreply.github.com`, so no personal address is published.
  Never mention an AI tool in commits or pull requests.
