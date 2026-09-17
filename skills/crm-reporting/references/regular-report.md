---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# The regular report: lines, comparison bases, counterweights, freeze dates

The unit here is **the report line**: one metric, on one population, for one period, carrying its comparison
base, its counterweight, its freeze date and its definition version. Here you decide what stands on a page,
what each line is compared with, what stands beside it, when its conclusion is final, and what happens when
something published was wrong. `metric-definitions` owns what a metric means; change over time is
`cohort-reading.md`; money is `attribution-and-money.md`.

## Entry conditions

The program reports to the business on a schedule; or somebody asks for a CRM dashboard; or a report exists
and nobody takes a decision on it.

## Exit conditions

A page per reader. Every line carries a decision, a comparison base, a counterweight where the vanity register
requires one, a freeze date and a definition version. A re-read log. A check that runs before every
publication. An archive of dated snapshots, and a rule for restatement notes.

## Steps

**1. Start from decisions: one page per reader.** List who reads, which decision each of them takes, and how
often: the business (the goal and the budget), the program owner (the build queue, verdicts on mechanics),
channel and mechanic owners (diagnosis). A page holds only lines its reader decides on. A number requested
with no decision behind it is a slice: it lives in an on-request view, not on a page. A page runs at the
cadence of its decision and never faster than the read cycle (`crm-program-design`): a report faster than
the decision it serves produces nothing but movements somebody has to explain.

**2. Put the program's numbers at the top of the business page.** The program's target metric and its
balancing metrics (`crm-program-design`), then each program area's control metric with its guardrails
(`metric-definitions`). Everything else goes lower or onto another page. The unclaimed share of
`crm-program-design` is a design instrument: it belongs in the pack for the program's revision cycle, not on
the regular business page. Duty signals from `program-audit-and-ops` do not appear on the page; an annotation
appears when an incident changed a published number.

**3. Give every line a comparison base written into its definition, not chosen when you publish.** The base
follows from the question the line answers:

- did we do what we planned: the plan or the goal;
- is this unusual: the line's own noise band, from its self baseline;
- is this the season: the same period of the previous cycle, and for a period that holds a promotional window,
  the extended window and the pair of periods (`promo-calendar`);
- did the program cause it: the control group (`experiments-and-holdouts`).

One base per line. Two questions about one metric make two lines. Changing a line's base is a change of
definition and goes through the protocol in `metric-definitions`. A new line with no history says "no base
yet" and the date it will have one, and it states no direction.

**4. Write each conclusion as a category against the base: above, below, or within.** The noise band is the
spread of the line across its own stable periods, set before publication (`metric-definitions`, the metric set,
step 7). Against a plan, the band is the tolerance written into the line's definition; against a control
group, it is the interval from the test read; against the same period of the previous cycle, it is the spread
of that same comparison across earlier cycles, and with no such history the line's own noise band, marked on
the line. No adjectives: "strong growth" is not a category.

**5. Put every rate beside the count and the base it stands on, every share beside its total, and every metric
in the vanity register beside its counterweight, in the same row.** The register is `vanity-metrics.md`. "The
same row" is literal: whoever copies the row into a screenshot or a slide copies the counterweight with
it. Beside every rate computed on sends, show the absolute count of what the business wants
(orders, people, margin): a rate on sends improves when you stop sending to the people least likely to respond.

**6. Keep apart what must not be pooled.** Indices normalized within a row, such as the provider response index
of `deliverability` and the environment click index of `email-design`, are shown row by row and never averaged:
averaging removes the one thing the index shows. Control metrics that their skills read per threshold step, per
entry point, per platform, per brand or per market (`lapse-and-winback`, `welcome-and-activation`,
`push-notifications`, `crm-program-design`) are shown that way; a pooled figure is allowed only as an on-request
slice. Channel figures add up only where the definition declares them additive (`metric-definitions`).

**7. Give every line a freeze date and mark it provisional until then.** The freeze date is the end of the
period plus the provisional period from the freeze rule of the line's definition: the return window, the lag of
offline data, the cohort window, the read date of a holdout. A provisional line still carries a conclusion; the
mark tells the reader the conclusion can still move.

**8. Check before you publish.**

- **Sum against the whole.** Three equalities. The period's revenue in the order data behind the report sits
  within the reconciliation tolerance (`metric-definitions`, reconciling across systems) of the period's revenue
  in accounting: that is the completeness check on the data. Channel money lines sum to the deduplicated attributed
  revenue, which is no more than the period's revenue; the remainder is a line of its own, not attributed.
  Where the page shows the claims of channel tools, their sum minus the deduplicated total is the double credit
  line (`attribution-and-money.md`, step 7).
- **Freshness.** Every source has rows dated through the end of the period; a load that ran and brought nothing
  is not fresh (fresh rows arriving is that source's heartbeat in `program-audit-and-ops`). A stale source
  takes its lines off the page with a note; do not publish them on old data. The failed export goes to
  `program-audit-and-ops`.
- **Rows behind a money line.** Open a random sample of the orders credited to the line and confirm that each
  exists, is not canceled or returned beyond the rules of the definition, and falls in the period by the
  timestamp the definition names. Take as many as one person can check in one sitting, and raise the number
  after a conclusion that did not hold because of an error.
- **Versions.** Each line's definition version matches the register; a mismatch takes the line off the page.

**9. Annotate the timeline.** The decisions taken on the previous report; definition version changes, as break
markers; incidents that changed a published number; releases of the sending platform and of web analytics;
windows from the `promo-calendar` register; holdout rotations. Without them, the next reader explains a step
in the chart with customer behavior.

**10. Publish a dated snapshot and never edit it.** A correction goes into the next report as a restatement
note: the line, the conclusion as published, the corrected conclusion, and the cause. A silent edit destroys the
only way a reader can notice that something changed, which `metric-definitions` says about restated history as
well. A conclusion published under a definition version is re-read under that version; a deliberate change of
question does not reopen it. A definition fixed because the old version computed something other than it
claimed (a filter that dropped returns, a join that doubled orders) does reopen it: re-read the conclusions
published under the broken version with the corrected one. A version that fixes an error and changes the
question at once is two versions: the old question with the error fixed, under which you re-read the old
conclusions, and the new question, which reopens nothing. The definition-change protocol of `metric-definitions` records
which kind each version is and keeps the outgoing version computable until the last conclusion published
under it has been re-read; a version that can no longer be computed leaves its conclusions not re-read.

**11. Re-read every conclusion on its freeze date.** Recompute the line, record held or not held, and name the
cause of every conclusion that did not hold: settling, error, attribution, not re-read. Schedule the
re-read from the freeze date you wrote at publication, not from an event: a re-read nobody runs emits no event.
The control metric reads this log.

**12. Retire lines nobody decides on.** A line that fed no decision across one revision cycle of the program
moves to the on-request view. Its published conclusions keep their re-read dates: retiring a line cancels no
re-read, and you read the held share of retired lines beside the control metric. A slice requested twice
for the same decision is a segment candidate; hand it to `segmentation`.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Freeze date of a line | the end of the period plus the provisional period from the freeze rule of its definition | follows from the definition |
| Noise band | the spread of the line across its own stable periods, set before publication | parameter |
| Cadence of a page | the cadence of the decision it serves; never faster than the read cycle | parameter |
| Deadline for a re-read | the next publication of the page that carries the line after its freeze date; not re-read by then counts as not held | follows from the definition of the control metric |
| Sample of orders behind a money line | as many as one person checks in one sitting; larger after a not held conclusion caused by an error | parameter |
| Retiring a line | no decision taken on it across one revision cycle | parameter |

## Edge cases

- **A period that holds a promotional window.** Compare on the extended window and on the pair of periods (the
  peak plus the trough, against the same pair of the previous cycle), not on the days of the sale
  (`promo-calendar`). Read the window's verdict on the people in the active base when the extended window opened,
  which is that skill's control metric, and that fraction leaves out people who arrived for the first time after
  the extended window began. Put what the sale did for acquisition on a line of its own; that question belongs
  to `list-building`. Count revenue at promotional prices on orders. Never count a window on sends.
- **A new program with no history.** No base exists. Lines show the zero point (`crm-program-design`) and the
  date of the first comparison.
- **"How much did CRM bring?" as one number.** Give attributed revenue with its model and window, and the
  incremental figure where a holdout exists (`attribution-and-money.md`).
- **A small base.** Below the minimum denominator (`metric-definitions`) publish the count, not the rate.
- **Two brands or two markets.** Separate lines.
- **The source of a line changed, as in a platform migration.** That is a change of definition: a break marker,
  with the migration dates from `martech-stack`.
- **A definition fixed because it was wrong.** A restatement note; the conclusions published under the broken
  version are re-read under the corrected one, and those whose category changed count as not held, with the
  cause "error" (step 10).
- **The report builds itself.** Run the checks in step 8 on every publication, whoever or whatever assembles
  the page: automation repeats an error every cycle.

## Failure modes

**The report reads as good news that is not there.** Signs: a metric from the vanity register is quoted in a
decision without its counterweight; a base-wide rate rises while cohorts at equal age stay flat. The remedy is
step 5, and the split in `cohort-reading.md`, step 8.

**Conclusions do not hold.** The held share falls. Read the cause to choose the repair: settling means you publish
before the numbers settle, so move the decision to the freeze date; error means the checks in step 8 missed
something; attribution goes to `attribution-and-money.md`; not re-read means the log has no owner.

**Everything is within the band.** The held share is close to complete and the share of conclusions within the
band keeps rising. Two causes: bands wider than the line's own spread, or a band that moves with the line
(rebuilt each cycle from the latest periods while the line trends). The remedy is a band from your own stable
periods, set once, and a change of band handled as a change of version.

**Nobody decides anything on the report.** Pages grow and the decision column stays empty. The remedy is steps
1 and 12.

**History changed quietly.** Two copies of the same past report disagree. The remedy is step 10.
