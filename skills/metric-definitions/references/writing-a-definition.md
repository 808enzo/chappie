---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Writing one metric definition

Most arguments about a number are not about the number. They are about the denominator, and they
last as long as nobody says it out loud. A definition is the sentence that ends the argument;
without it, the argument is re-derived in every meeting.

This mechanic is one metric, written so that a person who was not in the room can reproduce it.

## Entry conditions

- Two people quote different values for one metric name, or one person cannot say how a number
  was produced.
- The metric is about to become a target, a KPI or a line in a report someone will act on.
- A new program area is starting to report.

## Exit conditions

The metric has a written numerator, denominator, measurement window, attribution window,
conversion key, credit rule, attribution method, system of record, exclusion list, unit of count,
refresh cadence and freeze rule, plus an owner and a version date. Where the metric carries a
target, the definition also holds the tolerance a reading against that target is judged by. The
record sits where the numbers live, not in a message thread.

## Sequence

**1. Name the decision the metric serves.** A metric with no decision behind it is a reporting
slice, and it belongs to `crm-reporting`. This is the same first step `segmentation` uses on a
cut of the base, for the same reason: without a decision there is no way to settle any of the
choices below.

**2. Write the numerator as an event with a qualifying condition.** "Purchase" is four different
numerators: order placed, order paid, order delivered, order not returned. The gap between the
first and the last can be wide, and its size in your own data is worth measuring once; the choice
belongs in the definition rather than in whoever built the query.

**3. Write the denominator as a population with a moment of membership.** Recipients at send
time, delivered messages, openers, entries into a flow, customers active at the start of the
period. **The denominator is where most disagreements live**, and it is also where a metric
breaks most quietly: conversion against clicks and conversion against delivered messages are
different metrics wearing one name.

**4. Fix both windows.** The measurement window says what period the number covers. The
attribution window says how long after a touch an action still counts as connected to it. Then
say how a window that crosses the period boundary is handled. If each touch books its conversion
into the touch's own period, one order lands in two periods whatever the window length: a send on
the last day of one period and a send on the first day of the next can both claim it. The
timestamp rule in step 5 is what prevents that.

**5. Give the conversion an identity, then say how you split the credit.** A window length is not
a deduplication rule. Two sends go out on the thirtieth and the thirty-first, each carrying a
three-day attribution window. Both can claim one order placed on the first of the next month, and
both windows are shorter than the reporting period. Fix five things: the key that identifies one
conversion, which is the order id and not a row in a report; whether more than one touch may claim
one conversion; whether the weights across touches sum to one; how a tie is broken when two touches
have an equal claim, such as two channels delivered to one person inside one window with no click
on either; and which timestamp decides the reporting period the conversion falls into. Late events and returns belong in the same paragraph,
because both arrive after somebody read the report.

Then say whether a reader may add the channel figures together. If they sum above the
deduplicated total, write that where you publish the numbers. Non-additive reporting is a
legitimate choice and an expensive accident, and the only difference between them is whether you
declared it.

**6. Name the attribution method and the system of record.** Not the correct method, the applied
one. A share quoted without its method compares to nothing, including its own value from last
period if the method changed in between. Choosing between models belongs to `crm-reporting`;
naming the one in force belongs here.

**7. List the exclusions.** Test and internal accounts, employees, wholesale orders, returns and
partial refunds, canceled orders, shipping and tax inside the order value, currency and the rate
date, duplicate profiles of one person. Each one you leave unstated becomes a difference between
two reports later.

**8. Name the unit of count and whether it is unique.** People, profiles, orders, messages;
unique opens or all opens. A metric missing this line changes value the first time the platform
updates how it counts.

**9. Set the refresh cadence and the freeze rule.** Numbers keep settling: late orders, returns,
delayed conversions, offline data arriving on its own schedule. Say how long a value stays
provisional and when it stops moving.

**10. Write it where the numbers live.** The register row, and the tooltip on the chart, carrying
the owner and the version date. A definition that lives in a thread is not a definition; whoever
reads the chart in six months will not be in the thread.

## Thresholds and timings

- **Attribution window shorter than the reporting period**, so that a period's credit is not
  carried by the touches of the period before, and the figure settles within one window of the
  period's close. The window prevents no double counting, across periods or inside one: the
  conversion key and the timestamp rule in step 5 do that. Where the
  category's decision cycle is longer, furniture and travel being the standard cases,
  lengthen the period to fit the window rather than shortening the window to fit the calendar.
- **A conversion key before any channel comparison.** Until one order carries one identifier
  across the reports you are comparing, a channel breakdown is a list of claims rather than a
  split of a total.
- **The measurement window comes from the category's purchase cycle**, not from the calendar. A
  monthly retention figure in a category people buy from once a year measures noise.
- **A minimum denominator for publishing a rate.** On a small denominator a percentage swings by
  tens of percent on a single order. Derive the floor from your own dispersion: the group size at
  which one extra case cannot move the value outside the normal variation of one reporting period.
- **The provisional period** adds up every clock that still changes the number: the attribution
  window where a conversion is dated by its touch, since a touch on the period's last day keeps
  collecting orders for that long; the category's return window on each of those orders; and
  however long offline data takes to arrive.
- **Review a definition on an event, not on a schedule:** the platform changed, the attribution
  method changed, the assortment or the business model changed.

## Edge cases

- **One metric, several published formulas, and one of them broken.** Retention rate is the
  teaching example. "(customers at end minus new) / customers at start" and "returning customers /
  customers at start" produce different numbers on the same data, and both circulate; the first
  one also turns negative whenever enough of the newly acquired customers leave before the period
  closes, because it subtracts them from the closing count anyway. Pick a formula, check it
  against a case where the answer is already known, and record the others as known variants you do
  not use. `customer-metrics.md` carries the worked case and the cohort form that survives it.
- **The denominator can be empty.** A cohort with no members, a period in which nobody was
  eligible, a channel you addressed nobody in. The rate is `not defined`, and you write that into
  the definition in advance. A zero in that slot reads as a measured outcome, and somebody acts on
  it: nobody churned, nothing was lost, the rule is safe.
- **Opens are no longer a clean measurement.** Mail clients that prefetch images turn some opens
  into machine events. Metrics built on opens stay directional: read CTOR next to CTR rather than
  instead of it, and say so in the definition rather than quietly trusting the number.
- **One person, two profiles.** Until stitching is done, a denominator labeled "people" counts
  profiles. Write that in the definition; a reader who assumes people will compare your number
  to someone else's people.
- **Offline purchases without identification.** Part of the numerator is physically unobservable.
  Publish the share of unidentified transactions next to the metric, or it will read as precise.
- **Multiple currencies and partial refunds.** The rate date and the treatment of a partial refund
  belong in the definition, not in an accounting convention nobody in marketing has read.
- **The definition changed mid-period.** The series breaks. Comparison with the previous period is
  invalid even when the value looks similar. Mark the break where the numbers live. `segmentation`
  applies the same rule to a changed segment.

## Failure modes

- **Two dashboards, two values, and an argument about which tool is wrong.** The tell: nobody in
  the room can state either denominator inside a minute.
- **The metric has no owner.** Nobody calls it wrong because nobody calls it theirs.
- **The metric only moves when the definition moves.** Usually visible as a step change on the
  date of a platform release rather than on anything a customer did.
- **A number quoted with no window.** A conversion rate stated without a period and an attribution
  window is a remark, not a measurement.
- **An average over a base that is not homogeneous.** One number for the whole base hides two
  segments moving in opposite directions, which is why it cannot settle an argument about either.
