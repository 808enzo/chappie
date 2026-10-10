---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Control metric: how to read the decided-close share

`SKILL.md` defines the metric: the risk case, the close by decision, the three remainder classes, the exits
kept out of the denominator, the period and the cut, why not the renewal, save or dunning recovery rate, and
what raises the share on worse work. This file holds how to read it.

## When the reading closes, and the unit

- **The reading waits** until every case of the period can have closed: the latest deadline among its
  recovery cases, the latest promised reply time among its requests by message, and the end of the cycle
  for each price consent. The effective date of a cancellation does not hold the reading: canceled, and
  kept after a restore before that date, are both decisions, so the date moves only the split between
  them. A recovery case with no deadline written does not hold the reading either; read it as ended
  without decision.
- **The unit is the case, not the person.** A person with a recovery case in March and an exit request
  in May contributes two cases, and both can close by decision. One action does not count twice: an exit
  request that ends a recovery case already open is that case's close by decision, not a second case.

## What moves it down

**What moves it.** Down: an obstructive screen that leaves people without a decision, because abandons
grow; a platform set to cancel on the first decline, because endings without decision grow; a case left
without a deadline, because you read it as ended.

## Read beside it

**Read beside it, and promote none of them.**

- **Exits decided outside the program**: cancellations in the store, blocks at the bank, disputes and
  notices of non-renewal on contracts paid by card, as a count and as a share of all exits.
- **The payment route** of recovery cases that paid: updated by the network, retry with no message, card
  updated after message N, paid by hand. A rising share of "updated by the network" is the card networks'
  work, not the program's.
- **Days in recovery per recovery case**, by access class: days of full access without payment are the
  price of the grace, days with access restricted or closed are the price of the window.
- **"Keep my plan" presses followed by another exit request**, through any door, before the next term
  ends: the sign that staying was the only exit the screen made visible.
- **"Cancelled recurring" disputes per thousand renewal charges**: the sign that a notice did not go out
  or the cancel path was not found.
- **Kept with an offer, at the end of the offer window**: the share still subscribed at full price once
  the offer's length and one full-price term have passed, read in `crm-reporting` as a cohort whose entry
  event is the accepted offer.
- **The closing lag of requests made by message** against the promised time.
- **Terms with no charge event** inside the platform's collection window: an object for
  `program-audit-and-ops`, not a metric.

## What it cannot see

**What it cannot see.** Whether the people kept stay: that is the cohort at the following term. The price
of keeping them: the discount. Whether the offer added anything over the screen without it: the holdout,
assigned when a request reaches the offer (reason "price", alternative declined), with the control
getting the cancel button and no offer, and both groups read on the same date, the assignment date plus
the offer's length plus one term at full price.
