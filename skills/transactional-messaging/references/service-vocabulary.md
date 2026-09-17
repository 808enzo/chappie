---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Vocabulary of service messages

The three mechanics assume these terms. The first three, *transaction*, *row* and *send*, are the reason
arguments about "how many statuses to send" do not settle: one side counts messages, the other counts the
questions people ask about their order, and they are counting different things. Several words here are
shared with neighbors, and those are marked at the end.

## The units

**Transaction.** What a person set in motion and is waiting on: an order with all its shipments, a
booking, a payment, an account request. The unit of reading. Its type is one of those four, and the types
are read on separate lines. A payment is a transaction of its own only when it is not part of an order
(an invoice, a top-up, a subscription charge); the payment of an order belongs to the order.

**Service register.** The list of service messages, one row per message.

**Row.** One service message: kind, trigger, content contract, promised time it writes, deadline, channels,
class, whether a law requires it, owner, template version, test path. The unit of construction.

**Send.** One message to one person, on one attempt, in one channel. The unit of delivery.

## States

**Internal status.** A status in a system of record: picking, packed, awaiting supplier, at a sorting
facility.

**Person-facing state.** One of the few states of a transaction a person can tell apart: received,
confirmed or paid, handed to the carrier, out for delivery or ready for pickup, delivered or collected,
canceled, refunded, and the exceptions.

**Status map.** The versioned table that sends every internal status to one person-facing state or to "no
change".

**Final state.** The state after which nothing more is expected: delivered or collected, canceled,
refunded, or the request completed.

## Kinds

**Kind.** Access, confirmation, progress or exception. Not a class: a class is one of
`contact-orchestration`'s five, and it sets precedence and exemption from the cap. A kind is one of four
inside the service class, and it sets the deadline anchor, the channels and failover.

**Access.** A row without which the person cannot go on right now: a code, a reset link, a verification
link, a pickup code, a ticket, a download link.

**Confirmation.** A row that records what the person agreed to: an order, a booking, a payment, a
cancellation, a refund, a change.

**Progress.** A row for a person-facing state reached along the promised path.

**Exception.** A row for a transaction that departed from what was promised or needs the person to act.

**Required row.** A row a law obliges you to send, or one the person cannot get the service without: every
access row, the confirmation, the first message of an exception, and rows named in `SKILL.md`'s legal
section. It is not withheld for a test and does not retire on data.

**Optional row.** A row that repeats what was already delivered: a reminder, an extra progress row. It can
be tested against its absence.

## Time

**Promised time.** The time of the next state that a message states: a date, a window, a ready-by time,
or, in an exception that can give no revised time, the time of the next update. A date is a window of one
day. A promise in `email-copy`'s sense, a debt the message owes the reader, whose content is a time, the
way `chat-and-bots`' promise is a time for a human reply. Every promised time has a timer.

**Promise timer.** The trigger of an exception row: the next expected state has not arrived by the promised
time minus a lead time.

**Lead time.** How far ahead of a promised moment the person acts on it.

**Deadline.** The moment by which a row has to arrive: the earlier of the person's next event minus the
time they need to act, and the low tail of time from the state change to the first chase about it, taken
on the transactions that had no delivered message about the state when the chase came.

**Hop.** The stretch of a send's path between two timestamps: system of record, messaging layer, send
request, provider acceptance, delivery receipt.

## Delivery

**Failover.** Sending the same row through the next channel, on a confirmed failure or on a deadline
passing with no receipt. Not a *fallback*, which in this library always names substitute content:
`personalization`'s fallback ladder for an empty value, `email-design`'s fallback part of a message,
`email-copy`'s fallback wording.

**Idempotency key.** The transaction plus the person-facing state, plus the shipment where there is more
than one; for an exception row, plus the promised time the message corrects. A retry carrying the same
key does not send again.

**Current-state rule.** Before a send, the transaction's state is read again, and a state older than the
last one sent does not go out.

## Reading

**Chase.** A contact tied to a transaction when it opened, whose topic is the transaction's state,
whereabouts, confirmation or access, in any channel where the company answers; or a repeated request.

**Repeated request.** A second code or reset request within the first one's validity, a second identical
order within the confirmation's deadline, a second payment attempt on an order already paid.

**Tied contact.** A contact tied to a transaction when it opened, by reference number, by an identified
person with exactly one transaction open or inside its tail window, or by the person's answer to "which
one" before any reply on the matter. An **untied contact** has no such tie and is counted apart.

**Path.** *On promise* when every state arrived by the first promised time a message gave for it;
*exception* otherwise. Set from the promised time in the message and the actual time of the next state;
a window is kept when the state falls inside it, and a revised time, kept, does not move the transaction
back.

**Tail window.** How long after the final state a contact still counts as a chase. Not the *settle
window* of `chat-and-bots`, which counts returns after an issue is closed.

**Reading ceiling.** The longest promised time you accept plus the tail window. A transaction with no
final state by then is read as open.

**Timeline.** A transaction's states, promised times, messages and deliveries, side by side.

**Gap class.** Where a chase came from: no row, no send, late or missing delivery, content or a broken
promised time, a chase before anything was due, a mislabeled topic.

**Chase share.** The control metric: transactions in a cohort with at least one chase, over all
transactions in the cohort, by type and path.

## Words shared with neighbors

- **Service, mandatory notice:** message classes of `contact-orchestration`, in its sense.
- **Issue, topic, identified issue:** `chat-and-bots`, in its sense.
- **Displayable endpoint, fan-out rule, loss interval:** `push-notifications`.
- **Sending identity:** `deliverability`.
- **Service frame, block, template version and its release:** `email-design`.
- **Heartbeat, expected silence, missed obligation, disclosure:** `program-audit-and-ops`.
- **Quiet hours, cap:** `contact-orchestration`.
- **Fact, promise:** `email-copy`.
- **Requested message** (a handover state): `onsite-capture`.
