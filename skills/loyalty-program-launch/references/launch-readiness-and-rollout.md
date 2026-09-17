---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Readiness and rollout

A loyalty program is one of the few marketing mechanics that runs inside the payment itself. That
is what makes its launch a different kind of project from everything else in this library: a broken
email is embarrassing, a broken points calculation is a queue at the checkout and a refund. The
work runs from the decision to launch through to the first weeks of a live program in every
location.

The design is an input. This mechanic does not reopen it; it tests whether it can be run, then
runs it.

## Entry conditions

- The design is settled: what is earned, on what, at what rate, with what tiers and what expiry.
  Launching against a design still under discussion means building twice.
- Someone owns the work that happens after the data starts arriving, and they are in the role
  before launch rather than hired once the results are in. The public half is a cost; the person
  who turns it into revenue is the reason the cost is worth paying.
- One person coordinates the build across every system involved. Not one per system.

## Exit conditions

The program runs in every location and channel it was scoped for, the members of any previous
program are in it with their balances intact, the incident flow from launch has dropped back to
routine, and the first month's numbers are being read on the schedule set before launch.

Deciding not to launch is a normal outcome of steps 1 and 2, and it is cheapest here.

## Sequence

**1. Name what the public half buys, and check it has a consumer.** Write the purpose as one
measurable sentence: what changes, for which customers, measured how. "Increase loyalty" is not
one. "Identify the purchases we cannot attach to anyone today, so that the people behind them can
be segmented and contacted" is. Then confirm that the person who will do that work exists.

Businesses that should hear "don't launch" at this step: where the purchase quantity is fixed by
something other than desire, where purchases are rare enough that a member forgets the program
between them, and where nobody will be free to use the data. The first two have an answer in some
categories, which is to point the program at a different part of the basket rather than at the main
purchase. The third has none.

**2. Test the design for launchability.** Three questions, all answerable before any code:

- **Can the till compute it at the moment of payment, and in what time?** A rule that needs a
  round trip per line of the receipt behaves differently from one that needs a single call.
  Checkout latency is a business constraint here, not a technical detail: a queue turns customers
  away, and staff blame the program.
- **Can a member of staff explain it in one sentence?** Explaining it while bagging an order, not
  reading it off a card. A rule that needs a diagram will not be offered to anyone.
- **Will finance carry the liability?** Points are an obligation you have issued. How they are
  booked, and how expiry is treated, is agreed before the first accrual. Marketing does not get to
  decide this after launch.

Failing any of the three sends the design back to `loyalty-program-design`. Patching it here
produces a program nobody can describe.

**3. Write the rules as a document that outlives the launch.** It states what earns, what is
excluded from earning and from redeeming, where the program is valid, and how long points live. It
also states the interval at which the terms get reviewed and the way changes are announced, and
that is the part left out of most rule sets. Publishing the review interval up front is what makes
a later tightening survivable: a term nobody was told could change reads as a broken promise,
whatever notice you give.

**4. Sequence the build so the till is last.** Order the systems by what constrains what. The
things that set limits go first: pricing, order composition, the register of excluded categories,
customer records. The checkout goes last, because it depends on every parameter at once, and
starting there means rebuilding it after each of the others moves.

Where the existing systems are numerous or owned by different teams, the alternative to editing
each of them is a single module that talks to the loyalty processing on their behalf. Count the
systems that have to read or write a balance and the teams that own them: the module pays when that
count is high or the teams are separate, and it is overhead where one team owns both ends. What
belongs here is the ordering and the reason for it.

**5. Work the three readiness dimensions in parallel.**

*Legal.* The rules published; the lawful basis named; consent for messages taken separately from
enrollment; the disclosures your jurisdiction requires for an incentive offered in exchange for
data.

*Technical.* Load tested at the volume you expect on launch day, on the merged base rather than a
sample. Every action at the till and on the site logged, because the first weeks are spent
reconstructing what happened to individual balances. A defined behavior when the loyalty service
does not answer. A tested path for correcting a wrongly accrued or wrongly spent balance, which
will be needed on day one.

*Organizational.* Scripts and one-sentence explanations for everyone who faces a customer.
Answers to the objections staff hear at the counter. A channel where a location gets an answer the
same day. A support line sized against the questions a pilot location generates. Targets set on
identified transactions rather than on cards issued. See `enrollment-and-identification.md` for
why that distinction is the expensive one.

**6. Pilot in a few locations or in one channel.** Choose the pilot locations for comparability
with the rest of the network, not for being the best performers: a pilot in your strongest stores
does not transfer to the rest, and you will have no way to explain the gap when it appears.

Run it long enough for a first cohort to earn *and* redeem. A pilot that ends after accrual has
tested half the program. The redemption path at the till, partial payment by points, and the refund
of an order paid partly in points then all meet the network for the first time on the same day.

**7. Roll out in waves.** Size the wave from what training and support can absorb, not from
impatience. Between waves, look at whether the last one's questions have been answered and its
error classes closed; carrying an open class into the next wave multiplies it.

Decide the order of the waves before the first one opens. The locations not yet launched are an
untreated group, and the rollout is the only stretch in which you have one. Order them at random
inside each cluster of comparable locations and you hold a cluster-randomized comparison for the
length of the rollout, at no cost beyond writing the order down; order them by readiness or by
enthusiasm and the comparison is gone. `experiments-and-holdouts` owns the design and the sample
arithmetic. What belongs here is the timing: the chance exists only until the order is fixed.

The same wave machinery runs a change to a program that is already live: `loyalty-program-design`
decides that a change goes out in waves and what each wave has to be taught, and hands the running
of them here. Two things differ from a launch. The untreated group is the later waves of the
existing base, not locations without a program, so the comparison is between the old rule and the
new one. And there is no pilot to measure questions per unit on, so the first wave is sized from
the launch's own history and the quotient is recomputed from it before the second.

**8. Cut over, if a program already exists.** The order that works: freeze, migrate, verify,
resume, with the frozen window announced in advance. Members move with their balances. Tiers are
recomputed from each member's own history against the new thresholds rather than reset to the
floor. Expiry clocks restart at the cutover, so that nobody's balance burns because of a migration
they did not ask for. The restart moves the ceiling on the liability out by a full expiry period,
for the whole migrated base at once, so the liability forecast is redone against the new dates
before the cutover rather than discovered after it. Raw logs are kept at every step of any merge,
because the first support question will be about one specific person's points, and the answer has
to be reconstructible.

Where two programs are being merged, expect the same person to exist twice with different details.
Deduplication rules and the priority between conflicting values are decided before the import, not
during it. Then verify on the merged data in a test environment before the live import.

## Thresholds and timings

- **Pilot length: at least one full earn-then-redeem cycle for the category.** In practice, no
  shorter than two median interpurchase intervals, and long enough for a first cohort to clear
  whatever minimum makes redemption possible.
- **Wave size: support capacity divided by questions per unit per week**, both measured during the
  pilot rather than estimated. The unit is whatever the wave is made of: a location where the
  rollout is geographic, a channel where it is not. A wave larger than that quotient produces a
  queue of unanswered stores, and an unanswered store reads as a resistant one. A rollout by
  channel has too few units for the quotient to bind, and the limit there is the number of order
  paths one support shift can hold open at once, measured the same way.
- **The frozen window at cutover comes from a measured import, not an estimate.** Measure the
  import speed during development, when the volume is already known, and announce the window
  before it starts.
- **Infrastructure readiness is not a constant.** With a ready platform and a single channel it is
  a matter of days; with in-house checkout software and several order paths it is months. An
  estimate made before the contact points have been inventoried comes out wrong by a multiple, and
  the correction runs upward.
- **Daily incident review after each wave, until first-contact errors fall to routine.** The
  trigger for stopping is the trend, not a date: classes of error closing, no repeat of a closed
  one, declining volume. A span fixed in advance is either too short for the first wave or too long
  for the last.

## Edge cases

- **The program runs in locations you do not own:** franchise, partner, concession. Who bears the
  cost of the discount, and who reimburses whom, gets settled before launch. Settlement between
  owners can be deliberately deferred to make the launch possible, with a stated date to revisit;
  what cannot happen is the question going unasked and surfacing as a refusal to participate
  halfway through the rollout.
- **The checkout system cannot be restricted by territory.** Then the pilot is a channel, not a
  region: click-and-collect, delivery, the app. A phased rollout by channel is available even when
  a geographic one is not.
- **The processing is unreachable.** The sale must complete without points and reconcile
  afterward. A till that blocks payment when the loyalty service times out has turned a marketing
  program into an outage.
- **Categories that cannot participate.** Alcohol, tobacco, gift cards, regulated goods, orders
  placed through a third-party platform. The register of exclusions exists before the first
  accrual; built afterward, it means recalculating balances people have already seen.
- **Members earn in one location and redeem in another.** Decide whether that is settled between
  owners or absorbed, and say which. The decision is defensible either way; the absence of one is
  not.
- **A location opens during the rollout.** Which reading breaks depends on what is being compared.
  The location itself has no before-period and stays out of every period-over-period reading until
  it has one. The network total does have one, and the new location inflates its after-period, so
  read the total on windows that both sit before the opening or both sit after it.
  `first-months-and-course-correction.md` carries the same case for the comparison window.

## Failure modes

- **The date came from a marketing calendar rather than from readiness.** The tell is readiness
  items being closed retroactively, and a test environment that does not resemble production.
  Customers then find the first errors, and the first month goes on support work instead of on the
  program.
- **Nobody can state the purpose in one measurable sentence.** The program still launches, because
  the date exists, and becomes the thing that is too expensive to run and too public to withdraw.
  Write the exit criterion into the launch document while it is still a hypothetical: what would
  have to be true for the program to be shut down.
- **Coordination by one project manager per system.** Priorities diverge, each team optimizes its
  own piece, and the mismatch surfaces at the seams during integration testing, by which point each
  team has already built against its own reading.
- **The pilot ran in the best locations.** Its numbers do not transfer, and the rollout looks like
  a failure against a benchmark that was never real.
- **The pilot ended before anyone redeemed.** The redemption path breaks in front of the whole
  network at once, at the moment when support is already busiest.
- **Finance meets the liability after launch.** The first serious conversation about what points
  cost happens when the balance is already issued and publicly promised, which leaves only bad
  options: devalue and lose trust, or carry a number nobody planned for.
