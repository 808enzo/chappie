---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-09
---

# Early interception: signals, scoring, validation, and what a signal may trigger

The unit here is **one observed period for one customer**. Not a segment and not a message: the
signal comes from comparing a customer against themselves in an earlier period, and the mechanic
outputs a reason to look rather than an argument to send. Where somebody can go and look, that is
what the higher zone means. Where nobody can, the look is a question (step 5), and it is still not
an offer.

This is the half of the skill that runs before the threshold in `defining-lapse.md`. Everything
past that threshold belongs to `return-attempt.md`.

## Entry conditions

The observed unit has a norm of its own: enough periods of history to compute that norm from.
You also have a retrospective of people who already left, which is what you build the pattern on.

## Exit conditions

Named: the list of criteria with a class on each, the scoring rule, the zones, the mandatory
validation step, and what a signal is allowed to trigger. The quality of the system itself is
measured by two numbers, both computed on your own data.

## Steps

**1. Build the pattern from a retrospective of people who left, not from intuition.** Take the
ones who left over the past period and look at what happened to them for several periods before
they went. An intuitive list catches what feels alarming, which is not the same set as what
precedes departure.

**2. Separate two classes of criterion, because they normalize differently.**

- **A drop in level.** A usage measure fell relative to **this customer's own norm** in the
  previous period. Comparison against the base does not work here: every customer runs at their own
  level, and low for one is high for another.
- **An alarming action.** An event that carries intent on its own: exporting their own data,
  switching off automations, detaching a payment method, removing an integration, uninstalling the
  app. It needs no normalization. It either happened or it did not.

**3. Score one point per criterion that fires, with no weights.** Weights need data you do not have
at the start and manufacture false precision. The zone threshold is the number of criteria firing
at once: a lower zone that means look, a higher zone that means go.

Start with **a third of the criteria for the first zone and half for the second**. That is a
starting point rather than a property of anything: it applies to a set of six or more criteria,
and below that the scoring degenerates, because one criterion is already a third of three. Replace
it after the first retrospective, which shows the score at which the system starts missing people.

**4. Compare against the same period rather than the neighboring one wherever there is a season.**
A holiday, a vacation and a seasonal trough produce exactly the drop that leaving produces. One
criterion firing on its own is not a pattern, and that is the whole point of scoring several.

**5. Validate the signal before acting on it, and the more the action costs, the less optional the
validation is.** A list from the high zone is not a send list. The order is signal, validation,
diagnosis, action.

Where the units are few and each is expensive, a person validates: goes in, asks, confirms or rules
it out. That is the shape this mechanic came from, and there the higher zone means somebody goes.

Where the units are many and each is cheap, nobody goes, and the recency recheck at selection does
not substitute for the person: it answers whether the qualifying action has happened since
assembly, which is a different question from whether the drop is real. Two things take the person's
place:

- **A second independent reading of the same drop**, taken on a measure the innocent explanation
  would not move. A seasonal trough shows up across the whole comparable cohort, a vacation leaves
  a second unrelated measure alone, a broken integration does not. One measure firing by itself
  stays in the lower zone.
- **A diagnostic touch as the action of the higher zone**, with the reply as the validation. The
  zone still means go, but going is a question rather than a visit, and the answer, or the silence
  after it, is what confirms or rules out.

With neither a person to go nor a second reading to take, the interception mechanic does not get
built. Scoring with no validation step produces a list that gets messaged, which is what step 6
rules out.

**6. A signal triggers a diagnostic step, not a monetary one.** A question, a call, an offer of
help, a reminder about the part of the product they never switched on. A monetary argument at this
point teaches people to fall into the signal: somebody who has not left learns that going quiet
produces a discount. The argument belongs past the threshold, in `return-attempt.md`.

**7. Order the work by exposure rather than alphabetically.** Keep the money each unit represents
next to its score: revenue for the period, the recurring payment, the average spend per cycle. The
queue then sorts itself, and the conversation with the business happens in revenue at risk rather
than in a list of names.

**8. Measure the system itself with two numbers, name the population under each, and read them
together.** Each of them lies on its own: name only the people who have already written to say they
are leaving and the system has no false positives left and no early warning either. Read the
numerator and the denominator of each out loud before quoting either one.

- **Named in advance.** Numerator: people who crossed the lapse threshold in the period and stood
  in a zone before they crossed it. Denominator: everybody who crossed it, including the units the
  scoring was never allowed to look at, which are the new ones and the small ones left out in step
  3 and in the edge cases. Report what share those left out units are, because you cannot read a
  system that scores half the base as though it scored all of it.
- **Named with nothing wrong.** Numerator: named units whose validation came back negative.
  Denominator: named units that were validated at all, rather than every unit named. In the
  expensive branch those differ by whatever the queue did not reach; in the cheap branch the
  denominator is the units that got a second reading or a diagnostic touch, and a signal nobody
  validated sits in neither half of the fraction.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Recompute interval | how fast the observed behavior changes, not the calendar |
| Drop threshold per criterion | the unit's own norm over a comparable period |
| Criteria per zone | starting point: a third of the set and half of the set; replaced after the first retrospective |
| Depth of the retrospective | as many periods before departure as the signal needs to show up in |
| Minimum history for a norm | several periods; before that the norm is not computed and the unit is out of the scoring |

## Edge cases

- **A new unit.** It has no norm yet and nothing to compare against, so it stays out of the
  scoring until it has history. Score it earlier and every fluctuation reads as a drop.
- **A small unit.** Absolute values are low and the noise is larger than the signal: halved
  activity is two events against four. Set a floor on the absolute value, or leave it out of the
  scoring.
- **Seasonality and vacations.** See step 4. Separately: in some businesses the vacation is where
  leaving starts, and only validation tells the two apart.
- **A signal fires on somebody already past the threshold.** That is not interception, it is a
  win-back. The unit moves to `return-attempt.md` and stops being scored here.
- **B2B: an account under contract.** `b2b-retention` supplies the criteria of both classes. A drop
  in level: seats in use against the account's own norm, the time to the first milestone. Alarming
  actions: the champion leaving, a change of budget holder, a request to reduce, a request for the terms
  of data export or termination, a procurement procedure. The scoring stays here; the account manager
  validates, which is the expensive branch of step 5. A signal on an account with an open renewal case
  is a risk entry in that case, not a campaign. The sign of a breach: a campaign reaches an account
  inside its open renewal case. The remedy: write the signal into the case.
- **An alarming action with an innocent explanation.** Exporting data is sometimes preparation for
  a report. The class of the criterion does not change; what changes is the result of the
  validation.

## Failure mode

**A system that fires after the decision.** No false positives, everybody named does leave, and it
looks like excellent quality. The threshold sits so high that the signal arrives once the person
has chosen to go, which leaves you nothing to show up in time for.

Catch it by reading both numbers from step 8 together, and by a third one neither of them
contains: **how far ahead of departure the signal fired**. Compute that one separately, on the same
retrospective you built the pattern from.
