---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Legal regimes: consent, exemptions and deletion for event-fired flows, stated and dated

`SKILL.md` names the baseline this skill assumes and the rules. This file states each rule, ends it
with the people it does not bind, and lists every source with its date at the end. This is not legal
advice.

## The rules

- **EU.** Consent before the first send. The exception for your own customers is narrow and
  conditional: you took the address during a sale, you market your own similar goods, and you
  offer a free and simple refusal at collection and in every message after it. The directive runs
  through national law, so the exception is not identical in every member state. **Who this does
  not bind:** a message that is not direct marketing; service and transactional mail stands on its
  own footing.
- **UK.** A separate regime, and it turns on the type of subscriber. An individual needs consent
  or the soft opt-in, which carries five conditions that all have to hold. Browsing your site is not
  negotiating a sale, so a browse trigger does not create a soft opt-in. **Who this does not
  bind:** a corporate subscriber, for the consent rule only: you may send them unsolicited marketing
  email with neither consent nor the soft opt-in. Not for the rest of the regime. The ICO asks you
  not to hide your identity in messages to either type of subscriber, to give a valid contact
  address for opting out, and to comply with a corporate subscriber's opt-out request; a named work
  address is also personal data, and the person's right to object, including to the profiling behind
  a trigger, stands where PECR asks for no consent (`b2b-lifecycle` holds the quotes).
- **EU and UK, on what set the message off.** Treat a requested notification separately: "tell me
  when this is back in stock" is a request for one specific message, not consent to a program, and
  an address collected that way does not move into the regular list without its own basis. In the
  UK that request makes the notification solicited, so it needs neither consent nor the soft
  opt-in. A behavioral trigger is profiling for direct marketing, and the person may object to it
  at any time. An attribute that reveals special category data stays special category when you
  infer it from behavior: every category Article 9(1) of the GDPR lists, meaning racial or ethnic
  origin, political opinions, religious or philosophical beliefs, trade union membership, genetic
  data, biometric data used to identify a person, health, sex life and sexual orientation. A browse
  trigger in a pharmacy catalog is the standard example, and naming the flow after something else
  changes nothing. `consent-and-preferences` quotes Articles 9(1) and 21 and gives the test for a
  proxy. **Who this does not bind:** a person who also holds a marketing state for this channel and
  brand, who may receive the program beside the notification, and a trigger built on events that
  reveal none of those categories.
- **United States.** The rules apply whatever set the message off: you honor an opt-out within ten
  business days, and every message carries your valid physical postal address. The CAN-SPAM Act
  dictates both, not practice. A trigger does not move a message out of the commercial class, and
  neither does the recipient being a member or a subscriber. **Who this does not bind:** a message
  whose primary purpose is one of the five categories of transactional or relationship message,
  and a message with neither commercial nor transactional content. An order status message that
  picks up a promotional block becomes commercial when its subject line reads as a promotion or
  when the transactional content no longer opens the body; `transactional-messaging` quotes the
  rule.
- **Canada.** Express or implied consent, and implied consent from a business relationship has a
  clock: two years from a purchase, a lease or an accepted business opportunity; for a written
  contract, while it is in force and for two years after it expires; six months from an inquiry or
  an application. CASL sets these periods. Browsing is not on that list, so a browse trigger
  neither creates implied consent nor restarts its clock. **Who this does not bind:** express
  consent, which does not expire and ends only with an unsubscribe.
- **A child's birthday.** A flow built on a child's birthday holds the parent's data about a minor,
  on the parent's declared purpose: it produces the parent's message and no profile of the child
  (`consent-and-preferences`). Name the basis and the retention period for it separately. **Who
  this does not bind:** an adult's own date of birth.
- **Wherever a deletion right applies, it reaches a flow already in progress.** The request removes
  the person from the queued steps, not only from the list. `consent-and-preferences` owns the
  erasure route and the suppression entry that survives it. **Who this does not bind:** data the
  regime lets or requires you to keep, and people no deletion right reaches.

## Sources

**Sources.**

- FTC, *CAN-SPAM Act: A Compliance Guide for Business*, opened 2026-09-16:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- CRTC, *Guidance on Implied Consent*, opened 2026-09-07:
  https://crtc.gc.ca/eng/com500/guide.htm
- Directive 2002/58/EC as amended in 2009, article 13, opened 2026-09-07:
  https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219
- ICO, *Guidance on direct marketing using electronic mail*, opened 2026-09-16:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/

Articles 9(1) and 21 of the GDPR are quoted, with their addresses and dates, in
`consent-and-preferences`; 16 CFR 316.3 in `transactional-messaging`.
