---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Reading a result and deciding

The end of a test is where value gets lost. A number moved, someone says the variant
won, and three conclusions leave the room while only one of them was measured. This mechanic is
the order of operations that keeps the conclusion the size of the evidence.

## Entry conditions

The read date has passed: the last assignment under the stop rule set before the test, plus the
outcome window, plus finalization (`test-design.md`, step 8). Or you have decided to read an
unfinished test and are prepared to say so out loud: that reading is provisional.

## Exit conditions

Validity checked before results were looked at. Significance read per metric. Every result
carries an effect, an interval and the practical threshold you read it against. The decision metric
and the guardrails read separately. The payback of the win computed. A decision made, and the
whole thing written into the test log.

## Sequence

**1. Check validity before you look at the result.** The split, leakage into the control, actual
volume against planned, the integrity of the window, and whether any definition changed mid-test.
An invalid test is not read in either direction, which is why this step comes before you see the
numbers rather than after you dislike them.

**2. Read significance per metric.** A confidence level attaches to one metric, not to a table.
The standard substitution: conversion was tested, and the conclusions cover conversion, average
order value and revenue, with the last two never checked at all. Revenue varies more than
conversion and needs its own calculation (`test-design.md`, step 6), so a test sized for
conversion is not sized for revenue.

**3. Read the comparisons you declared in the design.** With more than two arms the comparison
set is part of the design: the default is each variant against the control, and you name one of
those the primary contrast that carries the decision. Every extra comparison raises the chance that
one of them clears significance by accident. If you keep several confirmatory comparisons, name the
procedure that adjusts for their number; otherwise mark the rest exploratory and say that they
carry no decision. Three arms do not oblige you to run three pairs. Variant against variant is a
separate question, and you answer it only if you asked it before the test.

**4. Read the decision metric, then the guardrails.** Opens and clicks are diagnostics rather than
verdicts. An intriguing subject line lifts opens and drops clicks, because it brings in people the
message was not for.

**5. Place the effect against the threshold you set before the test.** "Not significant" is not
a finding on its own. It means you failed to separate the effect from zero, and it carries nothing
about whether an effect of that size would be worth having. The practical threshold answers the
second question, and it is the same number as the MDE: on the way in it sizes the test, on the way
out it bounds the reading. Its mirror in the other direction is the harm boundary, unless a
guardrail sets a tighter one. Report the effect, the interval around it, and where that interval
sits. A test sized by power against zero at the MDE lands effects near the threshold in the fourth
row almost every time; the rule written before the test for an interval that clears zero and
crosses the threshold (`test-design.md`, step 6) decides that case, not a reading made after:

| Where the interval sits | Outcome | What it licenses |
|---|---|---|
| Entirely above the threshold | A useful effect | Ship it, subject to the payback in step 6 |
| Entirely below the harm boundary | Material harm | Do not ship, and read the guardrails for how fast you unwind |
| Entirely between the two boundaries | Practically negligible | The question is closed: decide on cost alone |
| Across either boundary | Undetermined | The test did not answer the question |

An interval running from a loss of two points to a gain of five, against a threshold of one point,
lands in the fourth row rather than the third: it still holds an outcome worth having and an
outcome worth avoiding. Declining to build the change at that point is a decision under
uncertainty, and the log has to say so. Filing it as "we tested it and it does nothing" buries a
question nobody will reopen. All four outcomes stay separate from "not enough data", which is an
unfinished test rather than an outcome at all.

**6. Compute the payback of the win.** Incremental target actions times margin, against the cost
of building and maintaining the change. A significant lift that does not repay the algorithm
behind it is a no, and saying so is the difference between a testing practice and a hobby.

**7. Verify the win one step further down the funnel.** Open, click, order, paid order, order not
returned. Wins that die downstream are common enough that the check is not optional, and a result
measured on paid orders sits higher on the ladder below than the same result on placed orders.

**8. Write it into the test log.** Hypothesis, design, dates, arms, metric, result with its
interval and read date, the removals and the leaked share, decision. Once the entry is written the
reading is frozen: the assignment log has served its purpose and what survives is the aggregate.
Without the log somebody runs the same test again the next time the question comes up, and
negative results disappear first, because nobody defends them.

**9. Scale carefully.** A win in a segment is not a win on the base: a variant that loses overall
can win in the audience it was written for, and the reverse. Re-read the metric after the rollout;
without a holdout that re-read is a before-and-after comparison, so keep a standing holdout
(`control-groups-and-holdouts.md`, step 5) where the effect has to stay proven.

## The evidence ladder

Use it on your own results and on anyone else's:

| Level | What stands behind the conclusion |
|---|---|
| 0 | Before and after: two periods compared, no control |
| 1 | A comparison against a control nobody randomized: matched stores, cities or cohorts |
| 2 | A comparison against a randomized control: an A/B test or a holdout, one hypothesis per test, including clusters such as locations randomized in the order of a rollout |

Random assignment moves a comparison up the ladder; having something to compare against does not.
Matching balances the attributes you thought of; randomization balances the ones
you did not. A matched control is therefore the weaker causal evidence at equal size and equal
care, and a randomized A/B test does not sink below a non-randomized comparison because someone
called the second one a control group.

Then add or subtract for the things that decide whether the level was earned: are the details of
the split disclosed, is a confidence interval given, were paid orders counted rather than placed
ones, is history for comparable prior periods shown, and does the income of whoever published the
result depend on the result.

## Thresholds and timings

- **The acceptance threshold has three parts: significance, the practical threshold, and
  payback.** You name all three before the test, not after. Significance covers whether the effect
  separates from zero, the practical threshold whether an effect that size is worth having, and
  payback whether this change repays what it costs to build.
- **A conclusion has a shelf life.** It ages with the base, the assortment and the channel. Say
  when the check should be repeated, at the moment you record the result.
- **Review the log once per planning cycle:** what has been confirmed, what has been refuted, what
  is due for a repeat.
- **Re-read the metric after rollout**, at the same window length used in the test, and read it as
  level 0 unless a standing holdout remains.

## Edge cases

- **Novelty effect.** The first exposure to a new format produces a lift that does not repeat.
  Extend the window or repeat the test later before building the roadmap on it.
- **A winner in one segment only.** Record it as a conditional finding, with the condition, rather
  than as a rule.
- **A seasonal window.** A test run during the peak carries the peak with it. Repeat it in an
  ordinary period before generalizing.
- **Someone else's case study.** Not evidence for your base at any level of detail. The variation
  between two audiences, assortments and channels is larger than the effect either of you measured.
- **The test won and the program metric did not move.** Usually the effect is real but small
  relative to program noise; sometimes the win was eaten somewhere nobody looked. Both are worth
  knowing, and neither is a reason to stop measuring.
- **A significant result below the threshold.** With a large enough sample, an effect too small
  to pay for itself still separates from zero. Significance and the practical threshold answer different
  questions, and this is the case where they disagree: the honest reading is "real and not worth
  building".
- **A definition changed during the test.** The comparison is invalid even if the arms both look
  fine. Note the break and rerun.
- **A fault hit the test, or a warmup began while it ran.** Read it only as `test-design.md`
  prescribes in its edge cases: nobody removed for not receiving, a cut by assignment date only
  when the fault hit both arms alike, and the cut written in the log.

## Failure modes

- **The conclusion is wider than the test.** "Personalized subject lines do not work" instead of
  "in three of our tests the first name in the subject line moved clicks by less than the threshold
  we set".
- **"Not significant" filed as "no effect".** The two are different claims, and you tell them
  apart only by reading the interval against the threshold.
- **Every pair compared because the arms were there.** The comparison set grew after the data
  arrived, and the chance of an accidental winner grew with it.
- **Significance computed for one metric, conclusions drawn for three.**
- **The losing variant quietly stayed live.** There was a test and no decision.
- **Tests keep running and nothing accumulates.** The tell: nobody can say what was tested six
  months ago or how it ended.
- **Everything wins and revenue does not move.** Either the tests are about trivia, or the wins die
  before they reach money, or the significance is being fitted to the desired answer. All three are
  worth checking in that order.
