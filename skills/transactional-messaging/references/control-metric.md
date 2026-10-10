---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Control metric: how to read the chase share

`SKILL.md` defines the chase share: the transaction, the cohort, the chase, the numerator window, the
denominator and the path; why transactions and not messages, why not latency, opens, revenue or the support
contact rate in general, what lowers it without better work, complaints and switch-offs after service
sends, the line that shows the cost of noise, and what raises it without worse work. This file holds what
else moves it, the other lines read beside it, and what it cannot see.

## What moves it

**Where it moves.** Down when exception rows get promise timers, when promised times become ones the
operation keeps, when service sends get a queue of their own.
Up after a bad week at a carrier (the share of transactions on the exception path rises, so read by
path), after a status map change that silenced a state, after a release that broke a trigger.

## Read beside it

**What to read beside it, and promote none.**

- **On-time share for each row:** transactions that had a send of the row delivered before the row's
  deadline, over transactions that entered the row's state, with the transactions whose send never
  happened in the denominator. A transaction whose only send went through a channel that issues no
  receipts stays out of both halves, and its share is read beside: acceptance is not delivery
  (`messaging-channels`). Both halves count transactions: a failover that delivered twice is one
  on-time transaction, not two sends.
- **Timeline sample findings** for the period, by gap class.
- **The share of untied status contacts** among all status contacts, and beside it the number of open
  transactions the person had at the moment of contact. When the share rises, the metric reads low; when
  it concentrates among people with several open transactions, the first line is not asking which one
  (`references/chase-reading-and-repair.md`, step 1).

## What it cannot see

**What it cannot see.** People who gave up asking, and chases in places where the company does not
answer: public reviews, and payment disputes filed as "not received".
