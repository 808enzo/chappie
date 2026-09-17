---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Triggered messages vocabulary

The terms the three mechanics assume. These definitions are scoped to this skill. The general
dictionary of marketing metrics, with formulas and denominators, belongs to `metric-definitions`.

In most teams the word *trigger* means the message. Everything here follows from separating the
rule from the message it sends, so settle that first.

## Trigger

The rule that binds a moment to a reply. The message and the platform scenario that carries it sit
downstream of it. You can reproduce, review and retire a rule; a scenario switched on in an
interface can only be switched off again by whoever remembers it is there.

## Firing event

The thing that sets the rule off. Five origins, and each one carries a different guard:

- **A customer action:** viewed, browsed, added to cart, started checkout. It ages in hours.
- **A catalog change concerning this person:** back in stock, price drop, stock running low. The
  object can change between firing and delivery, and the interest behind the change may be old.
- **A date that arrives:** birthday, purchase anniversary, expiry, an upcoming appointment. The
  attribute behind it is self-reported and editable.
- **A short-horizon absence:** started checkout and did not finish, received a code and did not use
  it. An absence fires it, tied to an action already begun.
- **A state the program records or computes:** an order delivered, a conversation closed, a move
  between groups of a grid. The state belongs to another system's map. An ask for feedback fires
  here, with the delay and the ration `voice-of-customer` sets.

Long-horizon absence, meaning someone stopped buying or stopped opening at all, belongs to
`lapse-and-winback`.

## Eligibility filter

The conditions that drop a person before the first message: bought recently, no valid consent,
already in a higher-priority flow, already received this flow inside the guard period. Broken
eligibility fails in both directions, too many people or almost nobody, and neither shows in an
open rate. The count of entries against fire volume shows both.

## Delay

The time between the firing event and the first message. Derived from the category's decision
cycle and from the strength of the signal, never from the platform default, which is a starting
point rather than a setting.

## Entry moment

The end of the session, or the arrival of the date, rather than the click inside the session. An
open tab is not an abandonment: while the person can still come back, nothing has happened.

## Object of the message

The item, cart, date or order the message is about, plus the system that owns it. Name the owner:
the flow reads that object twice, once at firing and once before sending, and the two reads have
to come from the same place.

## Recheck before sending

The verification at delivery time that the message should still go and that the live values it
quotes still hold: availability, price, whether the cart is still unpaid and not emptied, consent,
and whether the person has bought since. It does not re-read the event: the cart an abandoned cart
message shows stays as it was at firing (`personalization` calls it a frozen value). A live value
assembled at firing time and delivered later is wrong in exactly the share of cases where it moved.

## Event expiry

The age past which the event stops being an occasion and the flow does not start. A cart from
several decision cycles ago competes with a purchase already made somewhere else rather than with
forgetfulness. For a catalog change the age runs from the person's own action behind it (the save,
the view, the cart). Expiry is also the latest a first message may leave, deferral included, which
is the figure `email-copy` adds a retry ceiling to.

## Flow

The sequence of steps one trigger starts. One step is a complete flow. Length is a decision, not a
default.

## Step

One message carrying one argument. Two arguments in one message cancel each other; the same
argument twice reads as pestering.

## Cascade

Moving to the next channel because the previous one did not land. Ordered from cheap and mild to
expensive and insistent, with a wait per channel set by how fast that channel is read. Equal waits
in every channel mean a volley rather than a cascade.

## Stop condition

Any of the conditions that end the flow early: conversion, an order placed, the occasion
disappearing, entry into a higher-priority flow, a reply, an unsubscribe, a withdrawal or deletion
request. You check them before every step, not only at entry.

## Branch

A variant inside a flow. A variant built as a separate flow is a clone, and clones produce
duplicate sends and unreadable reporting.

## Entry

A firing that passed eligibility, written at that moment and before anything is sent, in the
treated group and in the holdout alike. You measure the flow in entries, and they are the
denominator of the control metric. A repeat firing while the entry's window is open is not a new
entry.

## Fire volume

The count of firings in a period, taken before eligibility and including firings with no address.
The gap between fire volume and entries tells you how much of the occasion your filters and the
missing addresses remove.

## Collision

Two flows firing on one person in the same moment. You resolve it with a priority order written
into the configuration. Priority between campaigns and the cap across all channels belong to
`contact-orchestration`; the order inside the automated layer belongs to this skill.

## Gap inside the set

The minimum distance between two triggered messages from different flows to one person, plus a
ceiling per period that counts every automated message. It exists so automated flows do not
interrupt each other, and it is enforced separately from the overall contact cap because flows fire
without a schedule. Steps and cascade escalations inside one flow keep their own timing.

## Dormant trigger

A flow that is switched on and has stopped firing. Reports that show rates rather than counts miss
it: the few entries left still convert at a healthy-looking rate.

## Retirement condition

The condition under which the flow stops earning the attention it costs. Name it at build time, so
switching the flow off is a check rather than an argument; the review in
`trigger-set-and-collisions.md` retires flows that never had one.

## Target action

The one action a flow exists for, written with the flow. For a purchase it is an order paid and not
canceled by the reading date, while the flow itself stops earlier, on the order being placed.
`welcome-and-activation` uses the same term on a different unit, a person's arrival rather than an
entry.

## Conversion per entry, the control metric

**What it measures.** The share of entries into a flow that reach the target action inside a fixed
window.

- **Numerator:** entries whose person completed the target action inside the window, in any channel
  and whether or not they touched a message. No credit rule: the holdout received no message to
  credit, so a credited numerator is zero there by construction.
- **Denominator:** entries, including those that received nothing because the recheck, a stop
  condition, a collision or an unavailable channel held every step. Not sends, which rise every
  time you add a step. Not opens, which move with anything that touches open counting.
- **Window:** fixed, opened at entry in both groups, and no shorter than the last step plus the wait
  that step's response needs. On a shorter window the later steps count as zero.

**How to read it.** Against a holdout drawn from entries, meaning people who fired the trigger and
received nothing from the flow. A held-out entry stays a member of the flow for the rules of the
set, so junior flows on the same object and the campaign on the same subject stay quiet for it too.
Everyone in a triggered flow has already shown intent, so the flow collects conversions that would
have happened anyway, and without a holdout it looks successful in every report. Holdout design and
the assignment log belong to `experiments-and-holdouts`. Read a period once its window and the
cancellation period of its orders have both closed.

**Read beside it.** The rate per entry rises when eligibility narrows to the hottest firings, while
the flow produces fewer extra orders. Keep the extra conversions per period (treated rate minus
holdout rate, times treated entries) and entries as a share of fire volume next to it.

**Where the benchmark is.** None exists for this metric: the value depends on which event you
picked, and a published figure would need a holdout drawn from entries. A published cart recovery
rate is a different ratio, recovered carts over abandoned carts or over messages sent, credited by
the sender and read without a holdout; a figure like that belongs in `references/` with its source,
market and sample size, and it is read beside the cart flow, not against this metric. Say so, then
build a self-baseline: one point per period, computed on that period's entries once their window
has closed, eight to twelve points, and read later points against your own median and spread. A
period too short to hold a readable number of entries is lengthened rather than skipped.
