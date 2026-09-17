---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Experiment vocabulary

The terms the three mechanics assume. These are scoped to comparison and proof. The formulas of
the metrics being compared, their numerators, denominators and windows, belong to
`metric-definitions`.

## Arm

One group in a test and the treatment it receives. Two arms is an A/B test; more than two costs
sample size and requires a declared set of comparisons rather than every available pair.

## Control group

An arm that receives nothing, so that the others can be read against what would have happened
anyway. Two kinds, and they answer different questions:

- **Local control:** withheld from one specific mechanic. Answers whether that mechanic works.
- **Global control:** withheld from all marketing messages, receiving only required rows, replies
  to requests and service rows the test is not about. Answers what the whole program adds. The strict version is also excluded from paid targeting;
  when it is not, the result describes something narrower than "the program".

## Holdout

The same idea named from the sending side: the share of the audience deliberately not sent to, so
the effect of sending can be measured. Its size is an output of the minimum detectable effect
calculation, never a habit. A **standing holdout** is a local holdout kept period after period on
one mechanic: a fixed share of each period's entries, rotated on the rule of a global control, each
period read on its own read date.

## Entry-based holdout

A holdout drawn from the people who triggered a flow rather than from the base. Required for
event-fired flows, because everyone who enters has already shown intent and a base-drawn control
compares different kinds of people. A held-out entry stays a member of the flow for the rules of its
set, so junior flows on the same object and the campaign on the same subject stay quiet for it.

## Randomization unit

The thing assigned at random: the smallest unit across which the treatment does not spill. The
person by default, or the cookie or device where that is all the site holds. A larger unit when
people inside it affect each other or get the treatment together: the account for a sequence before
or after a deal, the location for a program rolled out by store. A case, such as an exit request or
a transaction, where the object is the case. A unit stays in one arm for the whole test; assigning
per message means one human sees both variants.

## Assignment log

The record of who was in which arm and when, written before anything is sent, with every removal
(an objection, a deletion request, a cut after a fault) and its date. Needed to read the result, to
check the split, and to exclude the control from sends. Kept until the reading is frozen, not
indefinitely; a global control keeps it while it is live.

## A/A test

Two arms receiving identical treatment, run to check the split itself. Two random groups almost
always differ on a finite sample, so a gap between the arms proves nothing on its own: 50
conversions in an arm of 1,000 against 55 in the other is a z of about 0.5, which is what random
assignment produces. An A/A test also returns a significant difference as often as the significance
level allows.

An A/A test checks the machinery, not the size of the gap: the assignment mechanism, whether a
person stays in one arm, whether the arms came out at the configured size ratio, whether you lost
observations from one arm, and whether you built the split on an attribute of the person. Three
findings live here, and you read them differently.

- **Ordinary noise.** The arms differ within what random assignment produces. Nothing to fix, and
  nothing to conclude.
- **Sample ratio mismatch.** The arms are the wrong sizes for the configured ratio, or one arm lost
  observations. A data or assignment fault; investigate before reading any result.
- **A persistent instrument error.** The same skew reproduces across repeated A/A runs, or it lands
  on one identifiable group. This is what people mean when they say the randomization is broken.

An A/A/B design does the check and the test at once.

## Baseline rate

The current value of the metric before the change. One of the inputs to sample size, and the
reason a test on a rare event needs far more volume than a test on a common one.

## Minimum detectable effect (MDE)

The smallest difference the test is designed to detect. Set it from the decision, not from the
arithmetic: the smallest lift that would repay building and maintaining the change. A smaller MDE
demands a larger sample, which is why MDE, sample size and run time are one decision rather than
three.

## Practical threshold

The smallest effect worth acting on. You declare it before the test and use it at the end as the
boundary you read the result against. It is the same number as the MDE: on the way in it sizes the
test, on the way out it bounds the reading. Power against zero at the MDE is not power to clear the
threshold: at 95% and 80% a true effect equal to the threshold gives an interval entirely above it
about 2.5% of the time, so the design names in advance what an interval clearing zero and crossing
the threshold leads to. Its mirror in the other direction is the harm boundary,
unless a guardrail sets a tighter one.

Significance and the practical threshold answer different questions. Significance asks whether the
effect separates from zero; the threshold asks whether an effect of that size pays for itself. A
big enough sample clears the first while failing the second, and a test that ends "not significant"
leaves the second question open until you put the interval against the threshold.

## The four outcomes

The four conclusions a finished test is allowed to reach, decided by where the confidence interval
sits against the practical threshold and the harm boundary:

| Where the interval sits | Outcome |
|---|---|
| Entirely above the threshold | A useful effect |
| Entirely below the harm boundary | Material harm |
| Entirely between the two | Practically negligible: the effect is real or not, and either way too small to act on |
| Across either boundary | Undetermined: the test did not answer the question |

"No difference" is not one of the four. It collapses the third outcome and the fourth, and those
carry different decisions: the third closes the question, the fourth leaves it open at a cost you
now know. Declining to build a change on an undetermined result is legitimate, and it is a decision
under uncertainty rather than evidence of a zero effect.

## Multiple comparisons

Each additional comparison in one test raises the chance that at least one of them clears
significance with nothing behind it. The control is procedural: name the comparison set in the
design, keep it small, and mark everything outside it as exploratory. Where you keep several
confirmatory comparisons, name the procedure that adjusts for their number. Three arms do not
oblige you to run three pairs.

## Primary contrast

The one comparison the decision rests on, named before the test. It carries the confirmatory
reading; the others describe. Without it, the comparison set expands after the data arrives and the
winner is whichever contrast came out best.

## The four windows

Four separate spans that a design has to keep apart:

| Window | What it bounds |
|---|---|
| Assignment | While people still enter the test and get assigned to arms |
| Treatment | How long the change is allowed to act, bounded by things like an offer's expiry |
| Outcome | How long you count outcomes for each person, counted from that person's own assignment |
| Finalization | The wait before reading, so returns, cancellations and late orders settle |

**The treatment window closing does not close the outcome window.** A purchase after the offer
expired is still the outcome the design counts, if the design said so.

`segmentation` uses *observation window* for the lookback of a segment attribute. This skill says
*outcome window* for the span in which a test counts results, so the two do not get confused.

## Significance level and confidence level

**The significance level, alpha, is the risk you accept of calling a difference real when there is
none. The confidence level is `1 - alpha`**, the same choice written from the other side. Set alpha
to 0.05 and you have 95% confidence and a 5% false positive risk. Lowering the confidence level shrinks the required sample and raises the chance of acting on noise.
It is a convention about risk, not a standard of quality.

## Confidence interval

The range of effects the data is consistent with at the chosen level. The level describes the
procedure, not the single interval in front of you: run the same test many times and 95% of the
intervals it produces contain the true value.

You read the four outcomes off the interval. A point estimate on its own cannot separate "too
small to matter" from "we could not see it", which are the two readings that get swapped when a
test comes back short of significance.

## Power and type II error

**The type II error rate, beta, is the risk of missing a difference that is there. Power is
`1 - beta`.** Set beta to 0.20 and you have 80% power and a 20% chance of missing the effect. Low
power is why a test can end with what people call "no difference" when it means "we could not have
seen it either way". That is the undetermined outcome, not the negligible one.

Power is not a property of the test on its own. It is computed against one specific effect size,
normally the minimum detectable effect, and it falls as the effect gets smaller: a test with 80%
power against the effect it was designed for has much less against an effect half that size. State
the effect it was computed for, the unit of observation and whether the test is one sided or two
sided, or the number carries no meaning.

## The four numbers in one example

Alpha 0.05, beta 0.20, two sided, the person as the unit of observation, power computed against the
MDE:

| Field | Value | Reads as |
|---|---|---|
| Significance level, alpha | 0.05 | 5% risk of calling a difference real when there is none |
| Confidence level, `1 - alpha` | 95% | the same 5% risk, stated as coverage |
| Power, `1 - beta` | 80% | 80% chance of detecting an effect the size of the MDE |
| Type II error, beta | 0.20 | 20% risk of missing an effect the size of the MDE |

The pair 95/80 is the customary teaching setting, not a recommendation for every test. Both numbers
come from what being wrong costs in the decision at hand, and both go into the sample size
calculator as risks, not as coverage: a calculator that asks for alpha wants 0.05, not 95.

## False positive and false negative

**False positive:** concluding there is an effect when there is none. Its rate is alpha, so the
confidence level controls it. **False negative:** concluding there is no effect when there is one.
Its rate is beta at the effect you chose, so power controls it. The first wastes the cost of a
rollout; the second quietly discards a working mechanic. Which one
is more expensive depends on the decision, which is why both numbers are chosen rather than
inherited.

## Guardrail metric

A metric that is not allowed to deteriorate while the decision metric improves. Unsubscribes,
complaints, margin and reach are the usual set. A decision metric without a guardrail is an
invitation to win the test and lose the program.

## Stopping rule

The sample size or date at which assignment ends, fixed before the test starts. The test ends on
the **read date**: the last assignment plus the outcome window plus finalization. A reading before
it is provisional.

## Peeking

Watching results accumulate and stopping at the first favorable moment. It inflates the false
positive rate well beyond the confidence level you think you are using, which is why the stopping
rule is written in advance.

## Leakage

Marketing messages reaching the control group. Tolerated leakage is zero in the configuration.
Verified by counting messages received by the control, by person, not by trusting the
configuration. Leaked people stay in the control for the reading, the leaked share is reported
beside the effect, and the difference is pulled toward zero by what reached them; a period whose
leakage cannot be counted by person was not measured.

## Sample ratio mismatch

The arms ended up at sizes the design did not intend, for example 55/45 where 50/50 was
configured. It signals a broken assignment or a filter applied to one arm, and it invalidates the
comparison regardless of how good the result looks.

## Incremental effect

The difference in the decision metric between treated and control, per unit assigned, with no
credit rule in the numerator and a read date. The number this skill exists to produce. Per unit
exposed selects the treated arm by what happened after assignment; an attributed numerator is zero
in a control by construction.

**A word about the word.** "Incrementality" gets used to mean revenue minus cost. That is
payback, not incrementality. Payback says whether an activity was worth its cost under whatever
attribution produced the revenue figure; incrementality says whether the activity caused anything.
A program can be profitable in a report and incrementally worthless, and only the second
measurement will ever say so.

## Cost of the experiment

The margin forgone in the control group over the measurement window: the units in the control times
the expected effect per unit times margin, with the MDE as the expected effect when nothing better
exists. Not what the control produced in a prior period, which includes the purchases it makes
anyway. Stated before the test as the price of the answer.

## Evidence ladder

The ranking used to read a claim: before-and-after at the bottom, a comparison against a control
nobody randomized above it, and a comparison against a randomized control at the top, whether it is
an A/B test or a holdout. Random assignment raises the level and having something to compare
against does not, so a matched group of stores or cities stays on the middle rung no matter what
anyone calls it, while locations randomized in the order of a rollout sit at the top. Modified by
whether the split is disclosed, whether a confidence interval is given, whether paid orders were counted rather than placed ones, and whether the author's income
depends on the conclusion.

## Test log

The register of tests: hypothesis, design, dates, arms, metric, result, decision. It is what makes
a testing practice accumulate instead of repeating itself, and it keeps negative results that
nobody else has a reason to keep. Writing the entry, with the result, its interval and read date,
freezes the reading.

## Novelty effect

A lift produced by a format being new rather than by it being better. It fades, which is why a
short test of a new format tends to overstate what the rollout will produce.
