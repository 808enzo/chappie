---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Reading cohorts: the table by age, cell maturity, mix

The unit here is **the cohort**. Here you read change over time without mistaking a change in
the makeup of the base, or cells that have not matured, for a change in behavior. Neighbors define the specific
cohorts: the arrival cohort (`welcome-and-activation`), the first purchase cohort (`repeat-purchase`), the
install cohort (`push-notifications`), the attempt cohort (`lapse-and-winback`). This file is how you build a
table of them and read it in the report.

## Entry conditions

A rate across the whole base (repeat purchase, retention, engagement, return) is used to judge whether things
are getting better; or the volume or the source of inflow changed; or a peak recruited many new people.

## Exit conditions

A cohort table for every question the business asks over time, read by age. Every cell marked final or
immature. Base-wide changes split into mix and within-cohort change. Cohorts tagged by entry point, source and
occasion.

## Steps

**1. Name the question and the entry event.** One table per question. Take the cohort from the skill that
defines it; do not redefine it here. The entry event has to identify the person at the moment of entry: an
anonymous visit forms no cohort, because one person on two devices sits in it twice, so use the first event
that identifies the person.

**2. Fix the denominator at entry.** Everybody who entered in the period, including the people no channel could
reach, the people the frequency cap suppressed and the control group. Take out only the people whose entry was
revoked, such as a first order that came back. Never re-base the denominator on the people still active: that
builds a table of survivors.

**3. Choose the cohort period.** No shorter than the period in which a cohort reaches the minimum denominator
(`metric-definitions`), and no longer than the cadence of the decision that reads the table. If both cannot
hold, merge periods and say so on the table.

**4. Lay the table out by age, not by calendar.** Rows are cohorts; columns are the age since entry, in the unit
of the cohort period. A cell is the share of the cohort that took the action by that age (cumulative) or within
that stretch of age (interval). Write which one in the header: a cumulative cell never falls, and an interval
cell does.

**5. Mark each cell's maturity.** A cell is final once, for the whole cohort, its age has passed and so has every
span that settles it: the return window on the entry and the return window on the counted action, which with
the cohort window are the three spans of `repeat-purchase`, plus the lag of offline data from the freeze rule
of the line's definition. Show an immature cell as immature: not blank, which reads as zero, and not as an
unmarked partial value. Never compare a partial cell with final cells at the same age.

**6. Tag every cohort.** Entry point, acquisition source, platform, and the occasion tag when the entry fell
inside a promotional window (the register of `promo-calendar`). Read tagged cohorts on rows of their own: a
cohort recruited in a sale is not the program getting worse.

**7. Compare at equal age, against the spread of earlier cohorts at that age.** A change is a cohort whose cell
at age k falls outside the band of the earlier stable cohorts at age k. A comparison of calendar months mixes
ages.

**8. Split a base-wide change before it goes into the report.** A base-wide rate is the weighted average of the
rates at each age, weighted by the share of the base standing at that age. Recompute the current period with
last period's age weights: the difference between the actual rate and the reweighted one is mix, and the rest
is change within cohorts at equal age. Weights go by age, not by cohort: the cohort that entered this period had
no weight last period, while age zero always had one, and a cohort compared with itself one period older reads
aging as change. Close the table with an open last age (k and older) so both periods hold the same set of ages.
When mix explains the movement, write that on the report line, and keep the base-wide rate as a slice
(`vanity-metrics.md`).

Take a worked example with invented numbers. Last year, 5,000 customers made their first purchase in the year
(age zero) and 20% of them bought again (1,000 people); 5,000 customers from earlier years (age one and older)
bought again at 60% (3,000 people). The base-wide share was 4,000 over 10,000, or 40%. This year acquisition was
cut: 2,000 new customers, again at 20% (400 people), and 10,000 customers at age one and older, last year's
newcomers now among them, again at 60% (6,000). The base-wide share is 6,400 over 12,000, about 53.3%. Weighted
half and half, as last year, this year's rates give 40%: the change within cohorts at equal age is zero, and all
13.3 points of the rise are mix.

**9. Show the gap line.** Arrivals against entries into the first mechanic, per entry point, on a line of its
own under the table: the silent loss of `welcome-and-activation`. A report on a flow cannot see it by
construction, and a report on the base dissolves it into a total.

**10. Count stages on the cohort, not on the survivors of the previous stage.** A stage share is the people of
the cohort who reached the stage by age k, divided by the cohort. A sequential funnel drops everybody who skipped
a stage (an order placed without a cart, a visit booked without a call) and reads the next stage's conversion on
survivors. Show step conversion only beside the shares on the cohort. When the cycle is long, read each stage at
the age where it settles on your own distribution of time from entry to that stage: early stages settle earlier,
and the final stage later.

**11. Treat a transition between behavioral groups as an occasion, not a report line.** Show movement between
groups only where a mechanic acts on the transition, as entries into that mechanic. Group sizes are not program
health (`rfm-segments`).

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Cohort period | no shorter than the period that reaches the minimum denominator; no longer than the decision's cadence | parameter |
| Maturity of a cell | the cell's age plus the spans that settle it: return windows, the lag of offline data | follows from the definition |
| Band at age k | the spread of earlier stable cohorts at age k | parameter |
| Age at which a stage is read | the point where your own distribution of time to that stage levels off | parameter |

## Edge cases

- **A category bought once every few years.** A second purchase takes years to appear. Read the early stages, and
  whatever replaces repeat purchase for the program (`crm-program-design`, edge cases).
- **A cohort too small to read.** Merge adjacent periods and keep the tags.
- **The definition changed in the middle of the table.** Start a new table on the date of the change and do not
  splice. Recompute earlier cohorts under the new version only through the restatement protocol, and mark them.
- **History cut short by a migration or incomplete stitching.** Mark the cohorts that entered before stitching
  was complete (`martech-stack`, `list-building`).
- **A person enters again** (a second arrival, a reinstall). The neighbor's rule decides who that is: the second
  entry in `welcome-and-activation`, the reinstall in `push-notifications`. Show re-entries on a line beside the
  table.
- **A return revokes an entry after the table was published.** Every cell of that cohort's row changes, and it
  changes before the row's freeze date: the return window on the entry is one of the spans that settle it
  (step 5), and the provisional mark in `regular-report.md`, step 7, covers it.
- **A cohort recruited at a peak falls under a later window.** `promo-calendar` settles the overlap (step 8 of
  `seasonal-shape.md`); read that cohort on its own row.

## Failure modes

**"The newer cohorts are worse."** The lower rows sit below the older ones in later columns because their cells
are immature. Sign: the gap closes as the months pass. The remedy is step 5. **A second cause shows the same
sign:** the source of inflow changed. Sign: the gap holds on final cells and concentrates under one source tag.
Check maturity to tell the two apart: on an immature cell, wait for the freeze date; on a final cell, read by tag.

**The base-wide rate improves as inflow falls.** Signs: the base-wide rate rises, every cohort at equal age stays
flat, and the number of people entering new cohorts drops. The remedy is step 8.

**A table of survivors.** The denominator was re-based on active people, and the retention curve comes out flat.
Sign: cohort size shrinks from column to column. The remedy is step 2.

**Sale cohorts pooled.** One cohort drops, and it turns out to be the peak's. Sign: the occasion tag. The remedy
is step 6.
