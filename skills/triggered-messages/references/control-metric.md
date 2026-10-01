---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Control metric: the holdout and when a period's reading closes

`SKILL.md` defines conversion per entry: the share of entries that reach the target action inside a fixed
window, read against a holdout of entries. It says why entries and not sends or opens, the five conditions
the metric is written down with, the two lines to read beside it, and what to answer when someone asks
what is normal. This file says why an event-fired flow needs a holdout, who designs it, and when a
period's reading closes.

## The holdout and the read date

Everyone who enters a triggered flow has already shown intent, which is why an event-fired flow
looks successful in every report that lacks a control group. Holdout design and the assignment log
belong to `experiments-and-holdouts`. Demanding a holdout is part of this skill. Read a period only
once its window and the cancellation period of its orders have both closed.
