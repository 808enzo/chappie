---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Vocabulary for messaging-channels

The terms all three mechanics assume. The last section lists the words this skill shares with its
neighbors, several of them under other meanings.

## The units

**Origin.** A registered number or name a message leaves from: a ten-digit number under its
registered campaign, a short code, a toll-free number, an alphanumeric sender ID, a WhatsApp business
phone number inside its portfolio, an RCS agent. The unit of the standing mechanic. Carriers call it a
sender or a sender ID; the messaging platform calls it a business phone number. Standing, limits and
pauses live on it, and the gatekeeper's opinion is about it, not about the company.

**Send.** One message to one phone number from one origin, in one class. The unit of the send
mechanic. It has a category, a regime, a form, a price and a status.

**Inbound.** A message that arrives on an origin: a keyword, a tapped button, free text. The unit of
the keyword mechanic.

## The gatekeeper and standing

**Gatekeeper.** The carrier or the messaging platform between the origin and the phone. It prices
every message, decides whether to accept it, and scores the origin on what people do with what it
sent.

**Standing.** The gatekeeper's current judgment of an origin: its messaging limit, the quality
rating of its templates, the pauses in force, the errors it returns. Read daily in the standing
register. Not the person's basis for receiving texts, which is a record in `consent-and-preferences`.

**Messaging limit.** On WhatsApp, the number of unique recipients a portfolio may message outside a
reply window in a moving 24 hour period: 250 for a new portfolio, then 2,000, 10,000, 100,000,
unlimited. It rises on delivered volume with high-quality templates, and every number in the portfolio
spends the same limit.

**Quality rating.** The platform's rating of a template, from usage, customer feedback and
engagement: GREEN, YELLOW, RED, and UNKNOWN on a template that has no signals yet.

**Pause.** The platform's suspension of a template at the lowest quality rating: 3 hours the first
time, 6 hours the second, disabled the third. Attempts to send a paused template are refused and not
charged.

**Per-user marketing limit.** The platform's cap on marketing template messages one person receives
from all businesses in a period, set from that person's recent read rate and inbox. A refusal carries
code 131049, and the send waits at least 24 hours.

**Registered campaign.** In the United States, the use case registered with the carriers for a
ten-digit origin under A2P 10DLC: its purpose, sample messages, and the opt-in, opt-out and help
texts. One registered campaign per class of message; the opt-in applies to the campaign and the sender
it was obtained for.

**Portfolio.** The business portfolio on the messaging platform that holds the numbers. The messaging
limit belongs to it, and every number in it spends that limit; each template carries its own quality
rating and pauses.

**Snowshoeing.** Spreading the same traffic across many origins to dilute the signals about it. The
carriers' principles tell senders not to use it; a split by class is one origin per class, not many origins per
class.

**Deactivation file.** The carriers' list of numbers that left service. Processed daily, it removes a
number from the record before somebody else is assigned it.

**Ramp.** The release of a new origin's sends by tiers of audience, each tier released by the
previous tier's signals rather than by the calendar.

## The send

**Class.** The neighbors' word for what a message is: a service line, a touch under the cap, a step
of a cascade, an authentication code. Given before the send reaches this skill.

**Category.** The gatekeeper's word for a template: marketing, utility or authentication. A
free-form reply inside a window has none. Declared on the template, approved, priced, and revised by the
platform when the content says otherwise. Mixed content is marketing.

**Template.** A message format the platform has approved, in a category, with its variables, buttons
and language fixed; an edit starts a new review. The only form a message may take outside a reply
window.

**Reply window.** The period after the person's last message in which the business may write freely;
24 hours on WhatsApp, which calls it the customer service window. A tapped button opens one. Not the
settle window of `chat-and-bots`, which is how long that skill waits before counting an issue settled.

**Free entry point.** The pricing page's term for a conversation that begins through one of the
platform's qualifying entry points. If you answer inside the reply window, a 72 hour window opens in
which every message is free. It does not extend the reply window: after 24 hours without a message
from the person, only templates go out. The page lists which entry points qualify.

**Segment.** The unit a carrier bills a text by: 160 characters in GSM-7 or 70 in UCS-2 for a single
message, 153 or 67 per part when concatenated. One character outside GSM-7 switches the whole message
to UCS-2.

**Encoding.** GSM-7, the seven-bit set that fits 160 characters in a segment; UCS-2, the two-byte set
that fits 70. Which one applies is decided by the final text, not by the template.

**Expiry.** The moment after which the gatekeeper stops trying to deliver: the time-to-live on
WhatsApp, the validity period on a text. Set from the content; the platform's defaults are as long as
30 days.

**Capability check.** The query to the RCS platform whether a device can receive RCS; a device that
cannot returns a 404, and the send falls back to a text.

**Fallback.** The message that goes when the rich one cannot: a text in place of an RCS card or an
MMS, written as its own version inside the segment budget.

**Statuses.** Queued, sending, sent, delivered, undelivered, failed, read. Sent is the carrier's
acceptance; delivered is confirmation from the carrier and, where available, the handset; read exists
only where receipts are on. Dropped is the platform's word for a message that reached its expiry
undelivered.

**No receipt.** The class for a send on a route that returns no delivery receipts. Neither reached
nor failed: unknown, out of both halves of the control metric, with its share read beside.

**Held.** The control metric's class for a send stopped on the state of your own channel, whether your
gate caught it or the platform refused it: no approved template, a paused template, the portfolio's
limit, the per-user marketing limit, an origin paused.

**Refused.** The control metric's class for a send the gatekeeper stopped for the number or for the
traffic: unregistered or filtered traffic, a block by the person, an invalid or deactivated number, no
account on the platform. Only the refusals that are properties of the number (the block, the invalid or
deactivated number, no account) are loss events for `contact-orchestration`.

**Addressed.** A person for whom the program requested a send in this channel outside a reply window
in the period, held sends included, whatever the basis: the basis is read in
`consent-and-preferences`' join line. `contact-orchestration`'s word, narrowed to one channel and to
sends outside a reply window.

**Reached.** At least one message of the class delivered in the period. Delivered, not sent.

## The inbound

**Keyword.** A word the origin's code acts on without a person: a stop word, a start word, a help
word, in the program's language.

**Stop words.** Stop, quit, end, revoke, opt out, cancel, unsubscribe: the words the United States
rule names as a reasonable means per se; the provider's defaults; and normal language a reasonable
person would read the same way.

**Provider block list.** The provider's list of numbers that replied with a stop word, kept in your
account with that provider; later messages from that account to them fail at the provider. Not the
record.

**Record.** The person's basis record and its instructions in `consent-and-preferences`, which every
system that texts reads. The withdrawal lives here. The provider block list holds the stops that
reached that provider, and a number on it with no instruction here is a stop the record missed.

**Single confirmation.** The one message after a stop word: sent within five minutes, confirming the
withdrawal, carrying no marketing, the only message after the request. Where the person holds several
text programs, it may ask about scope.

**Scope question.** The line in the single confirmation that asks whether the request covers all the
person's text programs. Silence means all texts that stand on consent stop.

**Distribution lag.** The time from a keyword to the last system's action on it, per system, read
beside the control metric.

**One-way origin.** An origin that cannot receive a reply, such as an alphanumeric sender ID. Its
texts carry the disclosure that two-way texting is not available and an alternative route for
withdrawal.

## Words shared with neighbors

- **template**: `email-design` means the frame and the block library; `personalization` calls an
  unresolved substitution a template token; here it is a message format the platform approved, and the
  entry in `email-design`'s vocabulary already says so.
- **reply window**: `chat-and-bots` names "the reply window a messaging platform imposes" and keeps its
  own settle window apart from it; the same word carries the same meaning here.
- **addressed**: `contact-orchestration`'s population for its loss metric; here narrowed to one channel
  and to sends outside a window.
- **class**: `contact-orchestration`, `transactional-messaging` and `push-notifications` each classify
  messages for their own purposes; here class is their word and category is the gatekeeper's.
- **campaign**: `email-program` means a scheduled send to a chosen audience; the carriers mean a
  registered use case, and this skill always writes "registered campaign" for that.
- **sending identity**: `deliverability`'s unit, the domain, its signatures and the IP it leaves
  through; not used here. The counterpart in this channel is the origin.
- **loss event**: `contact-orchestration`'s word for a stop, a block, a deactivated number; here they
  are what the gatekeeper turns into standing, and they are handed over as loss events.
- **basis record**, **instruction**: `consent-and-preferences`' units; referred to here, never
  redefined.
- **suppression**: the neighbors use it in several senses already; this skill avoids the word and
  says provider block list or record.
- **fallback**: `personalization` means what a message carries when a substitution cannot resolve,
  taken down its fallback ladder; here it is the text that goes when the rich message cannot. Moving a
  message to another channel is never a fallback: it is failover in `transactional-messaging`'s word,
  and the next channel of a cascade in `triggered-messages`'.
- **provider**: `deliverability` means the mailbox provider that receives email; here the provider is
  the company that carries your texts and messaging app messages and reports their statuses.
- **held**: in `contact-orchestration` a send its policy stopped, suppressed or deferred, which then
  never reaches this skill as a request (its delivery state before the send is *reserved*); here held is a send stopped on the state of the channel.
  That skill's unknown, a receipt window that closed empty, splits here: no receipt on a route that
  returns none, failed on a route that does.
- **expiry**: `push-notifications` and `in-product-messaging` use the same idea for their surfaces, the
  moment set from the content; `consent-and-preferences`' expiry event is another thing, the event a
  basis's lifetime counts from.
