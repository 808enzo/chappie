---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Deadline, channel and failover: getting a service message there in time

The unit here is **the send**: one message to one person, on one attempt, in one channel. This file
takes a row of the register (`service-register-and-contract.md`) and gets it to the person before the
moment it stops being worth anything. Whether the rows are the right ones is `chase-reading-and-repair.md`.

## Entry conditions

Register rows with a kind and a promised time. At least one channel for each person, if only the address
given at checkout.

## Exit conditions

For every row: the deadline anchor and the deadline, the order of channels, the failover condition, the
idempotency key and the collapse key, the quiet hours rule. Timestamps on every hop. A queue and a sending
identity of their own. An expected ratio of messages to events.

## Steps

**1. Set each row's deadline from the next moment in the person's world.** The deadline is the earlier of
two: (a) the person's next event (the courier's arrival, the start of a pickup hold, a code's expiry) minus
the time they need to act on the message; (b) the low tail of the time from the state change to the first
chase about it, in your own data. Take (b) from the transactions that had no delivered message about the
state at the moment of the chase (gap classes b, c and e in `chase-reading-and-repair.md`, step 3): that
is how long people wait before asking when nobody tells them. The chases that follow a delivered message
measure its content, and a row that works removes the early chases from the whole set, so a tail taken
from all chases drifts later as the row improves and loosens the deadline that made it work. When the
unnotified population is empty in a period, keep the last value; do not recompute on the notified.
Access: while the person is still on the screen, and well inside the code's validity, which is your own
parameter. Confirmation: before the first "did my order go through" contacts and duplicate orders.
Progress: before the event the person is getting ready for. Exception: before the promised moment (the
promise timer in `service-register-and-contract.md`, step 5).

**2. Timestamp every hop.** The event occurs in the system of record; it reaches the messaging layer; the
messaging layer requests a send; the channel's provider accepts it; a delivery receipt comes back, where
the channel issues one. Read latency hop by hop and at the tail, not on the average: the median send can
be fast while the tail misses the deadline. A batch sync sets a floor under every latency behind it: with
a sync every fifteen minutes, an interval picked here only to illustrate, fifteen minutes is the best case
for every row that waits on it.

**3. Give service sends a queue of their own.** A separate queue, or a priority of their own, on the
sending platform, apart from campaigns, and a sending identity of their own (`deliverability`). A rate
limit at the provider that campaigns share is a shared queue under another name. The check: during your
largest campaign send, the tail latency of service rows stays inside their deadlines.

**4. Choose channels by kind.**

- **Access** goes where the screen told the person it would go, and nowhere else.
- **Confirmation** goes by email, the durable record the person keeps (in the EU and the UK, the durable
  medium in `SKILL.md`), with the order page as its twin.
- **Progress** goes to the channel that shows on a device when the event matters: a displayable push
  endpoint under `push-notifications`' fan-out rule, otherwise failover (step 5). An email copy is
  optional.
- **Exception** goes by the fastest channel available, plus a durable copy by email, because it carries
  the options and what happens without an answer.

A person's own choice of channel for service messages (the preference center, `consent-and-preferences`)
changes the default channel. It does not switch off a required row.

**5. Fail over on a fact, never on an open.** Send the row through the next channel when the current one
confirms failure (a hard bounce, an invalid number, no displayable endpoint, a provider rejection), or
when the deadline minus the next channel's own tail latency passes with no delivery receipt, in a channel
that issues receipts. Do not fail over on "not opened": machines register some opens, and a person may
read a push without tapping it. For an exception that asks for an action by a deadline, send the second
message when the action has not happened by a fixed point before the deadline; a missing action is a fact
too. The message sent on failover carries the same reference and says it repeats the earlier one. An
access row does not fail over on its own: it goes where the screen said, and at its deadline the screen
offers the other channel and the person chooses (the edge case below). The order of channels in a
marketing cascade, and the waits between them, belong to `triggered-messages`; the wait before a service
row fails over comes from its deadline.

**6. Send each state once, and only while it is current.** The idempotency key is the transaction plus
the person-facing state, plus the shipment where there is more than one. For an exception row the key
also carries the promised time the message corrects: a second delay on the same transaction is a new
message, and a key of transaction plus state would swallow it. A retry with the same key does not send
twice. Before sending, read the transaction's current state again, and hold back a progress state older
than the last one sent: events arrive out of order ("delivered" before "out for delivery"). Drop an
exception whose promised state arrived in the meantime, for the same reason. The confirmation is not a
progress state, and a progress state never holds it back: it is the record, and it goes even when the
order has shipped since, because the person keeps it and a regime may require it. After an outage or a
backlog, send one message per transaction, about its current state, with its promised time checked again,
plus the confirmation for every transaction that never got one; do not replay the queue. Collapse
repeated updates of the same thing on push under a collapse key (`push-notifications`).

**7. Apply quiet hours by kind.** Access, and exceptions whose deadline falls inside the night, go at
once. Progress and confirmation that the person cannot act on before morning wait, in channels that make a
sound on a device, until quiet hours end in the recipient's local time (`contact-orchestration`); when the
next moment comes before quiet hours end, send the row at once. Service rows sit outside the cap, and the
timing chart still counts them (`contact-orchestration`, the edge case on a transactional spike).

**8. Define the expected ratio of messages to events for each row.** Messages sent for a row should match
the transactions that entered its state, minus the exclusions you wrote down (no channel, a marketplace
order). A ratio that falls while the events hold means a broken row; events that stop mean a fault in the
system of record or the integration. Watching the ratio, and the incident route, belong to
`program-audit-and-ops` (the heartbeat and the expected silence); this file defines what counts as
expected.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Deadline of a row | the earlier of: the person's next event minus the time they need to act; the low tail of time to the first chase about that state | parameter |
| Low tail of time to the first chase | start with the 10th percentile for each state over a period, on the transactions with no delivered message about the state at the moment of the chase; this holds where a state collects such chases in every period, and where it does not, pool the states of one kind, and where the period has none, keep the last value; revise when chases on the on-promise path arrive before the deadline | starting heuristic |
| Wait before failover | the deadline minus the tail latency of the next channel | follows from the definition |
| Floor of latency behind a batch sync | the sync interval; the fifteen minutes in step 2 are an illustration | follows from the definition |
| Validity of an access code | yours | parameter |
| Quiet hours | `contact-orchestration`, in the recipient's local time | neighbor |
| Push expiry and collapse key | `push-notifications` | neighbor, platform rule |

## Edge cases

- **The code is late and the person is on the screen.** At the deadline the screen offers another
  channel, not a resend through the same one: a resend duplicates, and where issuing a new code voids the
  earlier one, the code the person is about to type stops working.
- **A reassigned phone number.** A code sent to somebody else's number is a disclosure
  (`program-audit-and-ops`' severity classes). Before sending a code to a number nobody has confirmed for a
  long time, confirm it through another channel.
- **A device with no connection.** A push service stores little for an offline device
  (`push-notifications` carries the platform rule), and a promotional push to the same endpoint can
  displace an awaited service push. While a service push may still be undelivered, send no promotion to
  that endpoint.
- **A corporate mail filter holds the message.** No receipt comes back, and the delay sits outside your
  queue. For an exception that asks for an action, send the second channel on the missing action
  (step 5).
- **The person left only a checkout email.** Failover has nowhere to go; the order page is the
  substitute, and the confirmation screen says that status shows there.
- **A warmup of the service identity.** Keep the service stream running (`deliverability`, its edge case
  on service mail during a warmup).
- **Two transactions in a row.** Each gets its own messages. Different transactions do not merge; repeated
  updates of one transaction's state collapse.

## Failure modes

**Service waits behind a campaign.** One queue, or one rate limit at the provider. Signs: the tail latency
of service rows rises on campaign days; "did my order go through" chases rise with large sends. The remedy
is step 3.

**The queue replays after an outage.** Several states per transaction within minutes, states out of
order, "handed to the carrier" arriving after "delivered". Signs: a spike in messages per transaction per
hour, and state order violations in the send log. The remedy is step 6.

**Failover on opens.** It fails in two opposite directions, and the second channel's volume tells them
apart. Where opens go unregistered (images turned off), the second channel reaches people who already read
the first message: duplicates and cost rise. Where machines register opens, the second channel stays
silent for people who never saw the first: chases rise on transactions whose message counts as opened. The
remedy is step 5.
