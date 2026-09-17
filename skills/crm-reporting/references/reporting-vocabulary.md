---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Vocabulary of reporting

The three mechanics assume these terms. Four of them are units. When two people disagree about a report, check
first whether one of them means the line and the other the conclusion drawn from it. Several words here are shared with neighbors, and those are marked at the end.

## The units

**Report line.** One metric, on one population, for one period, carrying its comparison base, its counterweight
where the vanity register requires one, its freeze date and its definition version. The unit of construction.

**Page.** The set of report lines for one reader and the decision that reader takes.

**Reader.** The person who takes a decision on a page.

**Cohort.** The people who entered through one identifying event in one period, read by age. The analytical unit
`segmentation` hands to this skill. The specific cohorts are defined by neighbors: arrival, first purchase,
install, attempt.

**Conversion and its credit.** One conversion identified by its key (`metric-definitions`), and the share of
credit each touch receives under the model. The unit of money.

**Conclusion.** The category a published report gave a line against its comparison base: above, below, or
within the noise band. One per line per published report. The unit of the control metric.

## Lines and conclusions

**Comparison base.** What a line is compared with: the plan or goal, the line's noise band, the same period of
the previous cycle, or a control group. One per line, written into the line's definition, and chosen by the
question the line answers.

**Noise band.** The spread of a line across its own stable periods, set before publication. Against a plan it is
the tolerance written into the definition; against a control group, the interval from the test read. Not the
amplitude band of `promo-calendar` and not a band on an axis in `rfm-segments`.

**Above, below, within.** The three categories of a conclusion.

**Freeze date.** The date after which a line's value stops moving under the freeze rule of its definition
(`metric-definitions`): the end of the period plus the provisional period. Not the freeze window of
`promo-calendar`, the span in which nothing in the stack changes.

**Provisional line.** A line before its freeze date. It carries a conclusion.

**Re-read.** Recomputing a line on its freeze date under the definition version in force when it was published.

**Re-read deadline.** The next publication of the page that carries the line after its freeze date. A re-read
recorded later, or one that cannot be computed, leaves the conclusion not held with the cause not re-read.

**Held, not held.** The outcome of a re-read. A conclusion did not hold when the re-read gave another category or
when no re-read was recorded by the re-read deadline. The causes are settling (late data, returns, immature
cells), error (a join, an export, a broken definition), attribution (the control group read at the freeze date
gave another category than the provisional one), and not re-read.

**Held share.** The control metric: held conclusions over all conclusions that have been re-read or whose re-read
deadline has passed. Each row of a breakdown and each counterweight carries a conclusion of its own; a line with
no base yet carries none.

**Report snapshot.** A published report, with its date, that is never edited. Not the snapshot `list-building`
takes of two records before a merge.

**Restatement note.** A line in the next report that corrects a published one: the line, the conclusion as
published, the corrected conclusion, the cause.

**Slice.** A breakdown no decision depends on. It lives in the on-request view. A cut that changes what somebody
gets is a segment (`segmentation`).

**On-request view.** Where slices and retired lines live, outside the pages.

**Counterweight.** The number that stands in the same row as a vanity metric and shows what that metric hides.

**Vanity metric.** A number that improves or holds while the work it is quoted for gets worse, by construction of
its numerator or denominator. The register is `vanity-metrics.md`.

**Check against the whole.** Channel money lines against deduplicated attributed revenue, and that figure against
revenue in accounting, before publication.

**Break marker.** The mark on a timeline where a definition version changed. Values on either side do not
compare.

## Cohorts

**Entry event.** The event that puts a person into a cohort. It has to identify the person.

**Age.** Time since entry, in the unit of the cohort period.

**Cell.** One cohort at one age. A *cumulative* cell is the share that took the action by that age and never
falls; an *interval* cell is the share that took it within that stretch of age.

**Maturity.** A cell is final once its age and every span that settles it have run out for the whole cohort; until
then it is immature.

**Cohort tag.** Entry point, acquisition source, platform, and the occasion tag from the `promo-calendar` register.

**Mix, within-cohort change.** The two parts of a base-wide change: the part explained by a different weight of
ages in the base, and the part left when last period's age weights are applied to this period's rates at each
age.

**Gap line.** Arrivals against entries into the first mechanic, per entry point: the silent loss of
`welcome-and-activation`, shown under the cohort table.

**Stage share.** People of the cohort who reached a stage by a given age, over the cohort. Not the conversion from
the previous stage.

## Money

**Credit, cause.** The two questions a money line can answer: how much came through a channel, and how much would
not have come without it.

**Attribution model.** The rule that gives credit to touches. Its choice is made here, per decision; its name in
force is written into the definition (`metric-definitions`).

**Attribution window.** How long after a touch a conversion still counts as connected to it
(`metric-definitions`). Derived here from your own lags against untouched people.

**Anchor.** The event a window starts from: the send (or delivery), the read or display receipt, or the click.
The narrowest signal the channel records; one anchor for every channel competing for a budget.

**Double credit.** The sum of the claims channel tools make, minus the deduplicated total, net of claims the
model rejects. Not an overlap in the sense of `segmentation` and `scenario-map`, where overlaps are between
segments and between mechanics.

**Unidentified share.** The share of revenue with no identified person, and on the website the share of sessions
without consent to analytics.

**Assisted conversion.** A conversion credited to another channel with a program touch inside the window before
it. Never added to direct credit.

**Incremental figure.** The difference against a control group, read with its interval and read date
(`experiments-and-holdouts`; incremental revenue in `metric-definitions`).

**Attribution multiple.** Attributed revenue divided by incremental revenue, on the same population for the same
period, per channel.

## Words shared with neighbors

- **Window** carries a qualifier across this library, and a report meets these: the attribution window (`metric-definitions`, and here), the
  promotional window and the extended window (`promo-calendar`), the cohort window (`repeat-purchase`), the
  attempt window (`lapse-and-winback`). This skill never uses the word without its qualifier.
- **Freeze:** the freeze rule of a definition (`metric-definitions`, and the freeze date here) against the freeze
  window of `promo-calendar`.
- **Band:** the noise band here, the amplitude band in `promo-calendar`, a band on an axis in `rfm-segments`.
- **Snapshot:** the report snapshot here against the pre-merge snapshot in `list-building`.
- **Read cycle, revision cycle, zero point:** `crm-program-design`.
- **Guardrail:** `metric-definitions` and `experiments-and-holdouts`.
