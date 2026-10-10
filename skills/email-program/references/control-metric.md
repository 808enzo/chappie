---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-04
---

# Control metric: how to read revenue per recipient against a holdout

`SKILL.md` defines revenue per recipient: the cycle, the denominator in people and why not revenue per
delivered message, why you read it next to total channel revenue, and why opens and clicks stay
diagnostic signals. This file holds how the metric reads against a holdout.

## Against a holdout

Against a holdout the metric changes shape. A control group receives nothing you can attribute
revenue to, so read revenue per person assigned to each group over the same window, in any channel
and with no credit rule, and take the difference as what the program added. The holdout that
answers that question is a control drawn from the base and rotated. The send-level holdout of step
6 in `send-selection-and-suppression.md` is a different object, and `experiments-and-holdouts`
designs both.
