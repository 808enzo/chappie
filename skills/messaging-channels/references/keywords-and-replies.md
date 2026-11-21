---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Keywords and replies

The unit here is **the inbound**: a message that arrives on an origin. It can be a keyword, a tapped
button, or a free-text reply. Check for a revocation before routing a reply to `chat-and-bots`.
This file also covers withdrawals received outside the origin, how to apply them, and what to confirm.

## Entry conditions

For an origin that can receive replies, start with the keyword table. For a withdrawal through an
alternative route, start at step 2. A one-way origin, such as an alphanumeric sender ID, cannot
receive replies; its texts carry the disclosure and the alternative route
(`references/origin-and-standing.md`, step 2).

## Exit conditions

A keyword table per origin and language. A person-level withdrawal record and confirmation that
each affected system applied it. A separate entry for any provider block. No duplicate confirmation
to the person. The HELP reply and the route for every other reply. A ledger with the lag per system.

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

**2. Record the withdrawal and check for a provider block separately.** At receipt, capture the route,
the request wording, the number, the origin if known, and the receipt time. Use
`consent-and-preferences` to check whether the request is valid and what it covers. Write a valid
revocation to the **person-level record** with that scope and the original receipt details. A valid
web request from a one-way origin needs no keyword or provider event to enter the record.

For a valid TCPA revocation in response to advertising or telemarketing, stop all covered advertising
and telemarketing calls and texts from that caller, across its origins. For a valid revocation in
response to an informational call or text, stop the category it targets unless the request expressly
reaches further. Pass the recorded scope to each affected sending system (step 4). Check the
remaining basis and channel rules before keeping another stream.

If the provider blocks the number, record and respect that block separately. For example, when
Twilio matches an opt-out keyword, it blocks the number in its pool, and subsequent sends subject
to the block fail with error 21610. The pool can be broader or narrower than the withdrawal's scope.
See the edge cases below for a separately requested code.

**3. If you confirm the withdrawal, use a plain confirmation and avoid a duplicate.** Where the
provider answers a keyword itself (on Twilio, Advanced Opt-Out matches the keyword and "returns the
confirmation message"), use that answer and do not send an extra copy. The FCC does not require a
confirmation text. If you send one under its rule, confirm what stopped and leave out promotions and
questions. Apply the revocation without waiting for a reply. The timing table gives the presumption
and what a late confirmation needs. For a web request, confirm the affected category and number on
the page without promising a provider block or reply. Do not send a text to repeat the page's
confirmation. If a required service notice loses its basis on this channel, use
`transactional-messaging`'s failover to a permitted channel. The carriers' principles ask for
"one final opt-out confirmation message per campaign" and say "no further messages should be sent
following the confirmation message". Apply those principles separately from the FCC rule.
On WhatsApp, requests "either on or off WhatsApp" are honored, "including
removing that person from your contacts list"; on RCS, a revocation applies "across all of their
promotional agents".

**4. Distribute inside the propagation deadline.** Honor a valid TCPA revocation within a reasonable
time from receipt; see the ceiling below. `consent-and-preferences` sets the propagation deadline for
texts, using the shortest window that applies. Have each affected system apply the instruction to
the streams it covers and cancel their queued sends. Get a timestamped acknowledgment from each
affected system that it applied the instruction, including the queue changes. Acknowledging receipt
of the instruction does not confirm application. A send within the withdrawn scope after the deadline
is unsupported. Log any sends within the window by system and track application lag in step 8.

**5. Answer HELP with the program's card.** The program's name, a way to reach customer care, how to
stop; the same elements the carriers' principles put in the opt-in confirmation of a recurring
program. No promotional content.

**6. Route everything else as a reply.** A tapped button and a free-text reply open the reply window
and a conversation: `chat-and-bots` gives it an issue and an assignee. Every automated message that can
be answered says in its own text whether replies are read, so that a person who writes back to an
unattended origin learns it before they wait. Check a STOP reply to an authentication code under the
same route and scope rules as other replies (steps 1 and 2).

**7. Log a start keyword without assuming it restores permission.** Start and unstop lift the
provider's block, and on Twilio they are reserved for that. Log the keyword's source ("reply START"),
date, and the text the person was replying to. Use `consent-and-preferences` to verify and record
any basis before resuming sends. The keyword or lifted block alone does not establish that basis.

**8. Log and verify application.** Log the receipt details and scope, any keyword, provider block,
or provider reply, and each affected system's application timestamp. Measure each system's lag from
receipt of the request to its application of the instruction. Keep the check open until each affected
system confirms application. Flag any missing confirmation at the deadline and use the last
application timestamp for the overall lag. Read the per-system lag beside the control metric to find
which system to fix.

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
- **A one-way origin.** Take a valid withdrawal through the disclosed alternative route. Start at
  step 2 and count from receipt on that route. For a designated web page, confirm there as in step 3
  and verify application in steps 4 and 8 even when there is no provider block or reply.
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
