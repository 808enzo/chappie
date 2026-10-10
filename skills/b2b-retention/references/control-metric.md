---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Control metric: how to read renewal cases decided by their decision point

`SKILL.md` defines the metric: the population from billing, the three forms of a decision, the remainder, the
terms kept out of the denominator and the period, and why this share rather than the renewal rate or revenue
retention. This file holds how to read it.

## When the reading closes, and the unit

- **Reading.** Read the share at the end of the period: the numerator closes at each decision point, and nothing after that
  point changes a case's class in the numerator. The split of the remainder (decided late, in holdover, ended) waits for the
  latest holdover ceiling among the period's cases, and for the payment date of the new term's first invoice on every case
  renewed by default: until then such a renewal can still come apart (a dispute settled as termination, a provision that
  does not hold without the notice the law requires, a completed switch) and move to ended. Each term is its own case, so
  a contract renewed by default twice stands in the remainder twice. The effective date of a notice holds nothing: "not renewed" and
  "renewed after a protective notice" are both decisions, and the date moves only the split of the numerator.
- **The unit is the case, not the account.** An account with two contracts on different dates contributes two cases, and
  two cases on one buying unit stand beside the metric as the sign of unaligned end dates.
- **The form matches the decided-close share in `subscription-retention`,** and the units differ: a recovery case is
  the neighbor's, a renewal case is this skill's, and a contract paid by card with an account manager contributes to each
  once, on different events.

## The metric on invented numbers

Take a worked example with invented numbers. In a quarter, 40 cases reached their decision point. 22 contracts were signed
before it: 17 unchanged, 3 with expansion, 2 with contraction. 4 written notices of non-renewal arrived; one of them was
protective, and a renewal was signed after it, before the effective date. 3 economic buyers confirmed continuation on
automatically renewing contracts. 7 automatically renewing contracts passed their decision point with no decision. 4
contracts that needed a signature reached their end with none: 2 were signed during a holdover, 1 ended at its ceiling, and
1 is still in holdover on the reading date. Separately, 2 contracts were terminated for non-payment before their decision
points; they stand outside the share, beside it. The share is (22 + 4 + 3) / 40 = 29 / 40, or 72.5%, not 29 / 42. The
numerator splits into 23 renewed (the 22 signed, plus the protective notice followed by a renewal), 3 continuations
confirmed and 3 non-renewals. The remainder of 11 holds 7 renewed by default, 2 decided late, 1 ended and 1 in holdover,
and its split waits for that holdover's ceiling.

## What moves it

**What moves it.** Down: a case opened after the customer's approval time, so the decision cannot arrive by the point; a
decision point never written; automatic renewals left to roll, so renewed by default grows; an account with no contact
holding authority, so nobody can confirm. Up: the opening date counted from the approval time, and a QBR with the economic
buyer before the case.

## Read beside it

**Read beside it, and promote none of them.**

- **Revenue retention,** gross and net, as the complements of revenue churn and net revenue churn in `metric-definitions`,
  by contract start cohort (`crm-reporting`), with renewed by default and holdover on lines of their own.
- **Contracts renewed by default,** as a count, those renewed by default in consecutive terms, and their fate in the next
  term: collection cases on the renewal invoice, renewals that came apart, notices of non-renewal.
- **Won-deal records** returned to the account executive, by the gap named, and records accepted past their promised time:
  here you read the quality of the record `b2b-lifecycle` hands over.
- **Contracts in collection and in holdover** on the period's end date: count, revenue, and whether the holdover is
  invoiced. This is the price of "live until the ceiling".
- **Days ahead of the decision point** at which the decisions came, as a distribution by contract class.
- **Coverage of the economic buyer** on the opening date, and the share of cases opened after a QBR with the economic buyer.
- **Milestones kept by their date,** by doer, and the time to the first milestone.
- **Terms decided before any case,** by cause; evergreen contracts, by count and revenue.
- **Reason codes** of non-renewals; protective notices and their outcome.
- **Amendments:** the share aligned to the end date; contractions at renewal; expansions signed less than one term before a
  notice of non-renewal.
- **Collection cases:** class, days overdue, payment route.
- **Renewal concessions** by depth.

## What it cannot see

**What it cannot see.** Whether a renewed customer got what it bought for (the milestones beside it); the price of the
renewal (the concessions beside it); whether a lost renewal was winnable with other work.
