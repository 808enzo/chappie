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
covers changing a definition, and every metric with no citable benchmark has a self-baseline or
says "no base yet" with the date it will have one.

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
counts as noise. This is the standing answer when no citable benchmark exists, which for most
lifecycle metrics is the normal state rather than a gap.

**8. Do not fit an outside benchmark to your own definition.** A market figure is usable only
together with the numerator, denominator and window its source used. A matching metric name
guarantees none of the three.

## Thresholds and timings

- **Eight to twelve completed periods for a self-baseline, as a starting point.** Fewer and the
  spread is unreadable; many more and you are averaging across a program that has changed. Revise
  it on your own series: shorten the span where the program changed inside it, lengthen it where
  the spread still moves as periods are added.
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
