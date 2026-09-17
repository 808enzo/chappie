---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-09
---

# Vocabulary for lapse-and-winback

The terms all three mechanics assume. Six of them are shared with neighboring skills under
different meanings, and those are marked at the end.

## Qualifying action

The one action whose absence constitutes lapse: a purchase, an order, a login to the product, a
use of it. Named before the threshold, because the threshold is measured on it.

## Lapse threshold

The time without the qualifying action after which somebody counts as lapsed. A multiple of your
own median interpurchase interval, not a number of days from outside. It carries a date, because
it drifts with the assortment and the price. It is a threshold of starting, and it falls earlier
than the deletion threshold in `list-building`, which sits on the same axis and marks the end
rather than the start.

## Threshold step

One of several threshold values, each with its own route. You have as many steps as you have
distinguishable routes.

## Commercial silence

The axis of absence measured on the qualifying action. It decides whether the person is gone.

## Channel silence

The axis of absence measured on response inside a channel. It decides which route can still reach
them and what happens to the address. It does not decide whether they lapsed.

## Addressable population

The lapsed minus four out of scope classes: out of the category by fact, said so out loud, natural
departure, and a business model with no return in it. Sizing happens after the subtraction, not
before.

## Pre-lapse signal

An observed deviation in somebody who is not yet past the threshold. Two classes: a drop in level
relative to their own norm, and an alarming action.

## Own norm

The level a specific unit ran at in an earlier comparable period. The basis of comparison is that
unit, not the rest of the base.

## Scoring zone

A range of simultaneously firing criteria with an action attached: look, or go. Criteria score one
point each and carry no weights.

## Validation

The step between the score and the action: a check that the signal matches the state. Performed by
a person where the action is expensive. Where the units are many and cheap, by a second independent
reading of the same drop or by a diagnostic touch whose reply is the validation, and not by the
recency recheck at selection, which answers a different question.

## Return attempt

A deliberate, finite sequence of touches addressed to the cohort that crossed the threshold in a
period. It has a declared end and an outcome for everybody who entered it.

## Attempt window

The time after the last touch during which a return still counts toward the attempt. Derived from
your own time between a response and the qualifying action.

## Argument step

A level of escalation: non monetary, small monetary, larger monetary. It rises only after the
previous step failed on this same person.

## Step distinguishability

The property of adjacent steps producing different responses. Checked before the ladder is built;
indistinguishable steps collapse into one.

## Cascade

The order of channels inside one touch, built on reachability and cost.

## Attempt outcome

One of five states on exit, each with an address: returned, answered without acting, silent,
refused, and never attempted. The first four describe what somebody did with an attempt that
reached them; the fifth holds the unreachable, the suppressed and the control group, and it carries
no demotion and no removal.

## Repeat attempt

A second attempt on the same person, bounded by the outcome they left with. Somebody who answered
without acting waits at least the first attempt's window. Somebody silent waits that long and also
needs a channel that did not exist for them last time. Somebody who refused gets no repeat, and
somebody never attempted gets a first attempt instead of one.

## Return rate

The control metric: people who performed the qualifying action inside the attempt window, divided
by everybody who crossed the threshold in the period. The denominator includes people no channel
reached.

## Returner survival

Whether a returner reached their next qualifying action inside their own interval. It catches the
attempt that produces one order and an immediate second lapse.

## Words this skill shares with its neighbors

- **Reactivation.** In `email-program` it is work with a tier inside the standing program: the
  dormant tier gets mailed less. Here it is a separate finite campaign with a target action and an
  outcome. Same word, different objects, and this skill never calls a tier cadence an attempt.
- **Dormant.** In `list-building` it is a state of the record, one of three states of silence
  leading out of the active base. Here it is a population under an attempt. A record can be dormant
  and not under an attempt, and the other way round.
- **Window.** In `welcome-and-activation` the window runs from the moment somebody appeared, and
  inside it they have not lapsed. Here the window runs from the last touch of the attempt and
  serves the denominator. They share nothing but the word.
- **Return.** In `loyalty-program-design` a return is a returned product, and the return window is
  what the delay on accrued value is measured from. Here a return is a person coming back. Both
  senses appear in this skill, which is why neither is ever written without its object.
- **Signal.** In `program-audit-and-ops` a signal says an object stopped working. Here it says a
  person is about to leave. The first is read off a system, the second off a person.
- **Churn.** In `metric-definitions` it is a metric with a numerator, a denominator and a window.
  Here it is a population selected by a threshold. This skill never calls its segment a metric.
