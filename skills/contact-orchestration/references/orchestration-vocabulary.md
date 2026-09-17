---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Vocabulary of contact orchestration

The three mechanics assume these terms. Three of them, *touch*, *load* and *deduplication*, mean
different things to different people in one room, and deduplication names two entirely separate
jobs. Settle them before the discussion, not during it.

## The unit

**Touch (message).** One delivered message, to one person, in one channel. The unit of counting is
delivery rather than dispatch: what never arrived is not load. In push, a message that the fan-out
rule of `push-notifications` delivers to several of one person's endpoints is one touch. Inside a
product, delivery is the display: `in-product-messaging` writes a display of a campaign, a flow, a
perishable message or an ask to a known person as a touch, a blocking one each time it shows and a
passive one once per person within the message's window, and counts it toward the total and toward
the channel "in-product".

**Load.** The number of touches one person received over a named period. Always carries two
qualifiers: over what period, and across which channels. "A load of four" without them is not a
measurement.

**Messaged person.** Someone who received at least one message during the period. The load
distribution is built on messaged people, with the reachable people at zero counted beside it. It is
not the denominator of revenue in this skill: revenue per messaged person rises when you stop
messaging the least responsive, so revenue is read per reachable person. A metric with sends in the
denominator answers a different question, and it improves whenever you send more.

**Addressed person.** Someone the program tried to contact at least once during the period,
counted on the attempt rather than on the arrival. An attempt is a send handed to a channel; a
message the policy held is not one. Every messaged person is an addressed person and not the
reverse. This is the denominator of reachability loss, because a hard bounce is a loss event for
somebody who received nothing, and a loss from someone not addressed in that channel in the period
is counted on its own line beside the rate.

**Reachable base.** The people you have both the right and the technical means to message in at
least one channel. Counted per channel and in total: one person can be reachable on push and lost
on email, and the two counts move separately. It is capital, and every send spends it. Taken at the
start of the period, it is the denominator of revenue per reachable person.

**Reachability loss.** The event after which a person stops being reachable in a channel:
unsubscribe, spam complaint, notifications turned off, a block, a hard bounce. It is scoped to the
channel and counted once per person per channel per period, however many reasons arrived. In push
it is the loss of the person's last displayable endpoint; a switch-off has no exact date, only an
interval, and it counts in the period in which you discovered it (`push-notifications`). An
unsubscribe is also an instruction in `consent-and-preferences`' sense; the two skills count the same
event for different reasons, one as a loss of reach and one as the person's word.
**Total unreachability** is the separate state of having no reachable channel left, and that is
the only one that means the person is gone. A refusal that arrived because a mailbox provider
blocked the whole flow is not a loss event at all: it is a property of the sending pair rather than
of the person, and it is `deliverability`'s to clear. A text refused as unregistered or filtered
traffic is the same case in `messaging-channels`.

## The rule

**Cap.** The ceiling on load for a period, in total and by channel. A parameter, computed from
your own data. It has no industry norm by construction, because it is a property of your base,
your category and your purchase cycle. Measured in deliveries and enforced against reservations:
if it counted only what a receipt confirmed, two senders could both pass the last message under
the ceiling. A mandatory notice counts toward the cap and is never held by it.

**Message class.** Service, mandatory notice, perishable and personal, automated flow, campaign.
The class sets precedence and decides exemption from the cap.

**Precedence.** The order in which messages yield to each other in a collision. Set by
perishability and by how specifically the message is addressed, not by importance to the business.
It is not build order: which mechanic gets built before which is priority in the sense
`crm-program-design` and `scenario-map` use, and it is decided long before any message exists.
It is also not **offer precedence**, which decides which of several offers applies to one order at
checkout. That one belongs to `offer-design`, and its vocabulary states the same split from the
other side. The two run on different units and at different moments, and they fail differently: a
message loses precedence and is suppressed or deferred, an offer loses it and simply does not
apply. Ask which one somebody means before agreeing to anything about "priority".

**Exemption.** Freedom from the cap, granted to what the person is waiting for as a consequence of
their own action. It ends the moment a promotional block is added to the message. A mandatory notice
is never held and still not exempt: the person is not waiting for it.

**Quiet hours.** An interval in the recipient's local time when messages are not delivered, applied
by class: a service message the person can act on now and a mandatory notice whose deadline falls
inside the night go at once.

## The decision

**Held.** Stopped by the policy: suppressed or deferred. Held is the policy's decision, not a
delivery state; a claim written before the send is *reserved*.

**Suppression against deferral.** A suppressed message never goes. A deferred one goes later and
consumes the cap of the period it lands in. Two different decisions with two different
consequences, and treating them as one is expensive: perishable messages that get deferred arrive
dead, and deferred queues turn into a volley.

**Pitch deduplication.** The same argument does not repeat in a second channel once it has reached
the person in the first. A pitch claim enforces it. Delivery history alone cannot, because a message
in flight appears in no history. Not to be confused with **profile deduplication**, which
merges several records of one person into one. That one belongs to `list-building`, and its
vocabulary states the same split from the other side. The two share a name and nothing else, so
ask which job somebody means before you start it.

**Contact log.** One row per person per message, with the channel, the class, the stream and the
state, fed by every system that sends a message or shows one to a known person. The cap, pitch
deduplication and the control metric read it; neighbors write their events into it.

**Reservation.** A row in the contact log, written before the send, that counts the message against
the cap while it is in flight and is released by a confirmed failure.

**Pitch claim.** A record on the person, the pitch and the window, written before anything reaches a
channel, which a second candidate for the same pitch finds and honors. It is what makes pitch
deduplication hold across two systems, and it holds only where both write to the same store. Its key
comes from the triggering event, so reprocessing that event finds its own claim.

**Delivery state.** One of four, and only the third proves the pitch arrived: reserved, in flight,
delivered, unknown. Unknown means the receipt window closed empty, and it is not a synonym for "not
delivered": decide per message what it counts as, and write the decision down. A message queued
inside a product is in flight until it is shown, and expiring unseen there is a confirmed failure
that releases the claim (`in-product-messaging`).

**Held share.** For one stream, the share of its sends that the policy stopped. A stream whose
majority is held is either redundant or misplaced in the precedence table.

## Neighboring constructions

**Cascade.** A sequence of channels inside one occasion, escalating when there is no response.
How a cascade is built inside a flow belongs to `triggered-messages`. Here it counts only as load
and as a source of a repeated pitch.

**Engagement tier.** The grouping of a base by how recently people respond, and by recency alone:
frequency of response is `rfm-segments`' axis. A tier belongs to a channel: email's is
`email-program`'s, and someone dormant in email can be active on push. The email cap uses email's
tier; the total cap uses a tier on the person computed by the same rule from response in any
channel, because one cap for every tier hits dormant people hardest at the point where they are
still recoverable.
