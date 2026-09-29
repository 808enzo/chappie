---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Control metric: what to read beside the reconciliation gap

`SKILL.md` defines the reconciliation gap: the numerator, the denominator, reading it per flow and no
sooner than the slowest fact in the flow, why this number, and the self-baseline. This file holds the two
numbers read beside it.

## Read beside it

Read two more numbers beside it and promote neither. **The share of live flows that appear in the
flow diagram** decides whether anybody can say what breaks when a system changes. **The share of
events in the plan that name a consumer** is the ballast measure: it tells you how much you are
collecting and paying for without reading. On a plan built under the rule that an event with no
consumer does not get built, that share starts at everything, and it drops for two reasons worth
telling apart: events that predate the plan, and events whose consumer was retired without anyone
turning off the capture.
