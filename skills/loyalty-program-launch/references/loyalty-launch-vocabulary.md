---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Vocabulary of a loyalty launch

The three mechanics assume these terms. Three of them, *penetration*, *member* and *carrier*, mean
different things to different people in the same meeting, and the readings they produce point at
opposite conclusions. Settle all three before a discussion rather than during one.

## The two halves

**Public half.** The part of the program the customer sees: the card, the points, the tiers, the
discount. It spends margin, and what it buys is the ability to attach a purchase to a known
person. Read as a cost center by default.

**Targeted marketing.** The work done with the data the public half collects: segmentation,
selection, offers, timing. This is where a loyalty program earns back what it spends. A program
with a public half and no targeted marketing is a permanent discount with extra steps.

## Identification

**Identified transaction.** A purchase attached to a known customer. The unit of everything
downstream: an unidentified purchase cannot be segmented, targeted, attributed or won back.

**Penetration.** A share. Two of them are in play here, and neither is the one next door:

- *Penetration into transactions*: identified transactions over all transactions in a window. This
  is the control metric of `loyalty-program-launch`, because it measures what the public half was
  bought to produce.
- *Penetration into the base*: enrolled members over all known customers. This one rises when new
  customer acquisition stops, so it improves when the business gets worse. Useful only when read
  next to new customer volume.

The first of those has a revenue twin, identified revenue over all revenue, and the two give
different numbers on the same period: revenue weights each transaction by its basket, so the two
separate by however much identified baskets differ from unidentified ones. Say which denominator
you are on. The control metric counts transactions, because a transaction is the unit that either
can or cannot be attached to somebody.

`loyalty-program-design` uses the word for a third share: the part of a basket actually paid in
currency, against the redemption depth its rules allow. That one measures spending points, and
these two measure recognizing people.

Name which one you mean, and name the window. `metric-definitions` owns the general form of a
metric definition; this file separates the variants because they get used interchangeably in the
same sentence.

**Member identifier.** The number that identifies a participant. It survives every change of
carrier and is never reissued when the carrier changes.

**Carrier.** The form in which a member presents the identifier at the point of purchase: plastic
card, wallet pass, app, a phone number spoken aloud. The carrier is replaceable; the identifier is
not. **Two neighbors use the word for something else.** In `offer-design` a carrier is whatever
presents a promise, and its rule that a unique carrier belongs to a person while a shared one
belongs to nobody is the rule behind the household card in `enrollment-and-identification.md`. In
`messaging-channels` a carrier is the telecom operator.

## States a member can be in

**Enrolled.** Purchases can be attached to this person.

**Activated.** A contact channel is confirmed and this person can be reached. Enrollment without
activation gives attribution and no channel; both shares are tracked separately, and activation
cannot exceed enrollment, because activating means confirming a channel on a record that already
exists. **`welcome-and-activation` uses the word for something else**, the moment somebody gets a
first value out of the product. That one is about what the person received; this one is about
whether a message can reach them at all.

**Active member.** A member who took a defined action inside a named window. Both the action and
the window are stated whenever the term is used; "active" without them is not a measurement. This
is the second reading of *member*: the first is a record that exists, and a base can gain records
for a year while the number of people recognized at a till stands still. The two readings point at
opposite conclusions about the same program, which is why the control metric counts transactions
rather than people.

## Money and obligation

**Processing.** The system that computes accrual and redemption at the moment of payment. Its
response time is a business constraint at the till, not a technical detail.

**Points liability.** Accrued minus redeemed minus expired: an obligation the company has issued
and not yet discharged. Expiry exists so that this number can be planned.

**Redemption share.** Points redeemed over points accrued in a period. Read together with the
liability: a low share means the reward is not wanted or is out of reach, and it is a warning
rather than a saving.

**Program rules.** The published document setting out what earns, what is excluded, where the
program applies, how long points live, and how the terms themselves may change. The last of these
is the part that makes a later change survivable.

## Stages of a launch

**Pilot.** A limited run in a few locations or one channel, chosen for comparability with the rest
of the network, and long enough to cover one full earn-then-redeem cycle.

**Wave.** One increment of the rollout, sized by what training and support can absorb rather than
by ambition.

**Cutover.** The move from an existing program to a new one: freeze, migrate, verify, resume.
Members arrive with their balances; tiers are recomputed from each member's own history; expiry
clocks restart so that a migration burns nobody's points. Here it is an interval with four stages.
In `martech-stack` the same word is a moment, the unit of a migration: the instant one flow stops
on the old platform and starts on the new one. A program cutover contains many of those.

**Frozen window.** The announced interval during which some operations, redemption above all, are
unavailable. Its length comes from a measured import, and it is announced before it starts.
