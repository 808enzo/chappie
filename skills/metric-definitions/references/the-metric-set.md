---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# The metric set: register, control metric, changing a definition

Metrics arrive one at a time, each with a good reason, and nothing ever removes one. After a year
a program reports on thirty numbers, several of them the same number under different names, and
the review meeting is spent explaining the movements rather than deciding anything.

This mechanic is the set: what is in it, which number the program is accountable for, what
protects that number from being gamed, and what happens when a definition has to change.

## Entry conditions

- More than a handful of metrics are in regular use, or more than one team reports on the same
  program.
- A definition is about to change, or a metric is about to become a target.

## Exit conditions

A register exists: metric, link to its definition, owner, system of record, consumer, cadence.
Owner here means whoever owns the definition: the person who may change what the number means and
who is asked when two systems disagree. Whoever is answerable for making the number move is a
different role, held in `crm-program-design`, and the two are separated on purpose: a metric whose
definition and whose target sit with the same person can be hit by redefining it.
Each program area has one control metric with guardrails named next to it. A written protocol
covers changing a definition, and every metric in the set has a self-baseline or says "no base yet"
with the date it will have one.

## Sequence

**1. Take the inventory.** One row per metric: the definition it points to, who owns it, which
system it comes from, which decision consumes it, the cadence it is read at. The first inventory
reliably turns up metrics with no consumer and two metrics with one name in different reports.

**2. Name one control metric per program area.** A list of control metrics is the absence of a
control metric. The rest are read metrics: you look at them during a diagnosis, you do not report
against them. `email-program`, `triggered-messages` and `segmentation` each name their own; this
skill supplies the formula, not the choice.

**3. Put guardrails next to it.** A metric named as a target starts being grown any way it can be:
opens by clickbait, rates by deleting the inactive part of the base, revenue per message by
sending only to the most responsive people. A guardrail is the metric that is not allowed to
deteriorate while the control metric improves. The usual set: unsubscribes, complaints, margin,
reach.

**4. Cap what goes into the regular review.** Everything else lives on request. A number nobody
can act on this cycle does not need to be in the room.

**5. Retire metrics with no decision behind them.** Same test as step one of
`writing-a-definition.md`, applied to a set that already exists. Nothing else shrinks the set,
because adding a metric has an owner and removing one does not.

**6. Write the definition-change protocol.** Version, effective date, whether history is restated
or the break is marked, who gets told, and which kind of change it is: a correction of what the old
version computed, a change of question, or both, recorded as two versions. A correction keeps the
outgoing version computable until `crm-reporting` has re-read the last conclusion published under it.
A change of question reopens no conclusion, so nothing waits on it: the outgoing version stays
computable through the cycle in which the break is marked, and retires at its end. Restating history
silently is the worst of the options: it destroys the only way anyone could notice that something
changed.

**7. Build a self-baseline instead of a market number.** Take eight to twelve completed periods as a
starting point, compute the median and the spread, and state in advance what movement counts as signal and what
counts as noise. This is the standing answer to what is normal for any metric in the set: this
library carries no market benchmark. The spread is the band from the lowest to the highest of those
periods. Read each new completed period against it with the signal rule:

- a period inside the band, an edge value included, is noise;
- one period outside the band is a flag. It says nothing yet about the work: check the data and the
  base (`reconciling-across-systems.md`; The base grew or was cleaned, under Edge cases) and wait for
  the next period. If the check explains the flag (a counting artifact or a change of base), the
  flag starts no pair: remove the cause, then read the series again;
- two periods in a row beyond the same edge, both read against the band in force at the first of
  them, are a signal.

Once the band exists, write the rule with its false-alarm rate for your own n beside it (Thresholds
and timings), so whoever reads the next period knows how often the rule fires when nothing has
changed. Asked what is normal before that, give the rule and its formulas, not a figure for some
other n.

**8. Do not fit an outside benchmark to your own definition.** A market figure is usable only
together with the numerator, denominator and window its source used. A matching metric name
guarantees none of the three.

## Thresholds and timings

- **Eight to twelve completed periods for a self-baseline, as a starting point.** Fewer and the
  spread is unreadable; many more and you are averaging across a program that has changed. Revise
  it on your own series: shorten the span where the program changed inside it, lengthen it where
  the spread still moves as periods are added.
- **The signal rule's false-alarm rate follows from the ranks.** With n periods in the band and
  nothing changed in the work, each of the n + 1 periods is equally likely to be the lowest, so a
  new period falls below all n in 1/(n + 1) of periods, and a flag on either edge fires in
  2/(n + 1). Any two of the n + 2 periods are equally likely to be the two lowest, so two new periods
  both fall below all n in 2/((n + 1)(n + 2)) of periods, and a signal on either edge fires in
  4/((n + 1)(n + 2)). With twelve periods, that is 2 in 13 for a flag and 4 in 182, about 1 in 45,
  for a signal; with eight, 2 in 9 and 4 in 90, about 1 in 22. One edge alone halves both. These are
  rates per period: on a monthly metric with twelve periods in the band, a false signal fires about
  once in four years on average. They are averages over all the bands you could build; the rate of
  any one band runs above or below them.
- **What the rates assume.** They hold for any shape of distribution, but only while the periods are
  independent and share one level, with no trend, no season and no period pulling the next one its
  way. Where values repeat at the edges (counts, rounded rates), an edge value is noise and the
  rates become ceilings. Where a period pulls the next one its way, both periods of a pair drift
  together and the signal fires more often than these rates say: name that condition beside the
  rate, and do not compute a corrected figure. Where the metric has a season, read each period as
  its ratio to the same period of the previous seasonal cycle (Seasonality against trend, under Edge
  cases), and build the band from the same ratio over earlier periods; building that band takes n
  periods plus one full seasonal cycle of the version in force. The rates change with n, so compute
  them for your own n: a figure for another n does not carry over.
- **Two periods in a row is a starting point.** It cuts the false-alarm rate to 2/(n + 2) of the
  flag's, a fifth at eight periods and a seventh at twelve, at the cost of at least one period of
  delay, and more delay where a shift is small enough that a shifted period still lands inside the
  band now and then. Where a late catch costs more than a false alarm, act on the flag and state its
  rate. Where a false alarm costs more, require three periods in a row and work out that rule's rate
  the same way. Choose the rule first, then compute its rate.
- **The band stays fixed between rebuilds.** Rebuild it at the review of the set, not every period,
  and not while a flag waits for its second period. A band rebuilt every period from the latest n
  periods takes in the shifted periods and moves its own edge toward them, so a shift that does not
  produce a pair at once is caught later or not at all.
- **One control metric per program area**, not per company: a channel program, an automated flow
  layer and a loyalty program are accountable for different things.
- **Review the set at the cadence of the decisions it serves**, and no faster.
- **A definition version lives until the measurement method changes.** A version without a date is
  not a version.
- **Restate or mark the break within one cycle** of a definition change, as a starting point,
  while the people who remember it are still available. Lengthen it only where the restatement
  needs data that has not landed yet, and say so on the break marker.

## Edge cases

- **The metric became a target and stopped being a measurement.** Test it by asking whether the
  number can be improved without improving the work. If it can, it needs a guardrail beside it
  before it goes on anyone's objectives.
- **Seasonality against trend.** In a seasonal business, comparison with the previous period
  misleads almost every time. Compare with the same period of the previous cycle, and write that
  into the definition so it survives whoever builds the next chart.
- **The base grew or was cleaned.** Every rate moves without any change in the work. Publish base
  size next to any rate.
- **Adoption metrics.** Money saved by consolidating tools, time to launch a campaign, hours of
  routine removed. A legitimate class, and useful during a migration, but they measure the
  rollout rather than the result for a customer, and they do not make good control metrics.
- **A metric only one person can compute.** It is honest until that person takes leave. Either
  automate it or accept it as a diagnostic rather than a reported number.
- **Two teams need the same metric with different denominators.** That is two metrics. Give them
  two names, or you will be reconciling them forever.

## Failure modes

- **Everyone has a dashboard, nobody has a definition.** The tell: the same metric name, different
  values, and nobody surprised by it.
- **The set grows and nothing is retired.** The same shape as the flow set in
  `triggered-messages`: adding has an owner, removing does not.
- **Comparison against a benchmark from someone else's method.** A number "in line with the
  industry" whose denominator you cannot state is the most expensive form of self-deception,
  because it looks like working from data.
- **History was restated silently.** The tell: the old charts changed and nobody can name the date
  it happened.
- **The control metric improved and the business did not.** Usually a missing guardrail: the
  improvement came from a narrower base, a cleaned list, or a definition that quietly moved.

## Worked example (made-up numbers)

This section runs step 7 on one rate, and every number in this worked example is made up. It builds
the self-baseline and, from the same periods, the minimum denominator of `writing-a-definition.md`.

**Input schema.** One row per reporting period, from the report the metric's definition names as its
system of record.

| Field | Type | What it holds | Where it comes from |
|---|---|---|---|
| `period` | month, ISO | the reporting period | the definition's period |
| `version` | integer | the definition version in force for the period | the register row's version history |
| `denominator` | count | delivered messages of the period's campaign sends | the sending platform |
| `numerator` | count | unique clickers of each send, added up over those sends | the sending platform, after each send's collection window |
| `status` | completed or provisional | completed once the last send's collection window has closed | the definition's provisional period |
| `rate` | percent, two decimals | numerator over denominator | computed per period, never averaged across periods |

**Data.** In this worked example the metric is the click rate of campaign sends, version 2 counts
unique clickers where version 1 counted every click, the collection window is seven days, and the
baseline is built on 2026-08-10, once July has closed.

| `period` | `version` | `denominator` | `numerator` | `status` | `rate` |
|---|---|---|---|---|---|
| 2025-09 | 1 | 38,400 | 2,074 | completed | 5.40% |
| 2025-10 | 1 | 39,100 | 2,197 | completed | 5.62% |
| 2025-11 | 2 | 40,200 | 1,576 | completed | 3.92% |
| 2025-12 | 2 | 41,500 | 1,702 | completed | 4.10% |
| 2026-01 | 2 | 40,800 | 1,514 | completed | 3.71% |
| 2026-02 | 2 | 41,200 | 1,586 | completed | 3.85% |
| 2026-03 | 2 | 42,000 | 1,768 | completed | 4.21% |
| 2026-04 | 2 | 42,300 | 1,684 | completed | 3.98% |
| 2026-05 | 2 | 41,900 | 1,525 | completed | 3.64% |
| 2026-06 | 2 | 42,600 | 1,725 | completed | 4.05% |
| 2026-07 | 2 | 43,100 | 1,672 | completed | 3.88% |
| 2026-08 | 2 | 56,400 | 1,867 | completed on 2026-09-07 | 3.31% |
| 2026-09 | 2 | 18,900 | 397 | provisional | 2.10% |

**Steps on the worked example:**

1. Keep the completed periods of the version in force. 2025-09 and 2025-10 count another numerator,
   so drop them: pooled in, they would lift the median to 3.98% and stretch the top of the band to
   5.62%. 2026-09 is still inside its collection window, and its rate will rise until the window
   closes.
2. Take the span: 2025-11 to 2026-07, nine completed periods, inside the starting point of eight to
   twelve. 2026-08 has not closed on the day the baseline is built, so it becomes the first period
   read against it.
3. Median of the nine period rates: 3.92%.
4. Spread: the lowest period, 3.64%, and the highest, 4.21%. That range is the band.
5. Write the rule before the next period closes: a completed period inside 3.64% to 4.21% is noise,
   one outside it is a flag, and two in a row below 3.64%, or two in a row above 4.21%, are a signal.
   With nine periods in the band, a flag fires by chance in 2 in 10 periods and a signal in 4 in
   110, about 1 in 27.
6. Minimum denominator. One clicker more or one fewer moves a rate on n delivered messages by 1/n, up
   or down, so the nearer edge of the band sets the floor. From the median, that edge is 3.92% minus
   3.64%, 0.28 points, so 1/n stays under 0.0028 only when n is above 357.1: the floor is 358 delivered.
   Publish a send with fewer as counts, not as a rate.

**What it returns in this worked example:** a register line that reads click rate, version 2, median
3.92%, band 3.64% to 4.21%, built from 2025-11 to 2026-07, minimum denominator 358, flag 2 in 10,
signal 4 in 110. August closes at 3.31%, below the band: a flag, not yet a signal. Its denominator
grew from 43,100 to 56,400, so check the base before the work (The base grew or was cleaned, under
Edge cases). If the check finds no artifact and September also closes below 3.64%, August and
September together are a signal. September's last send goes out on 2026-09-30, so its collection
window closes on 2026-10-07. Until then its rate is provisional: do not read it against the band.
This example assumes the rate has no season; where it has one, compare with the same period of the
previous seasonal cycle.

**When the data is too little.** Fewer than eight completed periods of the version in force is too
little: eight is the low end of the starting point in Thresholds and timings. The procedure then
returns "no base yet" with the date the eighth period closes, and nothing it would have computed: no
median, no band, no flag or signal, no minimum denominator, since the floor comes from the spread.
Until that date, publish each period's rate with its denominator beside it. In this worked example,
had version 2 started on 2026-03-01, the register on 2026-08-10 would hold five completed periods
and read "no base yet, 2026-11-07": October is the eighth period, its last send goes out on
2026-10-31, and the collection window closes seven days later.
