---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The origin and its standing

The unit here is **the origin**: a registered number or name a message leaves from. A ten-digit
number under its registered campaign, a short code, a toll-free number, an alphanumeric sender ID, a
WhatsApp business phone number inside its portfolio, an RCS agent. The gatekeeper forms its opinion
about origins, not about companies: a carrier scores the registered campaign and the number, a
messaging platform scores the template and the number and caps the portfolio. This file decides which
origins exist, what each carries, how a new one earns its limit, what you read about it every day, and
what you do when its standing drops.

## Entry conditions

The program is going to send texts or messaging app messages in at least one country. You know which
classes it will send (marketing, service, authentication codes, replies) and to which
countries. The basis for texting each person is a record in `consent-and-preferences`; nothing here
grants one.

## Exit conditions

A register of origins: country, platform, type, the classes that leave from it, registration state,
current standing and limit, the date of the last reading. The rule that assigns classes to origins,
written down with the question that decided it. A ramp for every new origin. A reaction to a drop in
standing, with an owner.

## Steps

**1. Inventory every origin, by country and class.** What texts and messaging app messages leave
from today, and from where: the marketing platform, the order system, the authentication provider,
the sales platform, the support desk, a manager's own phone. Each is an origin, registered or not. An
unregistered one is still an origin the gatekeeper scores; it is not exempt because nobody wrote it
down.

**2. Register each origin with its gatekeeper.** United States, texts: A2P 10DLC, a brand and a
registered campaign per use case, which carries the opt-in description, the opt-out and help texts and
sample messages; a short code under the Common Short Code program, and a toll-free number under its
own program, whose rules are left to you. Unregistered traffic from a ten-digit number draws
additional carrier fees; what a carrier does with it beyond the fee is what your provider reports. WhatsApp: a business portfolio, a
phone number, business verification. Newly created portfolios have a messaging limit of 250 unique
recipients outside a reply window in a moving 24 hour period, and it rises to 2,000 with business
verification or with 2,000 messages delivered outside reply windows to unique numbers in a 30 day
moving period using templates with a high quality rating. The limit belongs to the portfolio and every
number in it spends the same limit. RCS: an agent, verified and launched. Alphanumeric sender IDs: the
registration rules differ by country and are left to you, and the ID cannot receive a reply. Under the
United States rule, a texting protocol that does not allow reply texts obliges the sender to put on
each text a clear disclosure that two-way texting is not available and a reasonable alternative way to
revoke consent (47 CFR 64.1200(a)(10); the rule and its boundary are in `SKILL.md`). A one-way origin
therefore carries that line in every text and an opt-out route that works without a reply.

**3. Split the classes across origins, and write down the question that decided it.** Ask of every
place where the gatekeeper keeps standing: **what would a pause, a filter or a spent limit caused by
marketing take down?** A carrier scores the registered campaign and its numbers: if authentication
codes or the service lines the law requires (`transactional-messaging`) leave under the same registered
campaign as marketing, marketing gets an origin of its own, a ten-digit number under a separate
registered campaign or a short code of its own. A messaging platform keeps standing on three levels,
and a separate number answers only one of them. Each template carries its own quality rating and
pauses, so a service line never shares a template with marketing, and a template with mixed content is
marketing anyway (`references/send-and-cost.md`, step 1). The number's own rating and status are what
a separate number protects; this skill leaves that page to you. The messaging limit belongs to the
portfolio, every number in it spends the same limit, and the platform rate-limits a business whose
quality stays low: marketing from any number spends the limit the service templates need that day. So
pace marketing under a reservation for the service lines' daily peak of recipients outside a window
(`references/send-and-cost.md`, step 9). The split is by class, not by volume: one class, one origin per
country. Spreading the same traffic across many numbers is snowshoeing, which the carriers' principles
tell senders not to use, and a shared short code needs an arrangement with the provider and shares its
standing with everyone on it. To the carriers' principles, an opt-in applies only to the campaign and
the sender it was obtained for, and does not transfer.

**4. Ramp a new origin by audience, not by volume.** The first sends go to people who wrote to you
first, so that the window is open and the reply is theirs, and to recent buyers as service lines. The
next tier is released by the previous tier's signals, not by the calendar: stop keywords, blocks,
template quality. The principle is the one `deliverability` applies to a new sending identity: each
step is released by the previous step's signals, here the gatekeeper's rather than a mailbox
provider's. On WhatsApp the first tier inside open windows makes no progress toward the limit: only
messages delivered outside a reply window count toward the 2,000 that a new portfolio needs to raise
its limit without verification, and a free-form reply gives no template a rating. The service lines to recent buyers,
sent as templates outside a window, are the tier that counts. Above 2,000 the limit rises on its own:
when the portfolio has used at least half of its current limit in the last 7 days with
high-quality messaging across all numbers and templates, the limit rises one level within 6 hours,
through 10,000 and 100,000 to unlimited. No such published ladder exists for a carrier, so the audience
sets the volume there: send to the tier that answered without complaint, and widen when the register in
step 5 stays clean.

**5. Keep a standing register, read daily, one row per origin.** What to read: the messaging limit
and the share of it used; the quality rating of every template (GREEN, YELLOW, RED, or UNKNOWN on a
new template until the platform has signals); pauses, with the count of pauses on that template;
refusals with the per-user marketing limit code (131049); carrier errors by class (filtered, invalid
number); stop keywords received that day, by template or registered campaign; blocks, where the
platform reports them. Take the pause and status changes from the platform's webhook
(`message_template_status_update`) rather than from a daily poll: a template can be paused and
resumed between two polls, and the sends in between were refused.

**6. React to a drop in this order.** (a) Pause marketing where the drop sits: the marketing template
if the drop is on the template, and marketing across the portfolio if the platform rate-limits the
business or restricts the number, so that the service templates keep the limit. (b) Read the last
period's sends by template: which template drew the stops and the blocks, and to whom it went. (c)
Check that the template carries an exit (a stop button or a "reply STOP" line) and that its category
matches its content. (d) Fix with a new template, never by resubmitting the same text: the first pause
is 3 hours, the second 6 hours, the third disables the template. (e) Resume on the ladder of step 4,
from the audience that answered.

**7. Keep the numbers clean.** Process the carriers' deactivation files regularly, daily where your
provider supplies them: a number that left service will be reassigned to somebody else, so the record
loses it now. A refusal for an invalid or deactivated number is a loss event for
`contact-orchestration` and a change to the record in `consent-and-preferences`, not a retry.

**8. When you move to another provider, move the block list first.** The provider's list of numbers
that replied STOP is its own and lives in your account with that provider; the record is yours. Before
the move, compare the two: a number on the provider's list with no instruction in the record is a stop
the record never received, and a migration that leaves the list behind texts every such number after
the withdrawal, which `consent-and-preferences` counts. Carry the registered campaigns, the templates and the keyword
table across with it, and treat the new origin as new for the ramp.

## Thresholds and timings

| Quantity | Value | Where it comes from |
|---|---|---|
| WhatsApp messaging limit of a new portfolio | 250 unique recipients outside a reply window per moving 24 hours | platform rule, Meta |
| Rise to 2,000 | business verification, or 2,000 messages delivered outside reply windows to unique numbers within a 30 day moving period, with templates rated high | platform rule, Meta |
| Who spends the limit | every number in the portfolio | platform rule, Meta |
| Rise above 2,000 | at least half of the current limit used in the last 7 days with high-quality messaging, then one level up within 6 hours: 10,000, 100,000, unlimited | platform rule, Meta |
| Template pause at the lowest quality | 3 hours, then 6 hours, then disabled; attempts are rejected and not charged | platform rule, Meta |
| Per-user marketing limit | refusal code 131049; do not retry for at least 24 hours | platform rule, Meta |
| Deactivation files | processed regularly, "e.g., daily" | industry principle, CTIA 5.1.5 |
| The tier of the ramp | the audience of the previous tier that answered without complaint | yours |
| Reservation for service lines on a shared limit | the service templates' daily peak of unique recipients outside a window, over your last full cycle | yours |
| What the register reads | step 5 | this file |

The platform and industry rows are class 2 and carry their sources below; the boundary of each is in
`SKILL.md`. The last three are yours.

## Edge cases

- **A second brand in the same portfolio.** The messaging limit belongs to the portfolio; each
  template carries its own rating. Give the second brand its own number and its own templates. The two
  brands still spend one limit, so split the day's limit between them in writing, the service lines of
  both first, and read the share each brand used in the register.
- **An alphanumeric ID in one country and a number in another.** The register is by country. The
  one-way origin carries the disclosure and the alternative route from step 2 on every text; the
  two-way origin carries the keywords (`references/keywords-and-replies.md`).
- **A template disabled in the middle of a campaign.** The rest of the campaign does not go out with
  that template or with a copy of its text. A new template goes out after step 6 (b) and (c), and only
  to the audience that would let it keep its rating.
- **A shared short code.** The standing is shared: a drop caused by another sender on the code reads
  as yours. The arrangement with the provider decides what you can read about the others; if it
  reads nothing, the code carries nothing you cannot afford to lose.
- **A manager's own phone.** It is an origin without registration. Its messages do not travel
  through the program and are not counted here, but a STOP said to it is a withdrawal for the record
  (`consent-and-preferences`), and `b2b-retention` decides who writes in which stage.

## Failure modes

**The service line went silent because of marketing's standing.** The sign: a rise in "where is my
order" contacts (`transactional-messaging` reads them as chases) alongside refusals on the service line,
for a pause, a filter or the day's limit, in a period when marketing drew stops or spent the day's
limit before the service line ran. Step 3 was skipped, or answered with a separate number while the service line kept sharing the
limit or a template.

**The limit has sat at 250 for months.** The sign: deliveries outside a window stop at 250 people a day
while the base is larger. The business was never verified, and the other route never completes: its
2,000 unique numbers take at least eight days of 250 different people each, on templates rated high,
and a daily send that starts from the top of the same list reaches the same 250 people every day.

**The carrier bills for unregistered traffic.** The sign: a fee line in the provider's invoice. Step
2 was skipped, or a new number was added without a registered campaign.

**Standing dropped after an import.** The sign: stops and blocks concentrated among people with no
event in the window, or with a basis dated the day of an import. A rented or shared list, which the
carriers' principles rule out, or a list whose basis does not cover this channel.

**Sources for the platform and industry rules in this file, each opened 2026-09-15.**

- Meta, WhatsApp Business Platform, Messaging limits (250, 2,000, the 30 day and 7 day criteria, one
  level within 6 hours, one limit per portfolio shared by its numbers):
  https://developers.facebook.com/docs/whatsapp/messaging-limits
- Meta, WhatsApp Business Platform, Getting opt-in (rate limiting of a business whose quality stays
  low): https://developers.facebook.com/docs/whatsapp/overview/getting-opt-in
- Meta, Template quality rating (GREEN, YELLOW, RED, UNKNOWN):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-quality
- Meta, Template pausing (3 hours, 6 hours, disabled; attempts rejected and not charged; the webhook):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pausing
- Meta, Per-user marketing template message limits (code 131049, 24 hours):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/marketing-templates/per-user-limits
- Twilio, A2P 10DLC (brand and campaign registration, fees for unregistered traffic):
  https://www.twilio.com/docs/messaging/compliance/a2p-10dlc
- CTIA, Messaging Principles and Best Practices, May 2023, sections 5.1.2.2, 5.1.4, 5.1.5, 5.5.1, 5.5.2:
  https://api.ctia.org/wp-content/uploads/2023/05/230523-CTIA-Messaging-Principles-and-Best-Practices-FINAL.pdf
- 47 CFR § 64.1200(a)(10), the one-way protocol disclosure, eCFR edition of 2026-09-11:
  https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200
- Twilio, Advanced Opt-Out (the list of blocked numbers; later messages from your account fail):
  https://www.twilio.com/docs/messaging/tutorials/advanced-opt-out
