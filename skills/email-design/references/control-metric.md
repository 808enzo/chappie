---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Control metric: how to read the environment click index

`SKILL.md` defines the environment click index: the rate's numerator and denominator, the divisor, the
environment and the provider; why divide inside a provider, why not `deliverability`'s index and the
question that separates the two, how the index reacts to where a defect sits, and the preview tool count
nobody should report as a win. This file holds how to read it.

## When to read it, and when a new series starts

- **Read it** no earlier than the end of the click collection window you fixed (`metric-definitions`
  requires fixing one) and after the retry queue for that send has emptied, per pair of provider and
  environment, against that pair's own median and spread over recent sends of the same template.
  Clicks that arrive after the window stay out, so that sends read at different ages compare.
- **A new template version does not restart the baseline.** The index exists to catch what a version
  broke in one environment, and restarting it at every version blinds it to exactly that. A new
  environment starts a new row. A change in the set of layers starts a new series, because a message
  carrying a layer that only some environments show measures the layer; so does a version that gives
  environments different sets of links, such as a menu hidden at the narrowest width, because the
  index then measures the menu. `email-copy` starts a new baseline when the template changes, and
  the two rules do not conflict: its share is normalized inside one message and moves with the number
  of links the template carries, while the ratio between environments inside one provider does not,
  as long as every environment sees the same links.

## Where one environment holds nearly all of a provider

**Where one environment holds nearly all of a provider, the index cannot answer the question.** A
row holding nearly all of a provider's accepted recipients is the provider's rate, so its index sits
at 1 and moves by no more than the other rows' share: at a 95% row, a halving of its clicks reads
0.95. A break there shows as the small rows rising, as the provider's absolute rate falling, and as
`deliverability`'s index falling, which is the picture placement gives too. Open the seed mailbox in
that environment first, before you touch volume.

## A fall every environment shares

**When every index is flat and the absolute rate fell in every environment**, look for a cause the
environments share. Four qualify. Read them in this order: the share of sends on no released version
(`references/template-system.md`, second failure mode); the assembly log's share of full states
(`references/block-states.md`, first failure mode); then the words and the offer, which is
`email-copy`; then every provider at once, which is `deliverability`. The first two are this skill's,
and you read both from a log rather than from the index.

## The pull toward 1

**The environment field pulls the index toward 1.** The environment is the last one known, and a
person who reads in two environments sits in one row while reading this message in the other. A fall
in the broken environment therefore reads weaker than it is. The bias runs one way for the broken
row: it hides part of its fall. Rows whose readers also read in the broken environment carry a share
of that fall, smaller than the broken row's own; a row whose readers never open the broken
environment does not move down.

## A worked example

**Take a worked example with invented numbers.** A provider accepted 10,000 messages: 6,000 for
recipients in a mobile app environment and 4,000 for a desktop client. 180 and 160 of them clicked,
rates of 3% and 4%, a provider rate of 3.4%, and indices of 0.88 and 1.18. A new version breaks the
button in the app: 90 click there (1.5%), still 160 on desktop, the provider rate falls to 2.5%, and
the indices become 0.6 and 1.6. The app is below its band, and the desktop rise is the echo of that
fall. In the same invented send the other providers accepted 30,000 at 3.4%, so `deliverability`'s
index for this provider falls from 1.0 to 0.79 and looks like placement. Had it been placement, with
half the mail in every environment filed to spam, the rates would be 1.5% and 2%, the provider rate
1.7%, and the environment indices 0.88 and 1.18, unchanged. Now give the same provider 5,000 more
accepted recipients with no known environment, 25 of whom click, and on the next send 10,000 of
them, 50 clicking, after a cohort of new subscribers arrives. The divisor is the known rows, so the
indices stay at 0.88 and 1.18 through both sends. Had the unknown row been in the divisor, they
would have moved from 1.23 and 1.64 to 1.54 and 2.05 with nothing changed in any environment.

## Read beside it

**Read four numbers beside it and promote none of them.**

- **The absolute click rate in the row.** An index of 1.0 on three clickers is noise, and a defect
  shared by every environment leaves all indices flat.
- **The share of clicks on the web version link, per row.** Rising in one environment on one send,
  it says the message is not showing there.
- **The share of a provider's accepted recipients with a known environment.** The field is never
  cleared, so it falls only as the base fills with people who have not clicked yet. Read the unknown
  row's own absolute rate against its history: a break in the environment those people read in
  shows nowhere else, because they never get a row.
- **Release coverage:** the share of accepted recipients in environments checked for the version in
  use, and the share of sends that went out on no released version at all.

## Every class and who owns it

**Read every class and who owns it.**

| What happened to the recipient | In the index | Where it is read |
|---|---|---|
| accepted, clicked a link other than a required one | numerator and denominator | the index |
| accepted, clicked only a required link | denominator only | the route out, `deliverability`; the withdrawal, `consent-and-preferences` |
| accepted, clicked only the web version link | denominator only | the web version share of that row, beside the index: the reader asked for the message somewhere else |
| accepted, and the client did not show images by default | denominator | the index: if the job lives in text, the clicks arrive, and that is what the index measures |
| accepted and filed to spam | denominator | spread across the provider's environments, so `deliverability` |
| deferred, retries still running | not yet | joins if a retry is accepted; `deliverability` |
| refused | no | `deliverability` |
| not sent by a program decision or a cap | no | `contact-orchestration`, `email-program` |
| assembly returned do-not-send | no, and it is counted separately | the assembly log, `references/block-states.md`; resolved share, `personalization` |
| a block was removed for this recipient | denominator | the assembly log; removal does not depend on the environment, so the index does not see it |
| environment unknown | a row of its own | its share is coverage, read beside the index |
| forwarded and opened by somebody else | the click is credited to the recipient, from another environment | noise, and not correctable |
| the action is a reply, a call, or a link your platform does not rewrite for tracking | denominator, no click | read that row on a different event, or mark it unreadable |
| nearly every recipient in the row clicks within moments of acceptance | denominator, and the numerator is not a person | the row is unreadable until your platform separates those clicks |

## The smallest row worth reading

**The smallest row worth reading is yours to compute.** Take two consecutive sends of the same
template with nothing changed and see how far each row's index wanders; that wander is its noise.
Read the rows whose noise is smaller than the fall you want to catch.

## Triggered flows and new recipients

**Triggered flows send continuously**, so read a period, such as a week, in place of a send, with the
same formula inside it and both halves counted on messages: a message is in the numerator when its
recipient clicked it, so that a person who received three messages in the period is not one clicker
over three messages.

**A template whose recipients are mostly new**, a welcome flow first of all, has no rows: nobody has
clicked before the first message, and everyone sits in unknown. The matrix and the absolute rate
carry that template. Where a confirmation click precedes the first message, it is a click before the
send, and it sets the field.
