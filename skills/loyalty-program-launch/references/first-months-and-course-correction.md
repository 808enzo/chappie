---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# The first months and the first correction

The gap between "the program is live" and "the program works" is longer than anyone's patience, and
the pressure to answer inside that gap is where wrong conclusions about a program come from. The
work in this mechanic is knowing which question is answerable at which point, answering that one
well, and refusing the others out loud.

This mechanic ends at the first revision of the rules. Standing watch over a program that has
settled belongs to `program-audit-and-ops`.

## Entry conditions

- The program is live somewhere: a pilot counts, and the pilot is where the first readings of this
  mechanic are taken, because wave sizing and the redemption path both depend on them. The reading
  schedule was set before launch rather than negotiated after.
- The model that justified the launch is written down and available for comparison.
- You can identify which transactions belong to members.

## Exit conditions

You have a reading at each planned checkpoint, you can say which of the changes since launch are
build quality and which are behavior, the liability is tracked against the plan, and the first
rule revision has gone out through the announced process.

## Sequence

**1. Fix the reading schedule before launch.** One month, three, six and twelve is a starting grid,
not a rule: it suits a category people buy from monthly, and it is the wrong grid where they buy
twice a year. Set the checkpoints in median interpurchase intervals for your own category, then
write them down as dates, and against each one write what gets read and what that reading can and
cannot conclude. Set the number that ends the investment phase. Doing this before launch is what
makes it possible to refuse the revenue question in month two without appearing to hide from it.

**2. Read the first month as build quality.** Enrollments by entry point, classes of error,
volume of support contacts, questions per location per week. None of this is effect; all of it
predicts whether there will be one. The signal of health is the trend: error classes closing,
questions declining, the same problem not arriving twice from different locations.

**3. Read identification by location and channel, never as an average.** An average across
locations that behave differently describes none of them. The work is with the lower group, and the
first question about it is whether they differ in customers or in behavior at the counter. Those
have different remedies and look identical in a total.

**4. Compare members with themselves before they joined.** Frequency, order value and interval
before enrollment against after. Where non-members are identifiable, because an account, a
document or a delivery address exists regardless of the program, a member-to-non-member comparison
is also available. Both readings carry the same caveat, and it is stated every time:
the people who join are the people already more inclined to buy. The comparison is a signal, not a
proof of causation: nothing done to the comparison afterward removes the self-selection, and the
only design that turns it into proof is an untreated group, which the rollout supplies and the
finished program does not. `experiments-and-holdouts` owns that design.

**5. Read the redemption side as soon as the first cohort can reach it.** Points accruing with
nothing redeemed is the earliest warning the program gives you. Rule out the mechanical causes
before the design ones, because they look identical in the number: the redemption path does not
work at the till or staff cannot run it, and members do not know what they hold because no message
accompanies a movement of the balance (the flow that fixes the second belongs to
`triggered-messages`). What is left points at the design: the reward is not wanted,
the minimum for redemption is too far away, or the range on which points can be spent is too
narrow. The first two are yours, the last three go to `loyalty-program-design`, and all of them get
more expensive after the liability has grown.

**6. Run plan against fact monthly on the model that justified the launch.** Enrollment,
identification, accrual, redemption and the resulting cost, each against its planned value. Two
ratios belong in this reading and nowhere else in the skill: **redemption share**, points redeemed
over points accrued in the period, read next to the liability; and **active member share**,
members with the defined action inside the named window over all members, read next to new customer
volume, because it climbs on its own once inflow stops. Both are defined in
`loyalty-launch-vocabulary.md`, and neither is a control metric. The model will be wrong; that is
expected and is not the point. The point is knowing which line is wrong, by how much, and in which
direction, while there is still room to act.

**7. Make the first revision through the announced process.** Where the plan-fact gap is in the
cost of the program, the terms move on the interval published in the rules, with notice. Where
there is room, move terms in the direction of loosening: relaxing a strict start costs nothing to
announce, and taking back a generous one costs trust even when you do it correctly. A tightening
announced through a process customers were told about at launch is a term change. The same
tightening announced without one is a broken promise, and the people who hear about it are your
staff at the counter.

## Thresholds and timings

- **Effect on purchase behavior is not readable before several purchase cycles have passed.** Use
  two to three median interpurchase intervals for the category as the earliest honest reading. In a
  category where people buy twice a year, that is a year out, and saying so in month two is part of
  the job.
- **The first month's reading is operational.** Judge it on trend, not level: falling error volume,
  falling questions per location, no repeat of a closed class.
- **Redemption is read from the first cohort that can reach the redemption threshold**, not on a
  calendar date. If that cohort's balances clear the minimum and redemption stays near zero, act on
  the reward rather than waiting for more data.
- **Liability is tracked as a running balance:** accrued minus redeemed minus expired, against
  plan, every month. Expiry is what puts a ceiling on it: without one the balance has no
  contractual end date, and the forecast rests entirely on an assumption about when people redeem,
  which is the weakest input in the model. The pressure expiry puts on customers is a side
  effect of that, not the purpose.
- **The revision interval is the one published in the rules**, and you keep it even when nothing
  needs changing. An interval used only when the company wants something is not a process.

## Edge cases

- **No control group is possible once the program is everywhere.** The public half reaches
  everyone it has reached. Until then there are two ways out, and the first is cheap only while the
  rollout is unfinished: the locations of the later waves are untreated, so a randomized wave order
  inside clusters of comparable locations gives a comparison that lasts as long as the rollout
  (`launch-readiness-and-rollout.md`, step 7). Once the last wave lands, what remains is comparing
  members against their own pre-enrollment behavior. Say which one you used, because they support
  different claims: the first carries causation for the locations it covered, the second does
  not.
- **A location opened inside the comparison window.** The location itself cannot be read period
  over period at all until it has a before-period. The network total can, on windows that both sit
  before the opening or both sit after it; the alternative is to leave the location out of the
  total and say so. `launch-readiness-and-rollout.md` carries the same case for the rollout.
- **The first months land on a season.** Compare with a like-for-like period rather than the
  adjacent month. The launch campaign is a season of its own and gets the same treatment.
- **The launch was promoted.** Month one belongs to the campaign. The honest baseline starts after
  it ends, and the drop when it does is not a failure of the program.
- **The first expiry wave has not happened yet.** It is an event of its own, with its own support
  volume and its own reaction, and it is prepared for with notice rather than explained afterward.
- **A tier structure that nobody is climbing.** Where purchases are rare, the distance between
  tiers can exceed the customer's memory of the program. That is a design problem, and it goes to
  `loyalty-program-design` rather than being solved by messaging harder.
- **Two brands or two programs running side by side.** Read them separately before reading them
  together; a merged number hides which one is working.

## Failure modes

- **Penetration read as the goal.** The share of the base enrolled improves when new customer
  acquisition stops. Reported as success, it conceals the loss of inflow. This is why the control
  metric is the share of transactions identified rather than the share of the base enrolled, and
  why enrollment is always read next to new customer volume.
- **The launch is judged on the first quarter's revenue** in a category whose purchase cycle is
  longer than a quarter. The judgment arrives before the evidence could exist, and it is final.
- **Terms tightened without the announced process.** The margin comes back to the company and the
  complaint goes to the counter, so the people who absorb the decision are the ones who did not
  make it and cannot explain it.
- **The rise in members' average order value is read as the program's effect.** Members are a
  self-selected group of heavier buyers. The number is real; the attribution is not.
- **Nothing is being redeemed and it is reported as a saving.** An unredeemed balance is a
  liability that has not been discharged and a customer who has not come back. It is a warning,
  not a margin.
- **The program becomes an object to justify rather than to change.** The tell is a meeting agenda
  about how to present the program's results instead of what to alter in it. The exit criterion
  written at launch is what makes that conversation possible; without one, the program outlives
  everyone's belief in it.
