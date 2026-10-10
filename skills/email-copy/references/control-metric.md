---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Control metric: how to read the on-job click share

`SKILL.md` defines the metric: the numerator, the denominator with the required links kept out of it,
the messages it is compared against, why it divides, why not click-to-open rate or open rate, and how
it rises when the work gets worse. This file holds how to read it.

## When the reading closes

- **Read it after the clicks have stopped arriving**, at the end of the collection window you
  fixed for click metrics; fixing that window and writing it down is part of a definition
  (`metric-definitions`). Read the share the morning after a send and you read part of your own
  numerator, and on a triggered message a receiver that deferred it is still handing it over while
  you read (`deliverability`).

## Link roles come first

**Link roles are a condition, not a convenience.** Without them the metric cannot be computed at
all, and reconstructing them afterwards from a report is guesswork: a report shows the address, and
two links to the same catalog page can be the work of the message in one place and the header menu
in another. Assign them in the brief, before the template is built.

## The share on invented numbers

**Take a worked example, with invented numbers:** a thousand people clicked a work, support or
navigation link in a message, seven hundred of them clicked a work link, and four hundred clicked
navigation or support, some people doing both. The on-job click share in that example is 0.7, and
if your own history of messages of this kind sits near 0.85, this one failed to carry its job, with
the place to fix it the first block rather than the subject line.

## What moves it

**The share is a ratio, so its reaction depends on where you intervene, and that is computed rather
than guessed.** `SKILL.md` says how it rises when the work gets worse. The opposite case is real
too: add a block of supporting links and the share falls although the message got clearer.

## Read beside it

**Read two numbers beside it and promote neither.**

- **The absolute share of recipients who clicked a work link**, against delivered: the counterweight
  `SKILL.md` names beside a rise.
- **The share of messages whose job is not observable at all**, meaning the action leaves no event
  anywhere. This is the honest coverage number: while it is large, the control metric describes a
  minority of your messages, and you cannot quote a program-wide figure. Count it in three classes:
  observable, declared unobservable in the brief, and **sent with no brief at all**. A message with
  no brief is unclassified rather than observable, so counting it as observable makes coverage look
  best at the moment brief practice collapses, which is the failure mode in
  `references/message-brief.md`.

**Read every class of the denominator and who owns it.**

| What happened to the person | In the denominator | Where it is read |
|---|---|---|
| clicked a work link | yes, and in the numerator | the metric itself |
| clicked only navigation or support | yes | the metric itself |
| clicked only the unsubscribe link in the footer | no | unsubscribe rate, `metric-definitions`; the route out itself is `deliverability`, the withdrawal is `consent-and-preferences` |
| left through the one-click header instead of the footer link | no, and it leaves no link click at all | `deliverability`, which owns both routes |
| clicked only contacts, a legal page or the web version link | no | nowhere yet for the first two, and that is deliberate: the required role is outside the metric so the metric cannot reward burying it; the web version share is read by `email-design` as a rendering sign |
| opened and clicked nothing | no | the absolute share; opens themselves are `metric-definitions` |
| the message was never delivered | no | `deliverability` |
| the message was deferred and arrived after you read the number | no, and it should have been | the reading window above |
| the message was held back by a cap or a priority rule | no | `contact-orchestration`, `email-program` |
| clicked and then did nothing on the page | yes | conversion and its three denominators, `metric-definitions`; the page is not this skill's |
