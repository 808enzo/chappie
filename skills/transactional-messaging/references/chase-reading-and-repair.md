---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Reading chases and repairing the register: does the set of messages do its job

The unit here is **the transaction, as the person lives it**. This file reads the control metric in
`SKILL.md`, finds where the register fails, and changes it. What a row contains is
`service-register-and-contract.md`; how a send gets there is `deadline-channel-and-failover.md`.

## Entry conditions

Support contacts carry a topic and can be tied to a transaction. The register and the send log exist.

## Exit conditions

A weekly reading of the chase share by transaction type and path. A gap list sorted by gap class. A repair
log. Row changes, each with a reading before and after.

## Steps

**1. Tie every contact to a transaction when it opens.** Tie it by the reference number in the contact,
which reaches support because the "where to ask" link in the message carries it
(`service-register-and-contract.md`, step 6), or by an identified person with exactly one transaction
open or inside its tail window: "it says delivered and I have nothing" comes after the final state, and
a rule that reads "open" alone cannot tie it. When a person has several such transactions and no
reference, the bot's first line or the agent's script asks which one before anything else; a tie set from
that answer, before any reply on the matter, counts as set at open. A person who leaves without answering
stays untied; count that contact on a line of its own, with the number of transactions the person had.
Set the tie when the contact opens, not from what an agent writes later: a tie made after the fact
depends on how the contact went. Count contacts in every channel where the company answers: chat and the
bot (an identified issue in `chat-and-bots`' terms, at the moment it opens), phone, replies to service
messages, social messages. A reply sent to a no-reply address is a chase, so receive it.

**2. Count a repeated request as a chase.** A second code or reset request for the same account within
the first one's validity; a second identical order within the confirmation's deadline; a second payment
attempt on an order already paid. Each is the person asking "did that work?" without writing a word. The
window for each kind of repeat is a parameter. Identical means the same items and quantities to the same
address by the same delivery method; a second order that differs in any of those is a second transaction.
An identical pair can still be a genuine double, and the person's own action settles it by the reading
ceiling: one of the pair canceled or refunded, and the pair was a repeated request, counted as a chase on
the first; both fulfilled and kept, and they were two transactions, each in the denominator, neither
chased.

**3. Place each chase on the transaction's timeline.** For every chase, look at the person-facing state at
that moment, the last message sent and its delivery state, the active promised time and whether it had
passed. Then give the gap a class:

- **(a) no row for this state:** a gap in the register;
- **(b) a row exists and nothing went out:** a send failure;
- **(c) it went out and arrived late or not at all:** the channel or the queue;
- **(d) it arrived before the chase and the person asked anyway.** Two causes with two repairs, told
  apart by the active promised time at the moment of the chase: passed, and the promise broke (repair 3
  in step 5); not passed, and the content did not answer (repair 5);
- **(e) the chase came before any message was due:** the deadline sits too late, or checkout set the
  wrong expectation;
- **(f) not about the transaction's state:** a mislabeled topic, which leaves the numerator. A contact
  that takes an action the message offered (cancel, change the address) through support instead of the
  link goes here too; read it beside the metric as a sign that the self-service route failed.

**4. Read a random sample of timelines every period, not only the chased ones.** Draw random transactions
across all paths and look at states, promised times, messages and deliveries side by side. The sample
catches silence read as success (people who gave up, support that is hard to reach) and messages that went
out wrong with nobody asking (another person's data, the wrong recipient, which goes to
`program-audit-and-ops` as a disclosure at once). Draw the sample path by path: the common path dominates
a sample drawn from the whole cohort, and such a sample can miss a rare exception.

**5. Repair in this order.**

1. Disclosure and wrong data, at once, by severity class.
2. Missing exception rows, and promised times with no timer.
3. Promised times the operation breaks.
4. Send failures and late sends.
5. Content that does not answer.
6. Progress rows that do not reduce chases, removed.

Adding a message is not the default repair: a new progress row spends attention on every transaction.

**6. Read a change on the same mix of paths, before and after, and do not withhold required rows to test
it.** Keep access, confirmation, the first message of an exception, and rows a law requires out of any
control group (`experiments-and-holdouts` excludes transactional messages from holdouts). An optional row,
one that repeats what was already delivered (a reminder before a pickup hold ends, after "ready for pickup"
arrived; an extra progress row), can be tested against its absence, randomized by transaction. Content and
timing variants of any row can be tested when every variant meets the contract; adding a promotional block
makes a change of class, not a variant. Read before and after on the same mix of paths (delivery method,
carrier) and outside the peak: a shift in the mix moves the number along with operations.

**7. Retire a row on chases, not on revenue.** A row retires when its state no longer exists, or when it
is an optional progress row whose removal left the chases on its path unchanged. Required rows do not
retire on data. This is the criterion `program-audit-and-ops` and `scenario-map` hand to this skill.

**8. Report broken promised times to operations.** Chases that follow a broken promised time are a defect
in the operation (the carrier, the warehouse). Report them as the chase share by carrier and by
fulfillment location. A message does not repair a promised time the operation does not keep.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Tail window after the final state | read the daily count of status contacts by days since the final state; the window ends where the count stops falling | parameter |
| Reading ceiling | the longest promised time you accept plus the tail window; a cohort is read on its creation date plus the ceiling | follows from the definition |
| Window of a repeated request | by kind of repeat: the code's validity; the confirmation's deadline for a duplicate order; for a second payment attempt, any time while the order shows paid | parameter |
| Size of the timeline sample | as many timelines per path as one person reads in one sitting; raise it when a gap class appears that the sample had not shown | parameter |

## Edge cases

- **The bot answers "where is my order" by itself.** Still a chase: count it at the person's first
  message, not at the handoff to an agent.
- **The tracking page.** A visit is self-service, not a chase. Read repeated visits to one transaction's
  page within hours beside the metric, as a silent chase.
- **A contact from a gift's recipient.** Tie it by the reference number, not by the person.
- **A chase about the carrier's leg.** It counts; attribute it to the carrier (step 8).
- **A B2B customer with an account manager.** Questions sent to the manager stay outside the support
  systems, and untied, unless the manager logs them. Give the manager a way to do that.
- **A complaint about the product, not the transaction's progress.** Gap class (f); it leaves the
  numerator.

## Failure modes

**The bot swallows the chase.** The bot answers the status question and closes the conversation, and
contacts get counted only when an agent takes them. Sign: the chase share falls after the bot launches,
while the number of conversations opened on status topics does not. The remedy is counting at the
person's first message.

**The number falls because asking got harder.** A no-reply sender, a hidden phone number, a contact form
behind sign-in. Sign: the timeline sample shows exceptions with no message and no chase, and the
questions move to public reviews and payment disputes. The remedy is step 4; a change to the contact
routes starts a new baseline.

**Repair by adding messages.** Every chase gets answered with a new progress row. Signs: messages per
transaction rise, the chase share on the exception path does not fall, spam reports on the service
identity rise. The remedy is the order in step 5.
