---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-09
---

# The return attempt: the sequence, the escalation, the end, and the outcome

The unit here is **the attempt**: the cohort of people who crossed the threshold in a period,
together with the outcome each of them ended up with. Not a send and not a campaign. People who
were never reachable are inside this unit, and they are inside its denominator.

## Entry conditions

`defining-lapse.md` has run: the list exists, the out of scope classes are subtracted, recency is
rechecked at selection. Consent and reachability are known per channel.

A unit handed over by a neighbor arrives already gone and carries a reason code, and the code picks the
branch at entry. From `subscription-retention`: *payment*, a subscription that expired without a
decision, whose first message is the way back with an update of the payment method, not an offer; and
*cancel*, with the reason from the shared list. From `b2b-retention`: *non-renewal*, and *non-payment*,
whose first message is the way back together with settling the debt. The sign of a breach: one
attempt runs for every code. The remedy: branch by code at entry.

## Exit conditions

The attempt closed on the date it said it would, every person who entered has an outcome with an
address on it, and the last message said what happens next.

## Steps

**1. One target action per attempt, and it is the action whose absence defined the lapse.** Lapse
defined on purchases means the target action is a purchase, and an email open is not a success.

This has to be written down explicitly, because a cheaper definition is available and will be
used if you do not rule it out: opened one message from the sequence, therefore reactivated. It
makes the attempt measurable and meaningless at the same time, and it can coexist in one document
with a definition of lapse based on purchases without anybody noticing the two do not match.

**2. Ask before you pay.** The first touch is a question about the reason rather than a discount:
a short survey, a choice among a few options, an offer of help. Three reasons for that order. The
cause of leaving is not always addressable with money. The answer segments the population for the
second touch. And an argument handed out immediately also goes to everybody who would have come
back without one. Two entry codes change the first touch: *payment* and *non-payment* open with the
way back, not with the question (entry conditions).

**When to stop branching on the answer.** Routing by answer pays for itself while the answers are
spread out. Once one answer takes an overwhelming share, the branch collapses: the route simplifies
into the direct offer that answers it. The trigger is the share of a single option over a period,
and the level is set by what maintaining the branches costs you rather than by a round number.

**3. Derive the number of touches and the spacing from the attempt window, and the window from
your own response time.** The attempt window is how long you keep counting a return after the last
touch before you close the attempt and issue outcomes. It comes from your own time between a
response and the qualifying action, not from the calendar and not from an estimate. The gap is
worth measuring rather than guessing, because the guess and the measurement can differ by multiples
in either direction: where the category is bought on a weekly rhythm, a code handed out midweek is
used at the weekend, and a window sized for two days closes before those returns land.

Start with **three to five touches**, each carrying its own argument. That applies where there is a
regular program with a known habitual cadence; the spacing inside the attempt holds to that cadence
or runs slightly tighter. The first attempt produces your own distribution of time to return, and
the window and the number of touches get recomputed from it.

**4. Escalate the argument by steps, and only after the previous step failed on this same person.**
The order runs from a non monetary argument (a reminder, a selection, help, what is new in the
product) to a small monetary one to a larger one. The maximum handed out immediately leaves the
attempt with no steps and teaches people to wait.

**A step has to be distinguishable.** Before building a ladder, check that adjacent steps produce
different responses. Two depths of discount can perform the same as each other while both differ
from no discount at all, and in that case the ladder collapses into two rungs: without an argument
and with one. The economics of each step, the depth ceiling and the fate of an issued promise
belong to `offer-design`.

**5. Build the channel cascade on reachability and cost rather than on preference.** Channels that
cost nothing and can reach the person go first; the paid channel goes last and only to the people
the cheap ones did not reach. The cascade differs by threshold step: the longer somebody has been
absent, the less likely the cheap channel still reaches them, and the earlier the paid channel
appears in their cascade.

Three things are checked before each send in each channel: consent in that channel, the gap since
the last message to this person in that channel, and the target action (step 6). The gap inside a
channel belongs to that channel's skill (`email-program`, `push-notifications`), and the frequency cap
across all programs to `contact-orchestration`; what happens here is the check, not the policy.

**6. Stop the attempt on the target action, checked immediately before every send.** The person
bought, so the rest of the attempt does not go, regardless of whether the purchase came through
the message. Checking a click instead of the action is what sends a message about how much you
miss somebody to a person who ordered in the store yesterday.

**7. Declare the end of the attempt in advance and reach it.** An attempt with no end turns the
lapsed into a permanent segment nobody retires, and it distorts every denominator for as long as
it stands. Five outcomes, each with an address. Four of them say what a person did with an attempt
that reached them. The fifth is for the people it never reached, and it is the one no report will
produce for you:

| Outcome | What happened | Where it goes |
|---|---|---|
| Returned | the target action happened | the regular program; a second purchase is `repeat-purchase` |
| Answered, did not buy | at least one touch went out, a response came back, no action followed | the reason goes to `voice-of-customer`; the person stays lapsed, because a response is not the qualifying action, and their recency keeps counting from their last qualifying action rather than from the answer |
| Silent | at least one touch went out and nothing came back | tier demotion is `email-program`; leaving the active base is `list-building` |
| Refused | unsubscribed, asked you to stop | `consent-and-preferences`; there is no repeat attempt |
| Never attempted | no touch went out at all: no channel with both consent and reachability, suppressed by the frequency cap, or held in the control group | reachability is `martech-stack` and `list-building`, a suppressed touch is `contact-orchestration`, a held one is `experiments-and-holdouts`. It carries no demotion and no removal, because nothing in it is behavior |

The line between the last two decides who gets demoted and whose record leaves the active base.
Collapse them into one row and you hand `email-program` and `list-building` somebody you never sent
anything to, and you demote a control group for being a control group.

The last message of the attempt says what happens next, because after it there is nowhere left to
say it.

**8. Bound the repeat attempt by outcome, because one blanket condition binds nobody.** A repeat
is legitimate: an attempt that failed does not prove the person is unreachable forever. The
condition that makes it legitimate differs by the outcome they left with, and a rule written for
all four at once applies to none of them.

- **Answered, did not buy.** This is the outcome a repeat is for, and the pause is what bounds it:
  not shorter than the first attempt's window, expressed in your own windows rather than in months.
  Their recency was not reset by the answer, so a repeat here is a second attempt on somebody still
  lapsed rather than a fresh crossing of the threshold.
- **Silent.** A repeat down the same cascade changes nothing: what they ran out of is not
  arguments, it is a channel. So the repeat is conditional on the cascade having changed, meaning a
  channel now exists that did not exist for them last time, and it carries the same pause.
- **Refused.** No repeat, and the grounds are the legal ones in `SKILL.md` rather than tactical
  ones.
- **Never attempted.** Not a repeat at all. You tried nothing on them, so once you fix the channel
  they get a first attempt, and the pause has nothing to bound.

**9. Read the result as a cohort, not as a campaign.** The denominator is everybody who crossed
the threshold in the period, including the unreachable and the suppressed, which is the population
the fifth outcome names. The full reading is in the control metric section of `SKILL.md`.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Attempt window | your own time between a response and the qualifying action |
| Number of touches | starting point: three to five; recomputed from your first distribution of time to return |
| Spacing between touches | the habitual cadence of the regular program, or slightly tighter |
| Moment the target action is checked | before every send, not at assembly |
| Gap since the last message | in-channel gap owned by the channel's skill, cap across channels by `contact-orchestration`; checked here |
| Pause before a repeat attempt | not shorter than the first attempt's window |
| When the answer branch collapses | the share of a single answer at which maintaining branches costs more than it returns |

## Edge cases

- **The person came back in another channel or offline.** The attempt stops on the action, not on
  a click. This needs the stitched history that `defining-lapse.md` requires as an entry condition.
- **A public promotion runs over the attempt.** The person gets the same discount without any
  attempt, and the step loses its meaning. Collisions between offers on one order belong to
  `offer-design`; what belongs here is knowing the calendar before launch (`promo-calendar`).
- **A seasonal peak inside the attempt window.** People return on their own and the result reads
  high. The only cure is a control group held through the peak.
- **An address that unsubscribed years ago.** It does not get revived. A win-back is assembled out
  of old records by construction, and that is what puts an opt out from years ago within its reach
  in the first place.
- **B2B: the contact changed and the account did not.** A person left, not a customer. The attempt
  is addressed to the successor and to the budget holder rather than to a silent address, and the
  departed contact is a reason to update the record rather than a row in a lapsed segment.
- **Somebody inside the welcome window.** They have not lapsed: the absence horizon has not
  started (`welcome-and-activation`).
- **A short absence with an action already started.** Not here: an unfinished checkout or an unused
  code is `triggered-messages`.

## Failure mode

**The attempt turns into a permanent discount channel.** The argument is handed out past the
threshold, the threshold is reached by going quiet, and part of the base learns to go quiet until
the threshold. From the outside it looks like a working mechanic: returns happen and conversion on
the step is rising.

Three signs, all computed on your own data:

1. the interpurchase interval of returners drifts up toward the threshold across successive
   attempts: people who used to come back sooner now come back exactly when it pays. Read it as a
   drift and not as one reading, because a single reading of "shorter than the threshold" is also
   the signature of a borrowed threshold, which is the failure mode in `defining-lapse.md` and has
   the opposite repair;
2. the share of returners who bought only with the argument attached grows from attempt to attempt;
3. the control group returns nearly as often as the group that got the argument.

The third is decisive and needs a control group held permanently rather than for one test
(`experiments-and-holdouts`). Without it the first two read as success.

The third sign is also shared with the failure mode in `defining-lapse.md`: a control group that
returns as often as the treated group says the argument is not causing the returns, and it does not
say why. Sign 1 tells the two apart, so read them in that order.

**The second failure mode is an attempt with no end.** The lapsed segment never empties because no
outcome is issued, people accumulate, the attempt runs indefinitely, and every neighboring metric's
denominator degrades. The sign is a segment whose size only ever grows.
