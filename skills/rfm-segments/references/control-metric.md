---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Control metric: what moves the stale group send rate and what to read beside it

`SKILL.md` defines the stale group send rate: the numerator, the denominator and the label that makes it
readable, the four cases the label settles, the unit and the window, why it has a known right answer and
is read per group, and what to answer when someone asks what is normal. This file says from which side
each mechanic moves it, and names the two numbers to read beside it.

## What moves it

**All three mechanics move it from different sides.** Cutting the axes decides which axis is the
deciding one. The group set decides where being wrong is expensive. The recompute decides how
stale the read is allowed to get.

## Read beside it

Read two more numbers beside it and promote neither. **The share of the base sitting in groups
below the readable floor** says the grid was cut finer than the base supports, which is the
ordinary result of naming all twenty seven cells. **The share of the base the grid cannot place**,
meaning people with no purchase history, says whether the method describes your base at all:
where that share is large, RFM is answering a question about a minority of the people you have.
