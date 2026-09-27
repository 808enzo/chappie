---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-14
---

# Control metric: how to read accounts in step

`SKILL.md` defines the metric: the population past the handoff, the next step and what keeps it, the exits and
their records, and why accounts and steps rather than handoff conversion or cycle length. This file holds how to
read it.

## When the reading closes

- **Read at the period's end.** The period is your regular report's. A month is the starting point; it holds
  while the median interval between an account's steps is shorter than the period, and it is replaced by the
  stage's median duration where it is not, because a period in which nothing falls due reads every account as in
  step. A promised time that, with its grace, falls after the period's end is judged in the next period. A dead
  period of the account stops its timers; it does not remove the step.

## The metric on invented numbers

Take a worked example with invented numbers. In a month, 80 accounts were past the handoff at some moment. 47
kept every step of the period and hold a next step at month end; 9 closed with a code and no missed step; 5 were
returned with their kind recorded, and a date where the kind needs one, having missed no step before; 8 had a
step pass its time with no record, seven
of the account executive's and one of the program's; 3 had a customer's promise pass its grace with no account
executive's step on the next working day; 2 were handed over and not accepted by the promised time; 6 had no
recorded step at some moment of the month, two of them returned "not now" without a date. The metric is 61 over
80, about 76%, not 61 over 74: the six without a step count against the register.

## What moves it

**Doubling the program's touches leaves the share flat:** a program step is kept by construction. Doubling the
account executive's steps at the same discipline per step lowers it: every step is a chance to miss. That is why a
change of the step rule is read against the count of steps per account, which stands beside the metric.

**Where it moves.** Down when a sales stage does not require a step with a date, when a customer's promise gets
no timer, when a return leaves without a re-entry date, when some account executives keep the register and
others do not, when a salesperson's vacation is not covered by a substitute. Up with the steps of
`references/qualification-and-handoff.md` and `references/buying-group-and-stalls.md`.

## Read beside it

**What to read beside it, and promote none.**

- **Misses by doer** (the program, the account executive, the customer, the acceptance) **and by account
  executive;** steps per account.
- **Acceptance share and the codes of non-acceptance;** time to acceptance and to the first human touch after
  the handoff.
- **Return share by kind,** and the share of returns that carry a re-entry date.
- **Coverage by role, by stage** (`references/buying-group-and-stalls.md`).
- **Idle time by stage** against the stage's own median; reschedules per step.
- **The share of customer promises kept by their date.**
- **The share of accounts that changed stage in the period,** and the share of a handoff cohort that reached a
  decision, read at its settling age (`crm-reporting`).
- **Loss codes** and their mix.
- **Won share by grade cell at the time of handoff, and by coverage at the vendor evaluation stage:** the
  readings that test the grid and the role register, and they arrive a cycle later.

## What it cannot see

**What it cannot see.** The content of a step; whether the right role was touched (coverage beside it); whether
the deal was winnable (the cohort reading of `crm-reporting`); the quality of the won-deal record (read by
`b2b-retention`).
