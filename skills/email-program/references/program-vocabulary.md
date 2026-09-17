---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-04
---

# Program vocabulary

The terms the three mechanics assume. These definitions are scoped to this skill. The general
dictionary of marketing metrics, with formulas and denominators, belongs to `metric-definitions`.

## Program cycle

The planning unit of the program: the median interval between purchases in the category for a
retail business, the billing period for a subscription, the deal cycle for B2B.

Derive it, do not assume it. Take completed purchase pairs over a long enough history and use
the median rather than the mean, because a handful of very long gaps drags a mean into
uselessness. Every window, gap and review point in this skill is expressed in cycles, so that it
survives a move to another category.

## Send inventory

The list of everything that leaves the channel in one cycle: manual campaigns, automated flows,
service messages. One line per send, each with an owner. It exists to show the difference
between the planned program and the real one, which is larger than teams expect and hides in the
automated flows.

## Touch load

Messages received by **one person** over a period, counted across every send type. The unit is
per person, not per program. A program sending four times a cycle can still put twelve messages
in front of one recipient once you count the flows. Load is the number to argue about. Volume of
sends is not.

Load is read per person and the gap is enforced per address, and the two come apart on anyone who
sits in the base twice: a work address and a personal one that `list-building` has linked without
merging are two records, each resting on its own timer, and the person receives everything twice.
Where records are linked, run the gap on the linked group rather than on the row, and where they
are not linked yet, that is `list-building`'s to resolve before the load number means anything.

## Engagement window

The recency period you use to classify a subscriber. Derive it as the period within which most
responses to a typical send arrive, floored at one program cycle. A window shorter than the
purchase cycle files healthy customers as dormant.

## Engagement tiers

Four states plus one waiting room, assigned by recency of response inside the engagement window
and recalculated once per cycle. Recency is the whole axis. How often somebody responds is
`rfm-segments`' frequency axis, and a tier that counts frequency as well stops being the cut the
neighboring skills borrow from here.

- **Active.** Responded inside the window, where responding means opening or clicking rather than
  buying. Receives the base rhythm. `deliverability` uses the same reading, because it is the only
  one a mailbox provider can see.
- **Occasional.** Responded, but before the window closed on them. Receives a fraction of the
  base rhythm.
- **Dormant.** No response across a long multiple of the window. Anchor sends only, or a
  deliberate return attempt owned by `lapse-and-winback`.
- **Suppressed.** No longer eligible for marketing mail, by law, by their own choice, or by
  technical state. Service messages and mandatory notices only.
- **Unclassified.** Nobody has had the chance to respond yet: a new subscriber, an account handed
  over by `b2b-lifecycle`, anyone whose history is shorter than one engagement window. File them
  as dormant and the classification confirms itself, because the dormant rhythm is anchors only
  and they never receive enough mail to produce the response the tier is computed from. They carry
  the base rhythm until one full window has passed, and take a tier after that. Before the handover
  they belong to `welcome-and-activation`.

A tier belongs to the email program, not to the customer. Someone dormant here can be active in
another channel, and merging the two views produces contradictory sends.

**A demotion reads silence, and silence has two causes.** Somebody who did not read and somebody
whose mail did not arrive look identical from here, and you answer both by mailing them less, which
destroys the evidence. Split a wave of demotions by mailbox provider before you act on it.
Demotions concentrated in one provider are placement, which is `deliverability`'s work rather than
a tier change; demotions spread across providers are what they look like.

**Sunset.** The point at which somebody stops receiving the standing program at all. Set it here,
in windows rather than in months: after a stated number of engagement windows with no response, the
person gets one deliberate return attempt (`lapse-and-winback`) and nothing else from the program.
What happens to the record afterward is `list-building`'s, and whether the address is reachable at
all is `deliverability`'s. Without a sunset the dormant tier only grows, and every reach figure you
report counts people the program has already given up on.

## Slot

A recurring send in the calendar, defined by five things: purpose, recipient tier, frequency,
owner, and the fallback when there is no material. A send without a slot is a one-off, and a
program made of one-offs has no rhythm to measure. `in-product-messaging` uses the same word for a
screen and format pair, which is a different object; a bare "slot" here is always this one.

## Anchor send

A send tied to something that cannot move: a demand peak, a product launch, a program milestone.
You place anchors on the calendar first, and inside the standing program they are the only sends
the dormant tier receives, the deliberate return attempt of `lapse-and-winback` being outside the
standing program rather than an exception to this.

**Where the peak is comes from `promo-calendar`.** That skill builds the register of the year's
windows first, one row per window with its occasion, dates, audience scope and depth, and the
channel calendar is laid out around it. A channel cannot work out where demand peaks; it can only
read it off the register. An anchor of this skill is a row of that register, and a program that
lays anchors from its own sense of the season will fit the year around its own rhythm and meet the
peak late.

## Send types

- **Campaign.** Assembled by a person, addressed to a segment, scheduled.
- **Automated.** Fired by a customer event or by the absence of one. `triggered-messages` owns
  it. It appears here because it consumes touch load.
- **Service.** The consequence of a transaction: confirmations, status, receipts. Most regimes
  allow it regardless of marketing consent, because it is not marketing, which is also why you
  do not quietly add marketing content to it. Under CAN-SPAM the test is the primary purpose of
  the message, read from the subject line and the beginning of the body, so a service message with
  a promotional block in it is a commercial message with all the duties attached. **Who this does
  not bind:** the other three regimes, which draw the line between service and marketing in their
  own terms (`SKILL.md`, and `consent-and-preferences` for the basis behind either class).
- **Mandatory notice.** What you owe somebody by law or by contract: a recall or safety notice, a
  change of terms, points about to expire, a balance statement. It is neither a consequence of a
  transaction nor marketing, so without a name of its own you will file it as a campaign and your
  promotion rules will hold it back. Never suppressed. The send classes and their precedence are
  `contact-orchestration`'s: service, mandatory notice, perishable and personal, automated flow,
  campaign. This skill uses those. Its own three-way split of campaign, automated and service says
  who assembles a send, not which of them yields.

## Suppression

Two kinds, and the difference is whether you may ever override the rule.

- **Hard suppression.** Legal or technical, enforced by the platform: no valid consent where
  consent is required, unsubscribed, hard-bounced, on the suppression list. Never overridden.
  A pause the person asked for belongs here too and behaves differently from the rest: it carries
  an end date, it releases itself, and the resume lands in the tier's cadence rather than in the
  queue that piled up during it. `consent-and-preferences` records the instruction and its end
  date; applying it to an audience, and resuming into the rhythm, is this skill's.
- **Program suppression.** Rules the program sets for itself: minimum gap between touches, recent
  purchase, higher-priority flow in progress, open support incident. Tunable, reviewed once per
  cycle. None of them reaches a mandatory notice: a rule written to space out promotions has no
  business holding back a recall or a change of terms.

**Suppression scope.** How far one prohibition reaches: the address or channel, the sender as a
whole, one brand, one message type, or one program. Hard suppression reaches at least as far as
the brand, and further when the reason is the address itself; program suppression stops at its own
program. The scope belongs to the prohibition, not to the list it sits on. The five scopes and
their precedence are in `send-selection-and-suppression.md` step 2.

**The sender is the identity a message went out under**, meaning the From identity the header
names, not the business unit that paid for the send. A brand that sends under its own identity is
its own sender; brands sharing one identity are one sender whatever the platform's list structure
says. That is the operational test behind the two widest scopes, and it is the one
`consent-and-preferences` reads a withdrawal's reach from.

## Active core

The share of the addressable list that responded inside the engagement window. The denominator is
the reachable base in the channel as `metric-definitions` states it, the people you can get a
message to: a basis that still holds, an address that works, not suppressed. It is not
`list-building`'s active base, which is the wider tier the sending systems read from. It moves for reasons that have nothing to do with
the program, so the count goes next to the share every time, or a cleanup reads as a collapse.
Read the share as a trend across cycles rather than as a level: the level depends on how you set
the window, the trend does not. A program whose reach grows while its active core shrinks is buying volume with
list quality.

**Responded means responded to mail, not bought.** A mailbox provider reads opens and clicks and
nothing else, so a population picked on purchases is not the one it is measuring. The two overlap
and do not coincide, and where a warmup or a recovery has to pick an audience the provider will
approve of, the definition to use is `deliverability`'s.

## Channel revenue share

The channel's contribution to total revenue, always stated with the attribution method next to
it. Two systems attributing the same period will disagree, sometimes by a wide margin, and a
share quoted without its method compares to nothing, including its own value from last cycle if
the method changed in between.

## Revenue per recipient, the control metric

**What it measures.** Revenue attributed to a cycle's sends, divided by the people who received at
least one of them.

- **Numerator:** revenue attributed to the cycle's sends within a stated attribution window, under
  a stated method.
- **Denominator:** people, counted once each however many sends they received. Not delivered
  messages, which is `metric-definitions`' revenue per delivered message and asks about the message
  rather than the person; its revenue per recipient is this same object read on one send. Not
  openers, or the figure moves every time deliverability or open counting changes.
- **Window:** fixed, and shorter than one program cycle, so consecutive cycles do not overlap and
  double-count. A short window does not stop two sends inside one cycle from claiming the same
  order: only a conversion key and a credit rule do that, and both belong in the definition
  (`metric-definitions`).

**The denominator decides what the metric answers, so count it once on paper.** Take a cycle with
two sends of 10,000 recipients each, 8,000 distinct people behind them, and 20,000 in attributed
revenue. Per person it reads 2.50, per recipient-instance 1.00. Add a third send to the same 8,000
and take revenue to 24,000: per person it rises to 3.00, per recipient-instance it falls to 0.80.
The same program on the same data gives opposite readings, and only the first answers the question
this skill is accountable for. Fix the denominator before you read a trend, and do not change it
mid-series.

**How to read it.** Per cycle, next to total channel revenue, and against a holdout where you have
one, otherwise against the program's own history. Reach alone moves the figure: narrow the program
to your most responsive people and it rises while the channel earns less, which is a failure the
figure on its own reports as success.

**Against a holdout the metric changes shape.** A control group received nothing, so there is
nothing to attribute to it and a credited numerator is zero there by construction. Read revenue per
person assigned in each group over the same window, in any channel, with no credit rule, and take
the difference. That is a control drawn from the base and rotated, which is the global control of
`experiments-and-holdouts`, not the send-level holdout reserved for testing one send.

**Holdout membership survives the tier recalculation.** Somebody who receives nothing produces no
response, so the cycle's recalculation files them dormant and the dormant rhythm is anchors only.
By the time they rotate out, the program has changed what it does to them, which means the control
was treated after all and the tier mix no longer means what it did. Freeze the tier of anyone in a
control at the value it had on assignment, and compute the active core with them excluded.

**This library has no citable benchmark for this metric.** Say so when asked, then build a
self-baseline: take eight to twelve completed cycles, compute the median and the spread, and
treat movement outside that spread as signal and movement inside it as noise. Eight to twelve is a
starting point rather than a computed minimum, and a cycle whose attribution window has not closed
is not one of them. A baseline built this way belongs to the person who built it. It is not a market number and it does not travel to
anyone else's program.
