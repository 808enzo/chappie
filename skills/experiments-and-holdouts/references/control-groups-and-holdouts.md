---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Control groups and holdouts

A control group answers the only question attribution cannot: how much of this would have happened
anyway. It answers it by not sending, which means the answer has a price, and the price is paid
whether or not anyone bothered to compute it in advance.

This mechanic is how the group is built, how large it has to be, how it is protected, and what it
costs.

## Entry conditions

- The question is whether a mechanic produces anything at all, or how much of the result it
  produced.
- You can withhold messages from a group and keep that exclusion in force across every channel and
  every campaign.

## Exit conditions

The type of control is named, the population it is drawn from is named, its size follows from a
computation rather than a habit, the rotation and duration are set, the cost is stated in advance,
and leakage is verified with a number rather than an intention.

## Sequence

**1. Choose the type.** A **local control** does not receive one specific mechanic and answers
whether that mechanic works. A **global control** receives no marketing messages at all, only
the required and service rows of step 6, and answers what the whole program adds. The strictest
version of a global control is also excluded from paid targeting; where that is impossible, say so when you report the
result. Both can exist at once: carve the global control out of the base first, draw local
controls from what remains.

**2. Draw the control from the right population.**

The general rule: **assign at the moment a unit reaches the point where the treatment would
start, and read both arms on one date counted from assignment.** Assigning earlier dilutes the
effect with units that never reach the point; reading each arm on its own schedule compares
different spans.

| Object | Population and unit | Assignment and reading | Outside the holdout |
|---|---|---|---|
| Triggered flow | the entries, meaning the people who fired the trigger, not the base: everyone who enters has already shown intent | at entry, logged before any send; a held-out entry stays a member of the flow for the rules of its set (`test-design.md`, edge cases) | none |
| Exclusion rule | the people the rule selects, split at random; one part receives the send as if the rule did not exist | the difference is the margin given up, set against the send cost avoided, as the payback in `reading-a-result.md`, step 6, does; re-verify when the rule moves to another offer | none |
| Channel program | the base, at random, with rotation (step 5) | revenue per person assigned, any channel, no credit rule (`email-program`) | required and service rows still go out (step 6) |
| Added step in a cascade | people who did not respond to the earlier steps by the moment the new step would fire | at that moment; edge case below | none |
| Slot inside a product | people eligible for the message **who reached the slot** in the window, not every user of the app | at the first moment of eligibility; a split by platform is mandatory, because a divergence between platforms catches a broken destination on one of them; a view with an attribution window is not a test (`in-product-messaging`) | none |
| Retention offer on the cancel path | exit requests that reached the offer (for example the reason is price and the alternative was declined), not people and not subscriptions | the control gets the cancel button with no offer; read both arms on the assignment date plus the offer's length plus one term at full price, and the outcome is whether the unit pays full price on that date (`subscription-retention`) | recovery cases of failed payments are not in the population: their messages are service rows |
| Sequence before a deal | the account, not the contact, because contacts of one account talk to each other and leakage between them is the rule; a test on contacts reads that leakage as an effect (`b2b-lifecycle`) | at entry to the sequence | none |
| Program touches after a deal | the account | on the day the won record is accepted, or on the opening date of the renewal case; read at the decision point (`b2b-retention`) | notices a law or the contract requires, the business review and every step of the account manager still go out |
| Rollout of a program across locations | the location; there is no account and no person to assign | a random order of waves inside each cluster of comparable locations, fixed before the first wave; read while the rollout lasts, because after the last wave no untreated location exists (`loyalty-program-launch`) | none |
| Optional service row | the case, such as one transaction | a row that repeats what was already delivered (a reminder before a pickup hold ends, an extra progress row) is tested against its absence (`transactional-messaging`) | every required row still goes out: access, confirmation, the first message of an exception, rows a law requires |

**3. Size it from the minimum detectable effect, not from a customary percentage.** The share of
the base is an output of that computation. If the computation demands a share the business will
not give up, then this question does not get an answer, and saying so is more honest than a small
control that cannot detect anything.

**4. Price the answer before you start.** The margin forgone in the control group over the
measurement window is the cost of the experiment. State it in advance. What is forgone is the
effect, not the control's revenue: people in the control keep buying on their own. Estimate it as
the number of units in the control times the effect you expect per unit times margin, and use the
MDE as the expected effect when you have nothing better. What the control produced last month is
the base the effect sits on, and pricing the test from it counts purchases the control makes
anyway.

**5. Set duration and rotation.** Nobody stays without communications indefinitely: refresh the
membership of a global control on a period no shorter than the measurement window. Rotation is
both hygiene and protection against silently losing a slice of the base.

Membership survives every rule that reads a response to messages. Somebody who receives nothing
answers nothing, so the engagement tier of `email-program` files them dormant and the silence
threshold of `list-building` takes them out of the active base, and by the time they rotate out the
program treats them differently: the control was treated after all. Freeze those states at their
value on the day of assignment for as long as the person is in a control. States that read
purchases keep counting, because a purchase in the control is real behavior.

A local holdout read period after period (a triggered flow, a return attempt, a daily digest) is a
**standing holdout**: a fixed share of the units entering each period, the unit keeps its arm until
rotation on the same rule as a global control, and each period is read once its read date has
passed.

**6. Protect the control from leakage.** The exclusion has to hold across every channel and every
campaign, including one-off manual sends, which is where it breaks. Required rows (access,
confirmation, the first message of an exception, notices a law or a contract requires), replies to
a request the person made, and service rows the test is not about continue and do not count as
leakage.

**7. Verify the control with a number.** Count the marketing messages the control group received
during the period, by person. Leaked people stay in the control for the reading: removing them
selects on who a send happened to reach. A leak moves the control toward the treated arm by
roughly the leaked share of the control times the effect of what reached them. Report the effect
with the leaked share beside it, and say that the difference understates the effect wherever what
leaked pushes the outcome the same way. A leak you
cannot count by person, because the control has no contact record, means the period was not
measured.

**8. Read the difference on the decision metric**, money or the target action, as an effect with
an interval around it, and place that interval against the practical threshold you set before the
test. Distinguishable from chance is one question; large enough to repay the control is another,
and `reading-a-result.md` step 5 keeps them apart.

**9. Decide: scale, stop, or measure again.** A result without a decision means the cost of the
experiment bought nothing.

## Thresholds and timings

- **Control size** comes from the minimum detectable effect and the baseline rate. The floor is
  not a percentage, it is an absolute number of expected target actions inside the control.
- **The rotation period is at least the measurement window**, or you are measuring people who
  switched groups halfway through.
- **The outcome window covers the category's decision cycle.** It is the window over which you
  count results, not the window in which you may still send: `test-design.md` step 8 sets the two
  separately, and the second one closing does not close the first. A short outcome window reads a
  slow mechanic smaller than it is and reads purchases that were only moved earlier as a gain.
- **Tolerated leakage is zero** in the configuration, and the count of step 7 says how far the
  period fell short of it. The target comes from the construction of the measurement, not from your
  data. The other values this skill names without deriving them from your data (95% and 80%, whole
  weeks, eight to twelve readings for a self-baseline) are conventions or starting points, and each
  says so where it stands.
- **Review the global control once per planning cycle:** size, composition, and whether an entire
  segment has drifted into or out of it.

## Edge cases

- **An added step in a cascade.** The question "is another step worth it" has a specific procedure:
  at the moment the new step would fire, split the people who have not responded to the earlier
  steps at random, send the new step to the treated part only, count a fixed outcome window from
  each person's split, and take the difference as the incremental conversions. Then divide the cost
  of the step by the number of incremental conversions and compare that cost to the previous step and to your other channels, each measured the same way,
  against its own holdout: set against a cost per attributed conversion, the new step loses to
  steps whose credit includes what would have happened anyway. Make the decision on that cost
  rather than on whether an effect exists at all: a real effect whose cost per incremental
  conversion is many times that of your other steps is still a no.
- **A mechanic that cannot be randomized by person.** A loyalty program launch, a site redesign,
  a chain-wide promotion. First look for a larger unit you can randomize: a rollout in waves can
  take its order at random inside clusters of comparable locations, which is a randomized
  comparison by cluster for as long as the rollout lasts (step 2, and the cluster row of
  `test-design.md`, step 6). Where no unit can be randomized, or the rollout is over, build the
  comparison from matched groups, meaning comparable stores, cities or cohorts, and read it one
  level lower on the ladder in `reading-a-result.md`: matching balances the attributes you thought
  of, randomization balances the ones you did not. It sits above before-and-after and below a
  randomized control, and calling the matched group a control group does not move it.
- **A small base.** The control cannot be assembled in reasonable time. Say so directly, then offer
  what is available: a self-baseline over your own periods, which reads whether a number is unusual
  and sits at the bottom of the ladder as evidence of cause, and a matched comparison whose limits
  you state.
- **Peak season.** The control costs most exactly when measurement is worth most. Decide the
  question in advance and write it down, rather than deciding it under pressure in the middle of
  the peak.
- **Someone in the control asks why they did not get the offer.** A control group is a real
  customer experience, not a row in a report. Support needs an answer prepared.
- **Service messages.** Required rows are not tested for existence and are not withheld from any
  control. An optional row that repeats what was already delivered can be tested against its
  absence, randomized by case (step 2).
- **Someone in a group objects to marketing, or asks for deletion where that right applies.** They
  leave the group on the day of the request, in the treated arm and in the control alike, and the
  assignment log records the removal with its date; whether their earlier data still counts in the
  reading is counsel's answer, and the reading names the removals it excludes
  (`consent-and-preferences`, the objection and the erasure route).

## Failure modes

- **The control group received messages.** A common breakage: the exclusion lives in one system and
  a one-off send went out from another.
- **The "control" was assembled by hand.** A group chosen by an attribute answers a question about
  the attribute, not about the mechanic.
- **The control has not been refreshed in years.** It stops resembling the base, and the gap
  between them stops being about the program.
- **The cost was paid and no answer arrived.** The tell: the size was set as a share, the minimum
  detectable effect was never computed, and the difference landed inside the noise.
- **Only the saving was counted.** The money saved shows up on the channel invoice and the revenue
  given up shows up nowhere, which is exactly the trap `segmentation` warns about when a cut is
  used to withhold sends.
- **The global control is excluded from email but not from paid targeting.** The number then
  describes what the sends add while paid targeting reaches both groups, which is narrower than
  "the program". Name that on the result rather than reporting it as the program's effect.
