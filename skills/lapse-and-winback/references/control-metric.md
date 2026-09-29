---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-09
---

# Control metric: how to read the return rate

`SKILL.md` defines the metric: the numerator, the denominator, reading it per threshold step, the two
numbers read beside it, and why not revenue attributed to win-back campaigns. This file works the metric
through on invented numbers.

## The metric on invented numbers

Read it out on a worked example with invented numbers. Four thousand people crossed the threshold
in a month. Seven hundred of them had no channel with both consent and reachability; two hundred
were suppressed by the frequency cap; three hundred were held in a control group; the remaining two
thousand eight hundred got at least one touch. Inside the attempt window, six hundred and forty
people performed the qualifying action: five hundred and sixty of the ones who got a touch, thirty
of the control group, and fifty of the nine hundred nobody sent anything to. The metric is
640 over 4,000, which is 16%. Not 640 over 2,800, and not 610 over 3,700: unreachable and
suppressed are outcomes of the attempt too, and they are precisely the outcome the skill exists to
prevent. The control group sits in both halves of the fraction, because it is part of the cohort.

That third figure in the numerator is the one a narrow denominator never sees. People you could not
reach come back at some rate of their own, the control group estimates that rate, and assuming it
is zero is the same error as leaving those people out of the denominator.
