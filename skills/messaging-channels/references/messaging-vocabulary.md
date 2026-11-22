---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Vocabulary for messaging-channels

The terms all three mechanics assume. The last section lists the words this skill shares with its
neighbors, several of them under other meanings.

## What sets this work apart

Three properties make the channel unlike any other in this library.

1. **The gatekeeper prices every message and scores the sender collectively.** A carrier bills per
   segment; a messaging platform bills per delivered template, by category. The platform reads
   blocks and reports, pauses a template or holds the business at its limit. One bad send costs every
   send after it.
2. **A message from the business and a reply to the person are two regimes.** Outside a reply window
   the business speaks only through approved templates of a declared category; inside 24 hours of
   the person's last message it speaks freely. SMS has no window, and instead has keywords that have
   to work.
3. **The address is a phone number, and the person may not be on the platform.** Reachability is
   checked per platform: RCS by a capability check on the device, WhatsApp by the provider's error on
   a number with no account, and SMS goes to any mobile number and returns no signal that anyone read
   it.

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

**No receipt.** The provider reports sent on a route that returns no delivery receipts. Neither reached
nor failed: unknown, out of both halves of the control metric, with its share read beside.

**Held.** The control metric's class for a send stopped on the state of your own channel, whether your
gate caught it or the platform refused it: no approved template, a paused template, the portfolio's
limit, the per-user marketing limit, an origin paused.

**Refused.** The control metric's class for a send the gatekeeper stopped for the number or for the
traffic: unregistered or filtered traffic, a block by the person, an invalid or deactivated number, no
account on the platform. Only the refusals that are properties of the number (the block, the invalid or
deactivated number, no account) are loss events for `contact-orchestration`.

**Addressed.** A person for whom the program handed a send of the class to this channel outside a
reply window during the period. Held sends and cancellations after handoff count; a request stopped
before handoff does not. Audit marketing sends that went out separately in
`consent-and-preferences`' join line. `contact-orchestration`'s word, narrowed to one channel and to
sends outside a reply window.

**Reached.** An addressed person with at least one confirmed delivery before expiry from a handoff
in that week's origin and class. The handoff fixes the week, not the delivery or receipt date.
Delivered, not sent.

## The inbound

**Keyword.** A word the origin's code acts on without a person: a stop word, a start word, a help
word, in the program's language.

**Stop words.** The terms an origin recognizes as opt-out requests. For TCPA-covered US texts, see
[US TCPA revocation](legal-regimes.md#us-tcpa-revocation) for the FCC's keyword list, the conditions
for an exclusive method, and the rule for reasonable requests. Providers and platforms can recognize
other words or ordinary language under their own rules.

**Provider block list.** The provider's list of numbers that replied with a stop word, kept in your
account with that provider; later messages from that account to them fail at the provider. Not the
record.

**Record.** The person's basis record and its instructions in `consent-and-preferences`. A valid
withdrawal belongs here with its route, wording, receipt time, and scope, even when the provider
has no block to report. Each affected sending system reads the instruction and confirms application.

**Confirmation.** The acknowledgment to the person of what stopped. For a web request, the page
names the affected category and number without promising a provider block or reply. A confirmation
text states what stopped, without promotions or questions. The FCC does not require the text; see
[US TCPA revocation](legal-regimes.md#us-tcpa-revocation) for its timing and limits. Keep carrier and
platform requirements separate and do not duplicate the provider's reply.

**Scope of revocation.** The streams a valid opt-out reaches. For TCPA-covered traffic, it depends on
the caller and whether the communication was advertising, telemarketing, or informational. The
provider's pool block is separate. See [US TCPA revocation](legal-regimes.md#us-tcpa-revocation).

**Distribution lag.** For each affected sending system, the time from receipt of a valid withdrawal
request to that system's confirmed application of the instruction. The last application sets the
overall lag. An acknowledgment of receipt alone does not close the check. Read lag beside the
control metric.

**One-way origin.** An origin that cannot receive a reply, such as an alphanumeric sender ID. Its
texts carry the disclosure that two-way texting is not available and an alternative route for
withdrawal. That route can receive a valid request without a keyword or provider block. Count the
lag from receipt on that route.

## Seams with neighbors

- **The origin's standing is not the person's basis for receiving texts.** The basis is a record
  in `consent-and-preferences`, one per person, channel and purpose. Standing is the gatekeeper's
  judgment of the origin. A green rating grants nobody permission, and a written opt-in does not keep
  a template from being paused.
- **The cascade decides the order; this skill decides what each status means.** `triggered-messages`
  says SMS comes after the app message and how long to wait. This skill says which statuses count as
  reached, which as failed, which as held and which as unknown, so that a message that never landed
  moves the cascade on a fact. For marketing, use the response condition `triggered-messages` sets
  for the step. For a required service action, use the checkpoint in `transactional-messaging`'s
  `deadline-channel-and-failover.md`, step 5.
- **The reply window is not the settle window.** The platform's window says how long you may answer
  freely, and belongs here. How long `chat-and-bots` waits before an issue counts as settled is its own
  window, with the same person and a different clock.
- **A class is the neighbors' word; a category is the gatekeeper's.** `transactional-messaging` and
  `contact-orchestration` give a message its class. This skill maps the class onto the category the
  platform approves and prices, and the mapping is not free: mixed content is marketing on both sides.
- **A provider block and a recorded withdrawal are separate.** `consent-and-preferences` determines
  validity and scope. Apply that scope and verify application in each affected system, including for
  a web request with no block. Respect a real provider block within its pool; lifting it does not
  establish a basis to send.
- **The price of a text decides where the in-product message comes first.** `in-product-messaging`
  shows a pitch inside the product first to people who open the product more often than the pitch's
  window lasts, and the text goes only to those who did not appear by its cut-off. The price sits here;
  the order sits with `triggered-messages`.

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
  required notice off a channel that lost its basis calls for channel selection in
  `transactional-messaging`. Technical failover there requires a separate trigger. For a marketing
  cascade, `triggered-messages` chooses the next channel.
- **provider**: `deliverability` means the mailbox provider that receives email; here the provider is
  the company that carries your texts and messaging app messages and reports their statuses.
- **held**: in `contact-orchestration` a send its policy stopped, suppressed or deferred, which then
  never reaches this skill as a request (its delivery state before the send is *reserved*); here held is a send stopped on the state of the channel.
  That skill's unknown, a receipt window that closed empty, splits here: no receipt if the provider
  reported sent on a route that returns none, failed on a route that issues receipts.
- **expiry**: `push-notifications` and `in-product-messaging` use the same idea for their surfaces, the
  moment set from the content; `consent-and-preferences`' expiry event is another thing, the event a
  basis's lifetime counts from.
