---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# The service register and the message contract: what the program owes a person, and what each message says

The unit here is **the row of the service register**: one person-facing state, or one promised time
about to be missed. This file settles which states and which promised times produce a message, what the
message contains, and what else it may carry. How fast and through which channel it arrives is
`deadline-channel-and-failover.md`; how to tell whether the register does its job is
`chase-reading-and-repair.md`.

## Entry conditions

The systems of record (orders, payments, bookings, accounts) expose states with timestamps. Some
messages already go out, and more than one system may be sending them. With no timestamped states the
mechanic has nothing to trigger on; that is an input for `martech-stack`.

## Exit conditions

A register with one row per message: kind, trigger (a state change or a promise timer), content
contract, the promised time the row writes, the deadline anchor, the class in `contact-orchestration`'s
terms, whether a law requires the row and under which regime, owner, template version, test path. A
status map from every internal status to a person-facing state. A timer for every promised time a
message states.

## Steps

**1. Inventory what already goes out, from every system that sends.** The storefront, the order
management system, the payment provider, the carrier, the booking engine and the app each send
notifications of their own, and marketing does not know about some of them. Collect real samples by
running test transactions down every path: each payment method, each delivery method, a cancellation, a
return. Two systems sending the same state is a duplicate. A message in the brand's name from somebody
else's domain is a question for `deliverability`.

**2. Map internal statuses to person-facing states.** A system of record holds more statuses than a
person can tell apart. Person-facing states are few: received, confirmed or paid, handed to the carrier,
out for delivery or ready for pickup, delivered or collected, canceled, refunded, and the exceptions.
Map every internal status to exactly one person-facing state or to "no change", and version the map.
Internal steps (picking, packing, arrival at a sorting facility) get no message: the person has nothing
to do about them, and each extra message takes attention away from the exception the set exists for.
Send internal steps only as an account setting, never by default: for a B2B buyer, or on a large order,
where the person reports progress inside their own organization.

**3. Ask the chases where the gaps are.** Take the support topic list in the person's words ("where is my
order", "did my payment go through", "the code never came"), which `chat-and-bots` keeps, for a recent
period, and tie each contact to the transaction's state at the moment the person asked. The states people
ask in are candidates for a row, or for a better one. `chase-reading-and-repair.md` runs this step on a
schedule.

**4. Give every row a kind.**

- **Access:** without it the person cannot go on right now. A sign-in code, a password reset link, an
  email verification link, a pickup code, a ticket, a download link.
- **Confirmation:** the company records what the person agreed to. An order, a booking, a payment, a
  cancellation, a refund, a changed address or plan. A durable record.
- **Progress:** a person-facing state changed along the promised path. Handed to the carrier, out for
  delivery or ready for pickup, delivered.
- **Exception:** the transaction departed from what was promised, or needs the person to act. A delay, a
  partial shipment, an item out of stock, a substitute that needs the person's approval, a failed payment,
  a failed delivery attempt, a pickup hold about to end, an address problem, a sign-in from a new device.

The kind decides the deadline anchor, the channels, failover, whether repeated updates collapse, and the
severity class when the row fails. In `contact-orchestration`'s classes all four kinds are service. Where
a law requires the row (the confirmation in the EU and the UK, the delay notice in the US, both in
`SKILL.md`), write that into the row: its failure is a missed obligation in `program-audit-and-ops`'s
severity classes.

Subscriptions and contracts bring rows of their own, and their deadlines come from the obligation, not
from a next event.

- **Required by law or by a card network, from `subscription-retention`.** The reminder before the
  first charge after a trial or a promotional period ends, or after the agreement changed: Visa, at least
  7 days before; California, 3 to 21 days before the end of a trial or a promotional price that applied
  for more than 31 days. The notice before the renewal of a term of one year or longer: California, 15 to
  45 days before. The notice of a price change: California, 7 to 30 days before it takes effect. The
  annual reminder under an annual agreement: California.
- **Required by law, from `b2b-retention`.** The notice New York's General Obligations Law § 5-903
  requires before an automatic renewal: 15 to 30 days before the time for serving notice of non-renewal,
  served personally or by certified mail. Its channel is outside email and outside the program, and the
  row records the date and the method of service.
- **Invoice rows, from `b2b-retention`.** A request to confirm that the invoice was received, before the
  payment date; a reminder after the payment date; the notice of suspension, in the form the contract
  sets.
- **Exit rows, from `b2b-retention`.** The confirmation of a notice of non-renewal with its effective
  date; the window for exporting data; the date of deletion; the end of access.

The register holds the rows, not the rules. The quotations, the addresses, the date each page was opened
(2026-09-15) and the people each rule does not bind are in the `SKILL.md` of `subscription-retention` and
of `b2b-retention`.

**5. Trigger a row one of two ways: by a state change, or by a promise timer.** Access, confirmation and
progress fire on a state change. Some exceptions arrive as events too: a failed payment, a failed
delivery attempt. A delay does not. It is the absence of the next state by a promised time, and an
absence emits no event; a carrier's "delayed" event, where one exists, gets written when the carrier
learns of the delay, which can be after the promised moment. So **every promised time a message states
registers a timer**: when the next expected state has not arrived by the promised time minus a lead time,
the exception row fires, with a new promised time or a plain statement that you cannot give one yet. The
lead time is a parameter: how far ahead of the promised moment the person acts on it, arranging to be
home or planning a pickup. With no data on it, take the start of the promised window as the moment the
person acts. A promised time can be a window rather than a date, and a date is a window of one day. For a
window, the timer watches the state that has to precede it (handed to the carrier, for a delivery window)
and fires at the earlier of two moments: the window's start minus the lead time, and the window's end
minus the time the remaining states take in your own data. Firing at the window's end is too late: by
then the person has waited through it. An exception that gives no revised time still gives a time: when
the next update comes. That time is a promised time like any other and registers its own timer;
without it, "we cannot give a date yet" leaves the transaction with nothing watching it, which is the
silence the timers exist to end. In the US the delay notice has a legal outer limit (`SKILL.md`).

**6. Write the content contract.** Every service message answers, in this order:

1. what happened: the event in the person's words;
2. which transaction: the reference number, the date, and what is affected (the items or the amount,
   with a partial one called partial);
3. what happens next and when: the next state and its promised time;
4. what the person has to do and by when, if anything: collect by, pay by, confirm;
5. how to act: a link that opens the transaction with the person still signed in, to track, change or
   cancel, self-service first;
6. where to ask, with the reference carried into the contact, so that support can tie the chase to the
   transaction.

On top of that, by kind. Access: what it unlocks, when it expires, a route for "this was not me", and no
other links. Confirmation: the full record (items, prices, charges, delivery terms, cancellation and
return terms), and in the EU and the UK the information the law requires unless you already gave it on a
durable medium. Progress: the carrier's tracking, and who resolves problems with the carrier. Exception:
what went wrong, what you are doing about it, the new promised time or, with none yet, when the next
update comes, the person's options (wait, change, cancel with a refund), and what happens if they do
nothing. The subject or title names the event and the reference number (`email-copy`). Every claim has to
be true on the destination page: the tracking page shows the same state as the message (`email-copy`'s
rule on facts).

**7. Treat every date in a message as a promised time the program keeps or corrects.** Write dates the
operation keeps: a range from the carrier's estimate, not the fastest case. Each promised time registers
its timer (step 5), and a date no timer watches does not go into a message. Send a changed promised time
as an exception message, never as a quiet edit of the tracking page.

**8. Decide what else a message may carry at the template version, by class.** By default, nothing that
promotes. Help with what was bought (how to use it, care, assembly, how a return works) belongs to the
transaction. A promotional block changes the class, and each regime in `SKILL.md` draws that line in its
own terms: the subject line and the start of the body in the US, significant promotional material in the
UK, the word "solely" in Canada, and a mailbox provider asking senders to keep promotions out of receipts.
The working rule: a service frame reserves no place for promotion (`email-design`), and a cross-sell goes
as a message of its own, a flow in `triggered-messages` or `repeat-purchase` on the marketing identity, on
a lawful basis and inside the cap, after the service message it wanted to ride on. If the business decides
to carry promotion inside a service message anyway, that is a new row with a changed class, made in the
register rather than in the content. Take it through the regime question with whoever owns
`consent-and-preferences` questions where you work, and move it off the service identity
(`deliverability`).

**Where the class of a send gets checked: two moments.** At the release of a template version, the
version records the class of every block, and a service row may reference only a version whose blocks are
all service. At the send, the sending layer reads the class of the row and the class of the version; for
a service row pointed at a version that is not all service, it sends the newest released service version
instead and raises an alert to the row's owner. Do not let the class check block a required message: a
blocked confirmation is a missed obligation incurred to protect an exemption, and sending a service
version protects both.

The version it falls back to has to carry the current record, and you settle that before the fallback
is ever needed. The content the record consists of (items, prices, charges, delivery terms, cancellation
and return terms, the information a regime requires) comes into the message by substitution from the
system of record and from the current terms, never typed into a version: then every released
service version renders today's record, and an older version differs in wording and layout only. Where
a version does carry typed-in required content, its release records the date of that content, and the
version leaves the fallback set the day the content changes (`email-design` keeps the version registry).
The fallback picks the newest released service version still in the set. With none, the sending layer
holds the send inside the row's deadline and alerts the owner with that deadline; at the deadline it
sends the newest released service version anyway and sends a corrected record, same reference, marked as
replacing the earlier one, once a current version is released. A wrong record is corrected by a second
send; a missing one is a chase and a missed obligation both.

**9. Give every row an owner, a version and a test path.** The owner answers for the row. For a required
row that is whoever answers for the obligation (`program-audit-and-ops`), who need not sit in marketing.
Before a release, and after every release of any system on the path, run a test transaction down every
path, exceptions included: a delay, a partial shipment, a failed payment, a failed delivery, a
cancellation.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Lead time of a promise timer | how far ahead of the promised moment the person acts on it; with no data, the person is taken to act at the start of the promised window | parameter |
| Time the remaining states take, for a promised window | your own distribution from the state that precedes the window to the state it promises, by carrier and delivery method | parameter |
| Time of the next update, in an exception with no revised time | yours; it is a promised time and gets a timer | parameter |
| Internal statuses for a B2B buyer or a large order | an account setting, on the buyer's request | parameter |
| Reminder before a pickup hold ends | the hold is yours; the reminder's timing from your own distribution of time from arrival to collection | parameter |
| Payment window for a placed order, and the number of reminders | the window is yours; one message when the window is shorter than the time people take to pay in your own data, otherwise two, one at the start and one before the end | parameter |
| US: ship within the stated time, or within 30 days with none stated (50 days with a credit application); offer the delay option within a reasonable time and no later than that time; a renewed notice before the revised date | statute, 16 CFR 435.2, and the FTC's business guide, opened 2026-09-13 | legal |
| EU: confirmation on a durable medium within a reasonable time, at the latest at delivery of the goods or before the service begins | Directive 2011/83/EU, Article 8(7), opened 2026-09-13 | legal |
| UK: the same; treated as provided once sent or made available | Consumer Contracts Regulations 2013, regulation 16, opened 2026-09-13 | legal |

The first six are yours. The last three are dictated from outside, and each carries its source and the
people it does not bind in `SKILL.md`.

## Edge cases

- **Guest checkout.** The address given at checkout belongs to this transaction: service messages go
  there, and it does not become a marketing address (the *requested message* handover state in
  `onsite-capture`). With a typo, the confirmation bounces; the confirmation screen and the order page
  show that and let the person correct the address. The email is the durable copy, not the only one.
- **A gift: the recipient is not the buyer.** Progress and access (the pickup code) go to the recipient
  when their contact is given; the confirmation and exceptions go to the buyer; the recipient sees no
  prices. For a surprise, ask at checkout whether to write to the recipient before delivery.
- **A partial shipment.** A progress row for each shipment, with an order-level line such as "two of
  three shipments"; the confirmation says partial; the transaction closes when the last shipment arrives.
- **A preorder or a long wait.** The promised time is far away: a timer, a message when the promised time
  changes, and one before the promised window starts. No "still on its way" message with no news in it.
- **An order placed through a marketplace.** The marketplace holds the contact and sends the service
  messages. Do not send your own unless its terms allow it. Chases go to the marketplace, and these orders
  stay out of your cohort.
- **B2B: the buyer, the approver and the receiver are different people.** Rows by role; internal statuses
  by account setting (step 2).
- **Pickup.** "Ready for pickup" carries the end of the hold. Anchor the reminder to the end of the hold,
  not to days since arrival, and make the last one before the hold ends say what happens after it: back
  to stock, a refund.
- **An order placed and not paid.** Service, since it helps complete a transaction the person agreed to:
  the payment link and the time left, nothing else. A cart never submitted as an order belongs to
  `triggered-messages`.
- **Cancellation and refund.** The cancellation confirmation states the amount, the method and when the
  money lands. "Refunded" is a state of its own, with a promised time for the money to arrive. The money
  landing is a state your systems never see, so the timer cannot watch it: anchor the promised time to
  the last state you can observe, the payment provider's confirmation of the refund, plus the lag the
  provider states for banks, and let the timer watch the provider's confirmation. The message names both:
  when the refund is issued and how long a bank may take after that.
- **The first run of the timers.** On the day the timers switch on, every open transaction whose
  promised time has already passed meets its condition at once. Those go to a one-time list for
  operations, with the message they need written by hand, not to the exception row: a burst of delay
  notices for weeks-old orders is an incident. The timers take the transactions whose promised time is
  still ahead.
- **Account security.** A change of address or password sends a message to the previous address too:
  whoever takes over an account changes the address first. The "this was not me" route does not require
  the credentials that may be compromised.
- **A notice the law requires with no action by the person** (a recall, a change of terms). That is a
  mandatory notice in `contact-orchestration`'s classes. The register can hold its row; the deadline
  comes from the obligation, not from a next event. The notices subscriptions and contracts require are
  rows of this kind, listed in step 4.

## Failure modes

**Every internal status goes out.** Signs: messages per transaction grow with the status map; spam
reports on the service identity and push switch-offs after service sends rise; the chase share on the
exception path does not fall. People stop reading service messages, and the exception drowns. The next
mode differs in one sign: here the message count is high, there the chases sit on transactions whose
promised time passed. The remedy is step 2.

**Exceptions built on events.** Signs: chases concentrate on transactions whose promised time passed with
no message in the window before it; delay notices arrive after the promised moment. The remedy is
step 5.

**An internal status with no line in the map.** Operations add a status ("awaiting supplier").
Transactions in it send nothing and the timer reads the last mapped state, or a default sends a generic
message. Signs: a status in the system with transactions in it and no line in the map; chases on those
transactions. The remedy: give the map an owner, and let a status with no line read as "no change", with
the timer still running and an alert to the owner.

**A promised time the operation does not keep.** Sign: chases cluster right after the promised moment on
transactions the system of record shows as on time, because the date in the message was earlier than the
operation's own. The remedy is step 7, and the report to operations in `chase-reading-and-repair.md`,
step 8.
