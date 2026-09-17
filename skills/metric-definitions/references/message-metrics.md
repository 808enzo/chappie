---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Message and channel metrics

Formulas and denominators for the metrics a messaging program is read by. Every entry names what
it measures, what sits underneath the line, and where the number is observed. No ranges appear
here: what counts as a good value for any of these depends on the category, the base and the
method, and this library states a number only with its source.

If two systems can report the same metric, the definition has to name which one is the system
of record. See `reconciling-across-systems.md`.

**Every per-send rate has a collection window.** Opens, clicks, unsubscribes and complaints keep
arriving for days after a send. Count the window from the send, write its length into the
definition, set it from your own arrival lags, and read the rate after it closes. A rate read
earlier is the share of events that have arrived so far, and it rises until the window ends.

## Sent and delivered

**Sent** is what left your platform. **Delivered** is what the receiving server accepted. A
deferred message, one the receiving side asked you to retry later, is neither delivered nor
refused until the retries run out, so read delivered and delivery rate once the retry queue for
the send has emptied; before then the pending messages sit on neither side, and `deliverability`
owns deferral. Almost every rate below uses delivered, not sent, and the difference between the
two is the first thing to check when a rate moves without a reason.

Delivered is not the same as seen, reached, or placed in the primary folder. Inbox placement is a
different measurement and belongs to `deliverability`.

## Bounces, hard and soft

A **hard bounce** is a permanent refusal about the address: it does not exist, or its domain
accepts no mail. A refusal because the receiving side blocked your mail is not a hard bounce, even
though it arrives as a refusal: the address works, suppressing it removes a reachable person, and
`deliverability` classes it separately. A **soft bounce** is a temporary refusal: mailbox full,
message too large, a transient server condition.

- **Numerator:** bounced messages of that type.
- **Denominator:** sent.

Keep the two separate. A rising hard bounce rate is a list problem. A rising soft bounce rate can
mean full mailboxes, oversized messages, or a receiving side slowing you down, and the last one is a
reputation signal that `deliverability` separates from the other two. Reported together they hide
each other.

## Delivery rate

- **Numerator:** delivered.
- **Denominator:** sent.

A drifting delivery rate reads as list decay. What to do about it belongs to `deliverability`;
what it is belongs here.

## Open rate

- **Numerator:** opens recorded for the send. State whether it is unique openers or all opens.
- **Denominator:** delivered.
- **Window:** opens keep arriving for days; fix the window or the number keeps changing after you
  quoted it.

**Read it as a direction, not a measurement.** Mail clients that prefetch images register opens no
human made, so the metric carries a machine-generated component that varies by audience and
changes when a mail client changes. Two consequences: do not compare your open rate to anyone
else's, and do not let a metric derived from opens carry a decision on its own.

## Click rate (CTR)

- **Numerator:** clicks. State whether unique clickers or all clicks, and whether any link counts
  or only the tracked call to action.
- **Denominator:** delivered.
- **Window:** the collection window, counted from the send.

## Click to open rate (CTOR)

- **Numerator:** unique clickers.
- **Denominator:** unique openers.
- **Window:** one collection window for both halves, counted from the send.

CTOR asks how well the message performed for the people who opened it, which makes it useful and
fragile at once: it inherits every distortion in open counting. Read it next to CTR, never
instead of it.

## Conversion rate

The metric with three legitimate denominators, which is why it causes more disagreement than any
other entry on this page:

- against **delivered**: how much the send produced, per message that arrived;
- against **openers**: how well the content converted the attention it got;
- against **clickers**: how well the destination converted the traffic the message sent.

All three are valid. None is interchangeable with another. A definition that does not say which
one is in force is not a definition, and a conversion rate quoted in a meeting without its
denominator should be treated as a rumor.

- **Numerator:** the target action, with its own qualifying condition, inside a stated attribution
  window.
- **Note:** the destination does part of the work. A conversion rate moves when the site, the
  offer or the fulfillment moves, none of which is the message.

## Unsubscribe rate

- **Numerator:** unsubscribes attributed to the send.
- **Denominator:** delivered.
- **Window:** the collection window, counted from the send.

Read it with complaints. Few unsubscribes next to many complaints means the unsubscribe path
is broken or hidden, so people take the faster route. That is a diagnosis available from these
two metrics together and from neither one alone.

## Spam complaint rate

- **Numerator:** complaints reported by the receiving side.
- **Denominator:** delivered.
- **Window:** the collection window, counted from the send and set from the lag of the complaint
  reports you actually receive.

Observed in the mailbox provider's postmaster tools rather than in your platform, which makes it
the one metric on this page whose system of record is outside your stack. Thresholds that mailbox
providers enforce are facts about those products and belong in `deliverability`.

## Revenue per recipient, per delivered message, per thousand, per reachable person

Related metrics that share a numerator and differ in the denominator:

- **Revenue per recipient:** revenue attributed to one send, divided by the people it was delivered
  to.
- **Revenue per recipient over a period or a program cycle:** revenue attributed to the period's
  sends, divided by the people who were delivered at least one of them, each counted once. It is
  neither the single send nor the message: add a send to the same people and it
  rises while revenue per delivered message falls. `email-program` reads its control metric this
  way.
- **Revenue per delivered message:** the same numerator over delivered messages. Use it when one
  person can receive several messages in the period and you are asking about the message rather
  than the person.
- **Revenue per thousand messages:** the same value scaled, for when the per-message figure is a
  fraction too small to read.
- **Revenue per reachable person:** the period's revenue over the reachable base in the channel at
  the start of the period. It keeps the people you stopped messaging in the denominator, which is
  why `contact-orchestration` reads revenue this way.

- **Numerator:** revenue attributed within a stated window under a stated method, net of returns
  if your definition says so, and say so.
- **Denominator:** as above, and it is the whole decision. Name which one you mean before you read
  a trend, and do not change it mid-series.

**Read any of them next to total revenue from the channel.** Alone, the direction is ambiguous:
every per-recipient and per-message form rises when you send only to your most responsive people
and falls when you extend reach to the rest of the base, and neither movement is good or bad by
itself. The pair is what carries meaning, which is why `email-program` reads its control metric
beside total channel revenue.

## Share of revenue from the channel

- **Numerator:** revenue attributed to the channel.
- **Denominator:** total revenue for the same period.

**Always read next to absolute revenue.** A share can rise because the channel earned more, or
because it took credit from another channel, or because total revenue fell. The three look
identical in the share alone.

## Reachable base

The people you can get a message to in the channel: a basis that still holds, an address that
works, not suppressed. `list-building` owns the term across channels, as the records inside its
active base that at least one channel reaches, and `contact-orchestration` counts it per channel
and in total. It is the denominator under most program-level rates, and it moves for reasons that
have nothing to do with the program, so publish it beside any rate computed on it.

Do not call it the active base. In `list-building` the active base is the wider tier the sending
systems read from, and on `customer-metrics.md` an active customer is a buyer inside a window.

Engagement tiers within the reachable base, meaning who counts as active, occasional, dormant,
suppressed or not yet classified for sending purposes, are defined by `email-program`, because a
tier is a property of a channel program rather than of a metric. Its tiers run on recency of
response alone, with a waiting state for anyone whose history is shorter than one engagement
window; lapse sits on the commercial axis and belongs to `lapse-and-winback`.
