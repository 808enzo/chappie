---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Legal regimes: consent, exemptions and delivery windows, stated and dated

`SKILL.md` names the baseline this skill assumes and the rules, and says which skill owns consent
capture. This file states each rule, names who a rule does not bind where it has an exemption, and
lists every source with its date at the end. This is not legal advice.

## The rules

- **EU.** Marketing email needs prior consent. The exemption for your own customers is narrow and
  carries its own conditions: you took the address in the course of a sale, you market your own similar
  goods, and you give a free and simple way to refuse both at collection and in every message after it.
  The directive runs through national law, so the shape of that exemption is not the same in every
  member state. **Who this does not bind:** a message that is not direct marketing; service and
  transactional mail stands on its own footing.
- **UK.** A separate regime, and it turns on the type of subscriber. An individual needs consent or the
  soft opt-in, and the soft opt-in carries five conditions that all have to hold: you collected the
  address yourself, you collected it during a sale or negotiations for one, you market your own similar
  goods, you offered the refusal at the point of collection, and you offer it in every message after
  that. Browsing a catalog is not a negotiation, and a refusal placed only in the order confirmation
  does not close the last two conditions. **Who this does not bind:** a corporate subscriber, for the
  consent rule only: you may send them unsolicited marketing email with neither consent nor the soft
  opt-in. Not for the rest of the regime. The ICO asks you not to hide your identity in messages to
  either type of subscriber, to give a valid contact address for opting out, and to comply with a
  corporate subscriber's opt-out request; a named work address is also personal data, and the person's
  right to object stands where PECR asks for no consent (`b2b-lifecycle` holds the quotes).
- **Frequency, in both.** Neither regime caps how many messages you send. The promise you made when you
  collected the address binds you instead: someone signed up for a weekly digest, you send daily, and
  you have undermined the basis you send on.
- **United States, email.** Commercial email runs on an opt-out model: honor the unsubscribe within the
  statutory window and carry a physical postal address. **Who this does not bind:** a message whose
  primary purpose is one of the five narrow categories of transactional and relationship message, which
  sit outside most of those requirements, and a message with neither commercial nor transactional
  content. Membership and a subscription are not on their own among the five: those categories cover
  notice about such a relationship rather than marketing to somebody who holds one. Primary purpose is
  read from the subject line and from what opens the body, so a service message with a promotional block
  can turn commercial on either.
- **United States, phone.** The federal delivery window runs from 8:00 to 21:00 in the recipient's local
  time, for telephone solicitation to a residential subscriber, and at least one state runs an hour
  tighter: Florida ends at 20:00. We have not surveyed how many others narrow it, so treat that as a
  question for your own list of states rather than a pattern. Work out the recipient's local time
  yourself: the rule puts that job on the sender. **Who this does not bind:** email and push, which the
  rule does not reach at all; and, under the federal rule, anyone who gave prior express permission or
  sits inside an established business relationship, whom the definition of telephone solicitation
  excludes. The window is therefore not a federal absolute for consented CRM sending. The Florida hour
  binds a commercial telephone seller as that statute defines one, and its exemptions are its own: the
  federal exclusions do not carry over, and we have not mapped the state's. For everything you cannot
  place inside an exclusion, litigation over these hours still makes the window the default safe
  behavior.
- **Canada.** Consent is stricter than the US model: express consent, or implied consent whose life runs
  from the event that created it. A purchase, a rental or an accepted business proposal gives two years
  from the last one; a written contract gives the time it is in force and two years after it expires; an
  inquiry or an application gives six months. The period belongs to the event, not to the regime. **Who
  this does not bind:** express consent, which does not expire and ends only with an unsubscribe.
- **Everywhere.** A service message with a promotional block added to it can stop counting as a service
  message, which costs it both the consent exemption and the exemption from the cap. Settle that before
  the banner goes in, not after the complaint.

## Sources

**Sources, with the date each was last opened.**

- FTC, *CAN-SPAM Act: A Compliance Guide for Business*, opened 2026-09-16:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- FCC, 47 CFR § 64.1200, restriction at (c)(1) and definition at (f), opened 2026-09-16:
  https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200
- Florida Statutes § 501.616(6)(a), opened 2026-09-16:
  https://www.flsenate.gov/Laws/Statutes/2026/501.616
- CRTC, *Guidance on Implied Consent*, opened 2026-09-07: https://crtc.gc.ca/eng/com500/guide.htm
- Directive 2002/58/EC as amended in 2009, article 13, opened 2026-09-07:
  https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219
- ICO, *Guidance on direct marketing using electronic mail*, opened 2026-09-16:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/
