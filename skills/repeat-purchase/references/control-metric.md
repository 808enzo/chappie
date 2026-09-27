---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# Control metric: how to read the second purchase rate

`SKILL.md` defines the metric: the numerator, the denominator, the returned first order, why unreachable and
suppressed people stay in, reading by cohort, why not the repeat purchase share, and why not revenue attributed
to repeat purchase mechanics. This file holds how to read it.

## When the figure is final

What follows operationally is a timing rule. **The figure is final only once three spans have run
out for the whole cohort**: the return window on the first order, which settles the denominator;
the cohort window, which settles who bought again; and the return window on that second order,
since a returned second order is not a second purchase either. If you read it before the first
span ends, the rate is understated, because the denominator still holds people who will leave it.
If you read it before the last one ends, it is overstated, because the numerator still holds second
orders that will come back.

## The metric on invented numbers

Read it out on a worked example with invented numbers. Five thousand people closed a first order in
a month. Two hundred of them returned it inside the return window, so they leave and the cohort is
four thousand eight hundred. Inside that cohort: nine hundred have no channel with both permission
and reachability, one hundred and fifty were suppressed by the frequency cap, four hundred were held
in a control group, and the remaining three thousand three hundred and fifty got at least one touch.
Inside the window a second order closed for seven hundred and sixty five people: six hundred and
twenty of the ones who got a touch, fifty five of the control group, and ninety of the one thousand
and fifty nobody sent anything to. The metric is 765 over 4,800, which is 16%. Not 620 over 3,350,
which is 18.5%, and not 765 over 5,000, which is 15.3%.

That third figure in the numerator, the ninety nobody wrote to, is the one a narrow denominator
never sees. Some people come back on their own, the control group estimates how many, and assuming
that number is zero is the same error as leaving those people out of the denominator.

## Read beside it

Read two more numbers beside it and promote neither.

- **The signed miss**: the median of the next actual closed purchase of the subject minus the date
  the model said it would run out, before the advance comes off. Zero means the model lands. A
  persistent negative value means people restock before the model expects, so the interval is too
  long: the wrong level, a stale catalog field, quantity counted twice. It cannot see purchases
  your history does not hold, because it reads the next purchase from the same history as the
  interval, so you catch an unstitched channel by reconciling order counts
  (`references/interval-model.md`). Read it on purchases no reminder preceded where you can, since
  a purchase made in answer to a reminder takes its date from the reminder, and not before the wait
  named in the interval model's thresholds.
- **Margin per order beside average order value.** Order value on its own reads wrong: a monetary
  add on raises it and cuts margin in the same motion. The pair is read together or not at all. The
  economics are `offer-design`.
