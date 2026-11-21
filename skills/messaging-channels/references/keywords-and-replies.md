---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Keywords and replies

The unit here is **the inbound**: a message that arrives on an origin. It can be a keyword, a tapped
button, or a free-text reply. Check for a revocation before routing a reply to `chat-and-bots`. This
file sets the provider and record steps, what a confirmation can say, and where other replies go.

## Entry conditions

Messages leave from an origin that can receive replies: a ten-digit number, a short code, a
toll-free number, a WhatsApp business number, an RCS agent. A one-way origin, such as an alphanumeric
sender ID, has no inbound; its texts carry the disclosure and the alternative route
(`references/origin-and-standing.md`, step 2), and the withdrawal arrives by that route and is handled
from step 2 below.

## Exit conditions

A keyword table per origin and language. The catch on two levels, provider and record, with the
distribution of the recorded scope to every system that texts. A confirmation without a duplicate
if one is used or required. The HELP reply. The routing of every other reply. An inbound
ledger with the lag per system.

## Steps

**1. Write the keyword table per origin and language.** For TCPA-covered US calls and texts, check
the method and disclosure against [US TCPA revocation](legal-regimes.md#us-tcpa-revocation). If the
caller designates keyword replies as exclusive, accept `stop`, `quit`, `end`, `revoke`, `opt out`,
`cancel`, and `unsubscribe`, even when only one word appears in the message. Without a valid
exclusive designation, honor reasonable requests, including those in ordinary language. Keep the
provider's defaults (Twilio adds stopall and optout). Under the carriers' principles, act on ordinary
language such as "please opt me out"; case and punctuation change nothing. Start: start, unstop.
Help: help. In a program that runs in another language, the
equivalents in that language, which the RCS policy names outright ("'STOP' message or equivalent in
agent's language"). The provider keeps its own reserved words; on Twilio "stop", "start", "unstop"
and "help" cannot be removed.

**2. Catch the keyword on two levels.** The provider blocks the number in its own pool: on Twilio the
number goes onto a list of blocked numbers, and later messages from your account to it fail with error
21610. Log the request and its receipt time in the **record** (`consent-and-preferences`). For a valid
TCPA revocation that responds to advertising or telemarketing, record all covered advertising and
telemarketing calls and texts from that caller as stopped, across its origins. For a valid revocation
in response to an informational call or text, record the category it targets unless it expressly
reaches further. Pass the scope to every sending system so it can suppress the affected streams. The provider's block follows
its pool and can be broader or narrower than the legal withdrawal. Check the remaining basis and
channel rules before keeping another stream. See the edge cases below for a separately requested code.

**3. If you confirm the withdrawal, use a plain confirmation and avoid a duplicate.** Where the
provider answers a keyword itself (on Twilio, Advanced Opt-Out matches the keyword and "returns the
confirmation message"), use that answer and do not send an extra copy. The FCC does not require a
confirmation. If you use one under its rule, confirm what stopped and leave out promotions and
questions. Apply the revocation without waiting for a reply. The timing table gives the presumption
and what a late confirmation needs. If a required service notice loses its basis on this channel,
use `transactional-messaging`'s failover to a permitted channel. The carriers' principles ask for
"one final opt-out confirmation message per campaign" and say "no further messages should be sent
following the confirmation message". Apply those principles separately from the FCC rule.
On WhatsApp, requests "either on or off WhatsApp" are honored, "including
removing that person from your contacts list"; on RCS, a revocation applies "across all of their
promotional agents".

**4. Distribute inside the propagation deadline.** Honor a valid TCPA revocation within a reasonable
time from receipt; see the ceiling below. `consent-and-preferences` sets the propagation deadline for
texts, using the shortest window that applies. A send within the withdrawn scope after the deadline
is unsupported. Read sends within the window as lag, by system. Step 8 tracks that lag,
and the system with the longest lag is the one to fix.

**5. Answer HELP with the program's card.** The program's name, a way to reach customer care, how to
stop; the same elements the carriers' principles put in the opt-in confirmation of a recurring
program. No promotional content.

**6. Route everything else as a reply.** A tapped button and a free-text reply open the reply window
and a conversation: `chat-and-bots` gives it an issue and an assignee. Every automated message that can
be answered says in its own text whether replies are read, so that a person who writes back to an
unattended origin learns it before they wait. Check a STOP reply to an authentication code under the
same route and scope rules as other replies (steps 1 and 2).

**7. Treat a start keyword as a basis event, not as a flag flip.** Start and unstop lift the
provider's block, and on Twilio they are reserved for that. For the record, the
keyword is an event with a source ("reply START"), a date, and the text the person was replying to,
and `consent-and-preferences` writes the basis from it. A keyword alone creates no record.

**8. Keep an inbound ledger.** The keyword, the time, the origin, and the action in every system with
its timestamp. The lag from the keyword to the last system's action is read beside the control metric,
per system; the system with the longest lag is the one to fix.

## Thresholds and timings

| Quantity | Value | Where it comes from |
|---|---|---|
| TCPA confirmation | optional, only confirms the request, no marketing or promotion; within 5 minutes of receipt, presumed within prior express consent; later, show that the delay was reasonable | FCC rule, 47 CFR 64.1200(a)(12) |
| TCPA revocation | within a reasonable time, at most 10 business days from receipt | FCC rule, 47 CFR 64.1200(a)(10) and (11) |
| FCC keyword replies | stop, quit, end, revoke, opt out, cancel, unsubscribe; see the designation and disclosure conditions in step 1 | FCC rule, 47 CFR 64.1200(a)(10)(ii) |
| The provider's refusal after a block | error 21610 on Twilio | platform behavior, Twilio |
| The window a reply opens | 24 hours | platform rule, Meta |
| Your distribution target | inside `consent-and-preferences`' propagation deadline for texts, with the lag read per system | yours |

The FCC rows are class 2; see the source and limits in [US TCPA revocation](legal-regimes.md#us-tcpa-revocation).
The platform rows carry their sources below. The last row is yours.

## Edge cases

- **STOP on a service-only origin.** If it is a valid TCPA revocation in response to an informational
  text, apply it to the category it targets unless the request expressly reaches further. If a
  required notice loses its basis, route it as in step 3.
- **STOP sent to the brand's other origin.** The RCS policy extends a revocation across all of a
  brand's promotional agents. For a TCPA-covered request, check the route, identify the caller and
  apply the scope from steps 1 and 2. A different number does not create a different caller or basis.
- **A typo, or another language.** Without a valid exclusive designation, honor a reasonable TCPA
  request. Check any separate carrier or platform requirement to act on ordinary language or equivalents.
- **A one-way origin.** The withdrawal arrives by the alternative route the text named, and runs
  from step 2 on the same clock.
- **A reply after the platform's window closed.** It opens a new one: answer freely, and the
  conversation is `chat-and-bots`'.
- **A stop in reply to an authentication code.** Record the valid revocation's scope (steps 1 and 2).
  On Twilio, later messages to the blocked number fail with error 21610, including the next code the
  person asks for. Do not lift or route around the block. On error 21610, offer another permitted
  channel and say how to request texts again. `consent-and-preferences` assesses the basis for a
  separately requested code under FCC 15-72. Keep the stop entry and do not restart the program.

## Failure modes

**The provider caught the word and the record never saw it.** The sign: a number on the provider's
block list with no instruction in the record, and sends after withdrawal from a second system in
`consent-and-preferences`' join line.

**A confirmation with an offer.** Remove the offer before sending. A text with a promotion does not
qualify for the confirmation exception in the [US TCPA revocation rule](legal-regimes.md#us-tcpa-revocation).

**No confirmation.** Treat the omission as a failure only if an applicable carrier or platform rule
requires a confirmation. Apply the revocation whether or not you send a confirmation.

**Replies nobody reads.** The sign: windows open and close with no outbound message inside them;
questions in replies with no issue opened in `chat-and-bots`.

**Sources for the rules in this file. Platform sources opened 2026-09-15.**

- FCC, 47 CFR 64.1200(a)(10) through (12): see the rule and source in
  [US TCPA revocation](legal-regimes.md#us-tcpa-revocation).
- CTIA, Messaging Principles and Best Practices, May 2023, sections 5.1.2.1 and 5.1.3:
  https://api.ctia.org/wp-content/uploads/2023/05/230523-CTIA-Messaging-Principles-and-Best-Practices-FINAL.pdf
- Twilio, Advanced Opt-Out (default and reserved keywords, the list of blocked numbers, later
  messages from your account failing with error 21610, the confirmation message returned on a
  keyword, start and unstop reserved):
  https://www.twilio.com/docs/messaging/tutorials/advanced-opt-out
- WhatsApp Business Messaging Policy (requests on or off WhatsApp):
  https://whatsappbusiness.com/policy/
- Google, RCS for Business, Acceptable Use Policy (STOP or its equivalent; revocation across all
  promotional agents):
  https://developers.google.com/business-communications/rcs-business-messaging/terms-and-policies/aup
- Meta, WhatsApp Business Platform, Pricing (the 24 hour customer service window):
  https://developers.facebook.com/docs/whatsapp/pricing
