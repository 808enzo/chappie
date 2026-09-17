---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The send: category, window, form, price, status

The unit here is **the send**: one message to one phone number from one origin, in one class. A
neighboring skill has already decided that the message goes and to whom: `transactional-messaging`
for a service line, `contact-orchestration` for a touch under the cap, `triggered-messages` for a step
of a cascade. This file decides what the gatekeeper will accept, in which regime, at what price, and
what it will say afterward.

## Entry conditions

A neighbor requested the send with its class. The person has a number on record and a basis for this
class in this channel (`consent-and-preferences`). The origin exists and its standing is read
(`references/origin-and-standing.md`).

## Exit conditions

Named for the send: the gatekeeper's category; the regime, window or template; the reachability
check; a template approved and not paused, with every substitution given a fallback; the segment
budget for a text; the expiry; the price before the send; the status that will come back and what
each status means to the cascade.

## Steps

**1. Map the class onto the gatekeeper's category.** A template is marketing, utility, for what the person's own
action set in motion, or authentication, for codes; a free-form reply inside a window carries no
template category. The class is the neighbors' word and the category the platform's, and the map is not free. Mixed content
is marketing: the platform's categorization page treats "an order update with a promo or a feedback
survey with promotional content" as marketing, and the carriers' principles say that "adding a
call-to-action (e.g., a coupon code to an informational text) may place the message in the promotional
category". A service line with a promotional sentence loses its class with the gatekeeper and with the
law at the same time (`transactional-messaging`, `consent-and-preferences`). The platform also runs "a
recurring process to identify and update approved templates that should be of a different category",
with notice before the change; when a utility template becomes marketing, its price, its per-user
limit and its opt-in requirement change with it.

**2. Pick the regime.** A reply window is open when the person's last message is younger than 24
hours: you may write freely, and utility templates sent inside it are free. When a conversation starts at an entry point the pricing page counts as free and you answer
inside the reply window, a 72 hour free entry point window opens in which every message you send is
free. It does not extend the reply window: once 24 hours pass without a message from the person, only
templates go out, free until the 72 hours end. Which entry points qualify is on that page. Outside a
window, only an
approved template of the right category goes out. SMS has no regime of this kind; its obligation is
the keyword table (`references/keywords-and-replies.md`). Marketing inside an open window still stands
on an opt-in for marketing: the platform's opt-in covers categories, and a reply that carries a
promotional block is a touch for `contact-orchestration`, as `chat-and-bots` already counts it.

**3. Check reachability on the platform before the request, not after the refusal.** RCS: run the
capability check; a device without RCS returns a 404 from the platform, and the agent falls back to
another technology, such as SMS, whose text has to fit the segment budget of step 5. WhatsApp: where
your provider returns an error for a number with no account, record the number as unreachable in this
channel, with the date, and stop requesting it here until the person writes to you there or a new basis
for this channel is recorded. SMS: the number is mobile, is not on the provider's block list, has no
withdrawal in the record, and has not appeared in a deactivation file. A person found unreachable here
goes to the next channel in `triggered-messages`' order and is not requested from this channel, so that
the control metric's denominator holds only people this channel could have reached. The people kept out
this way are a pool of their own, read beside the control metric in `SKILL.md`.

A message goes to one number of the person: the one the record marks as the number for this channel.
A person with two numbers is one person with two addresses, and a message sent to both is two sends
against one touch of `contact-orchestration`'s cap. A number with no link to a record is an anonymous
address, and for the cap it counts as a separate person.

**4. Run the template lifecycle ahead of the campaign.** Submit early; templates are reviewed on
creation and after every edit, and an edit to the text starts a new review. Give the template the
category its content earns: a mismatch is a rejection or a later recategorization. A new template's
quality is UNKNOWN until the platform has usage, feedback and engagement signals, so the first sends
with it are part of the ramp, not the campaign. Substitutions are resolved at send time and get no second chance, so every
substituted value has a fallback (`personalization` owns the fallback ladder). Buttons: quick replies, a link,
and, in every marketing template, an exit: a stop button or a "reply STOP" line. One template does one
job; the rule that a statement without a fact behind it gets cut applies to a template as it applies
to a subject line (`email-copy`).

**5. Budget the segments of a text.** One segment holds 160 characters in GSM-7 or 70 in UCS-2; a
concatenated message holds 153 or 67 per part, because each part carries a header; a single character
outside the GSM-7 set, an emoji, a curly quote, a letter outside the set, switches the whole message to
UCS-2; each part is billed as a message. Count segments on the final text after substitution, not on
the template: a long name or a long product title can add a part. Aim for one segment; a link on
your own domain, so that the name in the link matches the name in the registration and the person can
tell who is writing.

**6. Set the expiry from the content, never from the default.** On WhatsApp the default time-to-live
is 10 minutes for authentication templates (30 days for authentication templates created before
October 23, 2024) and 30 days for utility and marketing; you can set authentication to between 30
seconds and 15 minutes, utility to between 30 seconds and 12 hours, marketing to between 12 hours
and 30 days. A marketing template left at its default delivers an offer to a phone that comes back
online three weeks after the offer ended. If no delivered status arrives before the expiry, assume the
message was dropped. A text has the provider's validity period, under the same rule: the moment the
content stops being true, as `push-notifications` sets it.

**7. Price the send before it leaves.** A text costs the price of a part times the number of parts,
billed for what was submitted; an undelivered text still costs. A WhatsApp template costs per
delivered message, by category, since July 1, 2025; an attempt with a paused template is refused and
not charged; a utility template inside an open window is free. A refusal with code 131049 means the
person has reached the marketing template limit the platform applies across all businesses: do not
retry for at least 24 hours, and hand the send to the cascade as held. The price decides where a
pitch whose only outside channel is a text shows first: inside the product for people who open the
product more often than the pitch's window lasts, and by text only for those who did not appear by its
cut-off (`in-product-messaging`).

**8. Hand the cascade a status it can act on.** The statuses a provider reports run queued, sending,
sent, delivered, undelivered, failed, and read; read exists only on RCS and WhatsApp with receipts on.
**Sent means the carrier accepted the message; it is not delivery.** Delivered means the carrier
confirmed it, and, where available, the handset did; receipts are not returned on every route. The
classes the cascade gets:

| Class | Statuses | What the cascade does |
|---|---|---|
| reached | delivered, read | the message landed; whether the cascade moves on is the response condition `triggered-messages` sets for the step, not a status |
| failed | undelivered, failed; on WhatsApp, no delivered status before the time-to-live | the next channel in the order, at once |
| held | refused or never submitted for the state of your own channel: a paused template, the limit, code 131049 | the order decides: the next channel now, or the same channel after the wait the refusal names (131049: at least 24 hours) |
| no receipt | sent, on a route that returns no delivery receipts | unknown, never reached: a marketing cascade moves on its response condition; a service line follows `transactional-messaging`, which fails over in such a channel only on a confirmed failure |

A send still at sent on a route that returns receipts is not in a class yet: it waits for its receipt,
and the requester's deadline, not the validity period, decides how long. `transactional-messaging` fails
a service line over when its deadline minus the next channel's tail latency passes with no receipt. With
no deadline, the wait ends at the expiry, and the send counts as failed, as the platform tells you to
assume on WhatsApp.

A cascade condition of "did not open" does not exist for texts: nothing reports an open. On the
platforms that report read, a read receipt is a setting the person controls, so its absence is not a
fact about the person either.

**9. Pace the send.** WhatsApp counts unique recipients outside a window in a moving 24 hour period
against the portfolio's limit, and every number in the portfolio spends the same limit: pace marketing
so that the service lines' daily peak still fits under it (`references/origin-and-standing.md`, step 3). A carrier's throughput is a property of the origin type and your
provider states it. Send in the recipient's local time; the quiet hours belong to
`contact-orchestration`, together with the federal solicitation window it records.

## Thresholds and timings

| Quantity | Value | Where it comes from |
|---|---|---|
| Reply window | 24 hours from the person's last message | platform rule, Meta |
| Free entry point window | 72 hours from your reply inside the reply window; every message in it is free; the reply window inside it stays 24 hours | platform rule, Meta |
| Segment | 160 GSM-7 or 70 UCS-2; concatenated 153 or 67 per part; one character outside GSM-7 switches the whole message | platform rule, Twilio and Vonage |
| Concatenation ceiling | the provider's; Twilio states 1,600 GSM-7 or 700 UCS-2 characters | platform rule, Twilio |
| Default time-to-live, WhatsApp | authentication 10 minutes (30 days if created before October 23, 2024); utility and marketing 30 days | platform rule, Meta |
| Time-to-live ranges, WhatsApp | authentication 30 seconds to 15 minutes; utility 30 seconds to 12 hours; marketing 12 hours to 30 days | platform rule, Meta |
| Pricing, WhatsApp | per delivered template message, by category, from July 1, 2025; utility inside a window free; paused template attempts not charged | platform rule, Meta |
| Per-user marketing limit | code 131049; no retry for at least 24 hours | platform rule, Meta |
| Expiry | the moment the content stops being true | yours |
| Segments per marketing text | counted on the final text; the aim is one | yours |

The platform rows are class 2 and carry their sources below. The last two are yours.

## Edge cases

- **The platform recategorized a template.** A utility template is now marketing: its price rose,
  the per-user limit applies, and the person needs an opt-in for marketing on record. The service line
  that used it is no longer a service line. Remove the promotional element and submit a new utility
  template; do not keep sending the old one to people with a service basis only.
- **The person replied, and a neighbor wants the answer to carry an offer.** Inside the window the
  text is free, but marketing stands on the marketing opt-in, and the reply with an offer is a touch
  under the cap.
- **An authentication code.** The default expiry is 10 minutes. The code does not fail over on its
  own: at its deadline the screen offers the other channel and the person chooses
  (`transactional-messaging`), and "sent" moves nothing.
- **A rich message with a text fallback.** An RCS rich card or an MMS falls back to a text without
  the image and the buttons. The fallback text is a version of its own inside the segment budget, not
  a truncation.

## Failure modes

**An emoji doubled the bill.** The sign: two or more segments per message on texts shorter than 160
characters. One character switched the encoding.

**"Sent" was read as delivered.** The sign: the cascade never moves to the next channel for people
whose texts were undelivered or dropped; on a route without receipts, the no-receipt share reads zero
because nobody defined the class.

**A dead offer three weeks late.** The sign: deliveries of a marketing template dated after the
offer's end. The time-to-live was left at its 30 day default.

**A recategorized template that nobody noticed.** The sign: the price of a service template became a
marketing price; refusals with code 131049 on a service line; a person with a service basis only
receiving what the platform now calls marketing.

**Sources for the platform rules in this file, each opened 2026-09-15.**

- Meta, WhatsApp Business Platform, Pricing (categories, per-message pricing from July 1, 2025,
  charged when delivered, the 24 hour customer service window, the 72 hour free entry point window in
  which every message is free while only templates go out once the 24 hours close, utility templates
  free inside the window): https://developers.facebook.com/docs/whatsapp/pricing
- Meta, Template categorization (mixed content, recategorization with notice):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-categorization
- Meta, Template fundamentals (review on creation and after editing, statuses):
  https://developers.facebook.com/docs/whatsapp/message-templates/guidelines
- Meta, Template quality rating (UNKNOWN on a new template):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-quality
- Meta, Template pausing (attempts rejected and not charged):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pausing
- Meta, Per-user marketing template message limits (code 131049, 24 hours, sends inside a window do
  not count):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/marketing-templates/per-user-limits
- Meta, Time-to-live (defaults, ranges, "assume the message was dropped"):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/time-to-live
- Meta, WhatsApp Business Platform, Messaging limits (moving 24 hour period, unique recipients, one
  limit per portfolio shared by its numbers):
  https://developers.facebook.com/docs/whatsapp/messaging-limits
- Twilio, What is the SMS character limit (160 and 70, 153 and 67, the encoding switch, billing per
  segment, 1,600 and 700): https://www.twilio.com/docs/glossary/what-sms-character-limit
- Vonage, SMS concatenation and encoding (160 and 70, the header, all characters in UCS-2, billed per
  part): https://developer.vonage.com/en/messaging/sms/guides/concatenation-and-encoding
- Twilio, Message resource (status values; "sent" as carrier acceptance; receipts "where
  available"): https://www.twilio.com/docs/messaging/api/message-resource
- Google, RCS for Business, How it works (capability check, 404, fallback to SMS):
  https://developers.google.com/business-communications/rcs-business-messaging/guides/get-started/how-it-works
- CTIA, Messaging Principles and Best Practices, May 2023, Exhibit II (a coupon code in an
  informational text):
  https://api.ctia.org/wp-content/uploads/2023/05/230523-CTIA-Messaging-Principles-and-Best-Practices-FINAL.pdf
