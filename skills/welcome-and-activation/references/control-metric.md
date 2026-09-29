---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-08
---

# Control metric: how to read the first-action rate

`SKILL.md` defines the metric: the numerator, the denominator, where the cohort is counted, reading it
per entry point, and the two numbers read beside it. This file works the metric through on invented
numbers and says how to read the people who bought before any touch went out.

## The metric on invented numbers

Read it out on a worked example with invented numbers: four hundred records arrive in a week through
the site form, forty are undeliverable from the start, twenty sit in a pending state that never
resolves, the remaining three hundred and forty enter the series, and thirty-four complete the
target action inside the window. The metric is 34 over 400, not 34 over 340. Those sixty people are
the ones this mechanic lost without sending anything, and no report about the series contains them.

**The numerator counts the cohort's outcome and not the series' work.** Six of those thirty-four
bought in the session they arrived in, before any touch went out (`entry-and-series-design.md`, edge
cases). They stay in the numerator, because the denominator counts everybody who arrived and both
halves have to stand on one population. Read that sub-count beside the metric, and when it grows
large enough to move the number, what moved is the capture point and not the series.
