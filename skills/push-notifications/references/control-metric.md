---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Control metric: how to read the displayable share

`SKILL.md` defines the displayable share of an install cohort: the cohort, the check age, the numerator,
the denominator and its classes, the staleness threshold, why endpoints and why an install cohort, the web
and each platform read apart, and the two numbers read beside it. This file holds two rules for comparing
cohorts.

## Stale and retired, added together

**Stale and retired split by how much you send.** A removed app shows up as retired only when a
send reaches its token and comes back rejected. Nothing tests the token of an endpoint you do not
send to, such as one never asked or refused, so a removal there lands in stale. A cohort that received more sends
shows more retired and fewer stale endpoints for the same behavior, so compare cohorts on the two
classes added together.

## A reinstall in two cohorts

**A reinstall is counted twice.** The person leaves the old endpoint in the old cohort, retired once
a send hits its token and stale until then, and a new endpoint in a later one. Where reinstalls or
device changes are frequent, report the old cohort's retired and stale endpoints whose person holds
a newer displayable endpoint on a line of their own, so that the old cohort's loss is not read as a
lost person.
