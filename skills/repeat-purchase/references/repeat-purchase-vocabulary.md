---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# Vocabulary for repeat-purchase

The terms all three mechanics assume. Four of them are shared with neighboring skills under
different meanings, and those are marked at the end.

## Subject

The thing whose repetition is being counted: a product, a product variant or a category. The level
is chosen once and does not change quietly, because changing it changes every interval computed
under it.

## Closed order

Paid and received. Every clock in this skill runs from that event and not from the order being
placed. An order that is later returned stops meeting this definition after the fact.

## Interpurchase interval

The time between two closed purchases of one subject by one person. It needs two points, so it does
not exist for somebody with a single purchase.

## Substitution ladder

The order of the four sources of an interval, from this person's own history down to published
research. You step down when the rung above fails its condition, not when it is convenient.
Everybody below the first rung has exactly one purchase of the subject.

## Unit duration

A catalog field holding how many days one unit of a product lasts. It is the first source to try
for somebody with a single purchase, because it counts consumption rather than people and so
carries no bias from who came back.

## Advance

Room to decide plus delivery time to the address, subtracted from the interval to get the reminder
date. It is the reason two people who bought the same thing on the same day get different dates.

## Reminder date

The computed date on which the message is due. This skill computes it; `triggered-messages` fires
on it.

## Deferred reminder

The person's own answer that they want reminding later. It outranks the model, applies to the pair
of person and subject, and survives the next recompute.

## First purchase cohort

Everybody whose first order closed in a period, including the people nobody sent anything to and
the people held in a control group, less anybody whose first order was returned inside the return
window. It is final only once the return windows on first and second orders and the cohort window
have all run out.

## Cohort window

The finite span over which the second purchase mechanic works on a cohort. Past it the person is
handed on by outcome, and for somebody with one purchase its end is also the absence threshold in
`lapse-and-winback`.

## Time to second purchase

The time from a first closed purchase to a second one, measured over the cohort rather than over
the people who bought twice. Where fewer than half a cohort ever buys again, its median does not
exist and a percentile or the flattening point is used instead.

## Stretch

An independent part of the window that fires on time elapsed since the order closed and evaluates
its own condition. Stretches are independent so that one failing does not silence the rest.

## Order of the argument

Service, then product, then money. The order is set by what each step costs you, not by manners: a
monetary argument placed first buys the purchases that were coming anyway.

## Add on

An offer made against an order. Three kinds: a dearer alternative, a companion item, and a cheaper
alternative.

## Cheaper alternative

The kind of add on whose entry condition is a refusal over price rather than a purchase. Hung on a
purchase instead, it discounts somebody who had already agreed to pay more.

## Pair

A link between two products, drawn either from a history of items bought together or from a rule in
the catalog.

## Exclusion list

The subtraction applied before a selection is shown: already owned and not consumable, out of
stock, outside this person's constraints.

## Repeat purchase flag

The catalog field saying whether an item is bought again or bought once. It comes from the catalog
and is not inferred by an algorithm.

## Monetary add on

An add on that raises the order value out of the margin: a discounted bundle, free delivery. One
per order, and none on an order that already carries another mechanic's offer.

## Signed miss

The median of the next actual closed purchase of a subject minus the date the model said it would
run out, before the advance. Zero means the model lands; a persistent negative value means the
interval is too long. It reads the next purchase from the same history as the interval, so it
cannot see a channel that history does not hold.

## Words shared with neighboring skills

- **Interval.** Here it is the gap between purchases of a subject, computed per person down the
  ladder. In `lapse-and-winback` the same word is the base of the absence threshold, taken as a
  median across a category and used as one number per segment. The difference is where the number
  comes from: the neighbor counts across the base, and here the number is personal and comes down
  the ladder.
- **Second purchase.** Here it is the target action of the cohort mechanic. In
  `welcome-and-activation` the target action is the **first** purchase, and breaking that series
  hands the person here. In `lapse-and-winback` a return can be somebody's second purchase and
  still not count here: it lands after the window, where a single buyer has crossed the absence
  threshold.
- **Selection.** Here it is a set of items assembled against an order by subtraction. In
  `personalization` it is the algorithm, the fallback and the place it is substituted into. This
  skill sets the condition on what may appear; the neighbor decides how the choosing is done.
- **Reminder.** Here it is a message on a computed consumption date. In `triggered-messages` a
  reminder is any message fired by an event after a wait, an abandoned cart included. The two are
  told apart by where the timing comes from: the neighbor's is a delay you set, this one
  is computed.
