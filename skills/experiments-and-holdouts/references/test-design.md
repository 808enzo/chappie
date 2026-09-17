---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Designing one test

A test is a decision waiting for one number. Everything below exists to make sure the number that
comes back is about the thing you changed, arrives before the decision is stale, and is large
enough to act on.

## Entry conditions

- A decision depends on the answer, and you can name what you would do differently under each
  outcome.
- The change can be delivered to one group and withheld from another.
- The audience is large enough to produce an answer before the decision expires.

## Exit conditions

Written down before anything is sent: the hypothesis, the decision metric with its definition,
the guardrails, the randomization unit, the minimum detectable effect and the calculation that
matches it, the sample size, the four windows, the set of comparisons, the stop date or stop
volume, and the read date that follows from them. The split has been checked.

## Sequence

**1. Write the hypothesis as one sentence: element, metric, direction, size.** "Will using the
first name in the subject line affect clicks" is a question, not a hypothesis. The hypothesis names
the expected movement, because the size of the movement determines the sample size, and the sample
size determines whether the test is possible at all.

**2. One test, one hypothesis.** The trap worth memorizing: adding a recommendation block to a
message changes two things at once, the presence of a block and the algorithm that fills it. To
separate them you need a third arm with a block of randomly chosen items. Without it you get a
result that does not answer the question you asked.

**3. Name the decision metric before the test, and take its definition from
`metric-definitions`.** A metric chosen after the numbers are in justifies the result instead of
testing it.

An email open is not a decision metric. Opens carry a machine component: Apple states that Mail
Privacy Protection downloads remote content in the background whether or not the person engages
(the address is in `email-copy`), and the share of such opens differs by audience and changes with
the mail client. A subject line or emoji test read on opens measures machines as well as people, so
its result reads as a direction and decides nothing on its own; name clicks or an action further
down as the decision metric.

**4. Name the guardrails.** A win on clicks next to a rise in unsubscribes is not a win. The usual
set: unsubscribes, complaints, margin, reach. Write down in advance how much guardrail movement
cancels the result.

**5. Choose the randomization unit: the smallest unit across which the treatment does not
spill.** Usually the person, not the message and not the session, and the person stays in the same
arm for the whole test. Otherwise one human sees both variants and the comparison is between two
mixtures rather than two treatments. Where the site knows a visitor only by a cookie or a device,
that identifier is the unit, and the share of sessions without one is read next to the result. Move
up when people inside a group affect each other or receive the treatment together: contacts of one
buying account talk to each other, so a sequence before or after a deal is assigned by account;
a program launched at a store is assigned by location. Where the object is a case rather than a
person (an exit request, one transaction), the case can be the unit, and a second case from the same
person while the first is still open keeps the first case's arm.
`control-groups-and-holdouts.md`, step 2, lists the objects.

**6. Set the minimum detectable effect, then pick the arithmetic that matches the outcome.** Not
the smallest difference the arithmetic could detect, **the smallest difference that would change
your decision**. From that, the baseline rate, the significance level and the power, the sample
size follows. The calculator computes power against this effect and no other, so record the MDE,
the unit of observation and whether the test is one sided or two sided next to the sample size. The
same number returns at the end as the practical threshold you read the result against. That is one
more reason to take it from the decision rather than from the audience you happen to have.

**Size for the reading you intend to reach.** Power computed against zero at the MDE is the chance
that the interval clears zero when the true effect equals the MDE. It is not the chance that the
interval clears the threshold. At 95% confidence and 80% power the MDE is about 2.8 standard errors;
an interval sitting entirely above a threshold of that size needs an estimate of about 4.8 standard
errors, which a true effect equal to the threshold produces about 2.5% of the time and a true effect
of twice the threshold about 80% of the time. So a test sized this way sends effects near the
threshold to the undetermined outcome of `reading-a-result.md`, step 5, almost every time. Choose
one before the test and write it down: size against the gap between the effect you expect and the
threshold, which needs an expected effect larger than the threshold and a larger sample; or keep
the smaller sample and write the rule for an interval that clears zero and crosses the threshold
(ship it as a decision under uncertainty, or extend the test), and log it that way.

A calculator does the arithmetic, and you pick the calculator from the outcome and the
randomization unit:

| What you compare | Randomization unit | What the calculation needs |
|---|---|---|
| A rate: conversion, open, click, reactivation | The person | Two proportions and the baseline rate. This is the default calculator on the web, and the reason people assume there is only one |
| Money per person: revenue, order value | The person | A continuous outcome, so it needs the spread of that outcome in your own data and not only its mean. A few large buyers stretch the spread, and the sample it demands runs well past a rate test on the same audience |
| An outcome measured on stores, cities or cohorts | The cluster | Cluster randomization: the sample counts clusters, not people, and it grows with how alike people inside one cluster are. A per-person calculator here returns a number you cannot trust |
| Repeat purchases, several events per person | The person over a window | One number per person for the window, a count or a sum, then the continuous case above. One row per event counts the same person several times and reports an interval narrower than the data supports |

The judgment is which difference matters; the arithmetic still has to match the outcome and the
unit you picked.

**7. Compute the run time and check it against the decision's shelf life.** If the answer needs
more time than the offer, the page or the season will survive, **do not run the test.** Decide
another way and record it as decided without a test. A months-long test for a fraction of a
percent is spending disguised as rigor.

**8. Name the four windows separately.** Collapsing them into one is the routine mistake, and
every item below moves independently of the others.

- **Assignment window.** While people still enter the test and you still assign them to arms. In a
  triggered flow they enter one at a time rather than in a single batch, so this window has a
  length of its own.
- **Treatment window.** How long the change may act. An offer that expires tomorrow closes this
  window tomorrow.
- **Outcome window.** How long you count outcomes for each person, counted from that person's own
  assignment rather than from a calendar date. It covers the category's decision cycle, and you set
  it in the design.
- **Finalization.** The wait before you read, long enough for returns, cancellations and
  late-arriving orders to settle.

**The read date follows from the windows:** the last assignment, plus the outcome window, plus
finalization. The stopping rule ends assignment, not the test. A reading taken before that date is
provisional and says so.

**The end of the treatment window does not close the outcome window.** A purchase a week after a
one-day offer expired is still the outcome the test was built to count, as long as a week is what
you wrote down. Cutting the count at the expiry removes late outcomes from every arm, and the
difference loses whatever part of the effect arrives late, so a slow mechanic reads smaller than it
is. It also hides a treatment that only moved purchases earlier: those people would have bought
inside a longer window anyway, and a short one reads the shift as a gain. The outcome window covers
the category's decision cycle for both reasons.

**9. Randomize, then verify the split.** Verify with an A/A test, by comparing the arms on the
prior period before the treatment starts, or with an A/A/B design that does both at once. Verify
the mechanism rather than the size of the gap: arms at the configured size ratio, assignment that
stays with the person, no observations lost from one arm, no attribute of the person used to build
the split. Arms that differ a little are what random assignment produces on any finite sample. A
size ratio that misses the configured one, a skew that reproduces across repeated A/A runs, or a
skew that lands on one identifiable group is a broken split. `experiment-vocabulary.md` separates
the three.

**10. Run all arms over the same calendar period.** A sequential test, this month one way and
next month the other, measures the season, the promotional calendar and the day of the week along
with your change.

**11. Freeze the environment.** While the test runs, the same audience is not part of another
change to the same metric. Two overlapping tests on one audience produce four groups nobody
designed.

## Thresholds and timings

- **Confidence and power are conventions, not norms.** A common pair is 95% confidence and 80%
  power, which is a 5% risk of calling a difference real when there is none and a 20% risk of
  missing an effect the size of the MDE. Lowering confidence shrinks the sample and raises the
  chance of acting on noise; both numbers should come from the cost of being wrong in this
  decision.
- **The minimum detectable effect comes from the economics of the decision:** the smallest lift
  that would repay building and maintaining the change.
- **Run for a whole number of weeks**, so every arm contains every day of the week, and for at
  least one behavioral cycle of the category.
- **The upper bound on run time is the decision's shelf life**, not patience.
- **The outcome window is the same length in every arm**, counted from each person's own
  assignment. A window counted from a calendar date gives late entrants less time to respond than
  early ones.
- **Sample size is computed before launch**, not watched as it accumulates.
- **Read no earlier than the read date** of step 8: last assignment, outcome window, finalization.

## Edge cases

- **More than two arms.** The sample requirement grows with each arm, and you choose the set of
  comparisons in the design rather than at reading time: the default set is each variant against
  the control, and you name one of those the primary contrast. Comparing every pair is a separate and more
  expensive question, and running all of them without adjusting for their number raises the chance
  that one arm looks like a winner by accident. Multi-arm testing is a tool for high volume.
- **Variants that barely differ.** Two shades of one button will not separate in any reasonable
  time. Test the value proposition and the wording; the styling is not where the difference is.
- **A narrow audience.** No test is possible, and that is the answer. Decide on other grounds and
  mark the decision as unverified rather than pretending a small sample settled it.
- **A test inside a triggered flow.** Randomize at entry, write the entry to the assignment log
  before anything is sent in either arm, count each person's outcome window from that person's own
  entry, and remember that people enter continuously rather than in one batch. A held-out entry
  stays a member of the flow for the rules of its set: junior flows on the same object and the
  campaign on the same subject stay quiet for it as they do for a treated entry
  (`triggered-messages`). Otherwise the control gets the same pitch by another path, and the
  difference measures the path. The event's expiry bounds when the message may go out; it does not
  bound how long you count the result.
- **A behavior you cannot assign.** Reaching an activation event or joining a tier is something
  people do, not something you give them, and comparing those who did with those who did not
  compares different people. Assign at random what pushes toward the behavior (the nudge, the
  guidance, the offer), read the outcome per person assigned in each arm, and read beside it how far
  apart the arms ended on the behavior itself. The first difference is the effect of the nudge. The
  effect of the behavior is that difference divided by the gap in the behavior's share, and only if
  the nudge can change the outcome through the behavior and no other way; say that condition when
  you report it.
- **A sending identity in warmup or in recovery.** Do not start a test there and do not read one:
  the audience is narrowed to the current step of the ladder, which is not the population the
  result would be applied to, and volume changes step by step inside the outcome window
  (`deliverability`). Start once volume is back at its ordinary level. A test already running when a
  warmup or a recovery starts is a fault, as below.
- **A fault during the test.** Stop assignment first. A fault that stopped delivery in one arm
  leaves the people it touched in that arm for the reading, which then measures the program as it
  ran, or the test restarts; removing people because their message did not arrive selects on what
  happened after assignment. A fault that hit both arms alike between two known dates can be cut by
  assignment date: everyone assigned between those dates leaves both arms, assignment continues to
  the planned sample, and the log records the cut. Extending the stop date to recover lost time is a
  change to the stopping rule, and it is written down before the test resumes.
- **A test of cadence.** The unit is the person over a period, the effect appears slowly, and the
  guardrail that matters, unsubscribes, moves later than revenue. Such a test needs a longer window
  than a content test and a decision rule that waits for it.
- **A test that changes price.** Design runs into law and into trust. The safer form varies the
  offer at a constant price; see the legal section of `SKILL.md`.

## Failure modes

- **The hypothesis is a question.** It can be neither confirmed nor refuted, and the test ends in
  "interesting, we should look deeper".
- **Two changes in one test.** You get a result and no conclusion.
- **The winner was picked on opens.** The decision metric was something else, but nobody named it
  first.
- **The arms differed before the start.** A small gap in the metric is what random assignment
  produces on its own. The tell is a systematic one: one arm holds noticeably more engaged people,
  because you split on a convenient attribute rather than at random.
- **The outcome window was cut at the offer's expiry.** The count stopped where the sending
  stopped, and every slow response fell outside the measurement.
- **Every pair compared because the arms were there.** Nobody named a primary contrast, so the
  winner was whichever comparison came out best.
- **The test was stopped when it looked good.** Peeking and stopping at the first favorable moment
  turns the confidence level into decoration.
- **The test was rerun until it won.** The same failure spread over months, and harder to see
  because each individual run looked fine.
