---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Keywords and replies

The unit here is **the inbound**: a message that arrives on an origin. A keyword, a tapped button, a
free-text reply, a typo that a reasonable person would read as "stop". The provider sees it first; the
record has to see it next; and everything that is not a keyword opens a window and a conversation
that belongs to `chat-and-bots`. This file decides how a keyword is caught on both levels, what the one
message after it says, and where the rest goes.

## Entry conditions

Messages leave from an origin that can receive replies: a ten-digit number, a short code, a
toll-free number, a WhatsApp business number, an RCS agent. A one-way origin, such as an alphanumeric
sender ID, has no inbound; its texts carry the disclosure and the alternative route
(`references/origin-and-standing.md`, step 2), and the withdrawal arrives by that route and is handled
from step 2 below.

## Exit conditions

A keyword table per origin and language. The catch on two levels, provider and record, with the
distribution to every system that texts. The single confirmation, with its scope question where the
person holds several text programs. The HELP reply. The routing of every other reply. An inbound
ledger with the lag per system.

## Steps

**1. Write the keyword table per origin and language.** Stop: "stop," "quit," "end," "revoke," "opt
out," "cancel," "unsubscribe", the words the United States rule names as a reasonable means per se,
plus the provider's defaults (Twilio adds stopall and optout) and normal language such as "please opt
me out", which the carriers' principles say should be read and acted upon and the United States rule
requires honoring when a reasonable person would read it as a request to stop; case and punctuation
change nothing. Start: start, unstop. Help: help. In a program that runs in another language, the
equivalents in that language, which the RCS policy names outright ("'STOP' message or equivalent in
agent's language"). The provider keeps its own reserved words; on Twilio "stop", "start", "unstop"
and "help" cannot be removed.

**2. Catch the keyword on two levels.** The provider blocks the number in its own pool: on Twilio the
number goes onto a list of blocked numbers, and later messages from your account to it fail with error
21610. That block is not the withdrawal. The **record** (`consent-and-preferences`, its instruction
routes) receives the same keyword at the same moment, and from the record it travels to every system
that texts this person from another origin: the sales platform, the support desk, the authentication
provider, a second provider, a second brand. The provider's list is tied to its pool, not to the
person; a keyword that reached only the provider leaves the other systems texting. What the
authentication provider does with a code the person asks for afterward is in the edge cases below.

**3. Send the single confirmation, and make it the last message.** Where the provider answers a
keyword itself (on Twilio, Advanced Opt-Out matches the keyword and "returns the confirmation
message"), that answer is the single confirmation: write the scope question into the provider's
confirmation text, and send nothing of your own. One message, within five minutes
of the keyword, which the United States rule presumes to fall inside the person's consent; later, and
the sender has to show the delay was reasonable. It confirms the withdrawal and carries no marketing
or promotional content, and it is the only message after the request. Where the person consented to
several categories of texts from this sender, the confirmation may ask whether the request covers all
of them; absent an answer, every text that requires consent stops, service texts standing on consent
included. A service line the law itself requires (a delay notice, a confirmation of a distance
contract: `transactional-messaging` names them) does not stop; it moves to another channel by that
skill's failover. The carriers' principles ask for "one final opt-out confirmation message per
campaign" and say "no further messages should be sent following the confirmation message". Where one
stop covers several campaigns, the United States rule still allows one message in all, so one
confirmation goes, not one per campaign. On WhatsApp, requests "either on or off WhatsApp" are honored, "including
removing that person from your contacts list"; on RCS, a revocation applies "across all of their
promotional agents".

**4. Distribute inside the propagation deadline.** The United States rule sets the outer bound at ten
business days from receipt. `consent-and-preferences` sets the propagation deadline for texts, the
shortest window that applies: a send from any system after it is unsupported, and a send inside it is
the cost of the lag, which that skill reads beside, by system. The lag per system is read in step 8,
and the system with the longest lag is the one to fix.

**5. Answer HELP with the program's card.** The program's name, a way to reach customer care, how to
stop; the same elements the carriers' principles put in the opt-in confirmation of a recurring
program. No promotional content.

**6. Route everything else as a reply.** A tapped button and a free-text reply open the reply window
and a conversation: `chat-and-bots` gives it an issue and an assignee. Every automated message that can
be answered says in its own text whether replies are read, so that a person who writes back to an
unattended origin learns it before they wait. A "stop" typed in reply to an authentication code is
still a stop: the word is per se, and the origin it arrived on does not narrow it.

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
| Confirmation of a withdrawal | one message, within five minutes for the presumption, no marketing, the only message after the request | statute, 47 CFR 64.1200(a)(12) |
| Execution of a withdrawal | within a reasonable time, not to exceed ten business days from receipt | statute, 47 CFR 64.1200(a)(10) |
| Per se stop words | stop, quit, end, revoke, opt out, cancel, unsubscribe | statute, 47 CFR 64.1200(a)(10) |
| The provider's refusal after a block | error 21610 on Twilio | platform behavior, Twilio |
| The window a reply opens | 24 hours | platform rule, Meta |
| Your distribution target | inside `consent-and-preferences`' propagation deadline for texts, with the lag read per system | yours |

The statute rows are class 2; the rule and its boundary stand in `SKILL.md`, whose owner is
`consent-and-preferences`. The platform rows carry their sources below. The last row is yours.

## Edge cases

- **STOP on a service-only origin.** Every text standing on consent stops; the line the law requires
  moves to another channel; the confirmation asks about scope, and silence means all.
- **STOP sent to the brand's other origin.** It applies to every origin of the sender: the RCS policy
  extends a revocation across all of a brand's promotional agents, and the United States rule speaks
  of a desire not to receive texts "from the caller or sender". The scope question in the single confirmation is where the person narrows it.
- **A typo, or another language.** Read as the person meant it; a doubt is settled toward stopping.
  The rule requires treating other words as revocation when a reasonable person would understand
  them so.
- **A one-way origin.** The withdrawal arrives by the alternative route the text named, and runs
  from step 2 on the same clock.
- **A reply after the platform's window closed.** It opens a new one: answer freely, and the
  conversation is `chat-and-bots`'.
- **A stop in reply to an authentication code.** It is a stop (step 6), and the provider's block does
  not read what the next message is: on Twilio every later message from your account to that number
  fails with error 21610, including the next code the person asks for. Send codes from a provider
  account of their own (`references/origin-and-standing.md`, step 3), and make the code screen answer
  error 21610 by offering the other channel and saying how to restart texts. Whether a code the person
  asks for after a stop may go is a question of basis, and `consent-and-preferences` answers it in its
  legal regime: the new request is a requested message for that one code, under the FCC's conditions
  for a one-time reply to a consumer's request, and the stop entry stays.

## Failure modes

**The provider caught the word and the record never saw it.** The sign: a number on the provider's
block list with no instruction in the record, and sends after withdrawal from a second system in
`consent-and-preferences`' join line.

**A confirmation with an offer.** The sign: the confirmation text carries a promotion. It breaks the
rule twice: promotional content, and a second message after the request.

**No confirmation at all.** The sign: repeated STOPs from one number, then blocks and reports, then
standing.

**Replies nobody reads.** The sign: windows open and close with no outbound message inside them;
questions in replies with no issue opened in `chat-and-bots`.

**Sources for the rules in this file, each opened 2026-09-15.**

- 47 CFR § 64.1200, paragraphs (a)(10) and (a)(12), eCFR edition of 2026-09-11:
  https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200
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
