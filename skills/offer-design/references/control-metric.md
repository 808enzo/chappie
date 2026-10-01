---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Control metric: what realized depth leaves out, and what to read beside it

`SKILL.md` defines realized depth: the benefit actually given over the pre-benefit value of the orders
that carried it, read per offer and only on those orders. It says why this is the number the three
mechanics move, and what to answer when someone asks what is normal. This file holds what the metric
leaves out (a promise that did not apply, and the outcome every redemption attempt gets) and the two
numbers to read beside it.

## A promise that did not apply

**A promise that did not apply is not in the metric, so record it as an outcome of its own.**
Realized depth is computed on orders where the benefit went through. A rejected code, an exhausted
stock, a limit that refused, and a personal offer outranked by a public one reach neither the
numerator nor the denominator. A carrier that half died leaves depth on the orders that got through
equal to the designed depth. A carrier that died completely leaves no rows at all, and the empty
cell reads as missing data, not as a failure. So every **redemption attempt**, meaning a code
entered or an order placed by the holder of an issued promise inside the redemption window, gets an
outcome: applied in full; reduced by the floor; or not applied, with a reason. Name the reason
after the rule that refused: an issuing limit (which of the six), the window, the entry condition, an
exclusion, the stock, a carrier that no longer works, or an offer that outranked this one. A refusal
with no reason of its own reads as a telemetry gap when somebody checks absolute counts. Beside the
metric, per offer, read **the share of attempts not applied**, broken down by reason. Keep those
attempts out of the depth denominator itself: their value would pull depth down while a leaking
stack pushes it up, and the two failures would cancel inside one number. On a shared carrier the
holders are unknown, so an attempt is only a code entered.

## Read beside it

Read two more numbers beside it and promote neither. **The share of orders carrying a benefit** is
the ballast measure: rising while revenue per order sits still is the signature of price
anchoring, and the skill's slowest failure. **Incremental share**, how many of those orders would
not have happened without the benefit, belongs to `experiments-and-holdouts` and cannot be
computed at all without an exclusion test. Requiring that test is this skill's obligation;
designing it is not.
