---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Legal regimes: disclosures, corrections and the incident log, stated and dated

`SKILL.md` names the baseline this skill assumes and the rules. This file states each rule, ends it
with the people it does not bind, and lists every source with its date at the end. This is not legal
advice.

## The rules

- **EU, a disclosure through message content.** Somebody else's name, order or balance shown to a
  recipient is a personal data breach: the GDPR defines one as "a breach of security leading to the
  accidental or unlawful destruction, loss, alteration, unauthorised disclosure of, or access to,
  personal data transmitted, stored or otherwise processed" (Article 4(12)). The controller "shall
  without undue delay and, where feasible, not later than 72 hours after having become aware of it,
  notify the personal data breach to the supervisory authority", and a later notification carries
  "reasons for the delay" (Article 33(1)). When the breach "is likely to result in a high risk to the
  rights and freedoms of natural persons", it goes to the people affected as well (Article 34(1)).
  The clock is the regulation's, and the procedure belongs to whoever owns privacy where you work;
  the severity route in `references/incident-response.md` exists to reach that person inside it.
  **Who this does not bind:** a breach "unlikely to result in a risk to the rights and freedoms of
  natural persons" is not notified to the authority, and it is still documented, because the
  controller "shall document any personal data breaches, comprising the facts relating to the
  personal data breach, its effects and the remedial action taken" (Article 33(5)). The UK version
  of these articles has been amended since 2020 and was not opened here.
- **EU and UK, sending without a basis.** Sending to people you held no basis for is a
  lawful-basis question, and `consent-and-preferences` quotes the articles that answer it. What this skill
  keeps is operational: capture who was affected and when, because every later answer starts from
  that list. **Who this does not bind:** people who held a basis for the message that went out, for
  whom the fault is late, duplicated or wrong content rather than a question of basis.
- **United States, a correction by email.** What the correction contains decides which rules it
  falls under. A message with both commercial and transactional or relationship content is
  commercial when a recipient reading the subject line would likely conclude it advertises, or when
  the transactional content does not appear "in whole or in substantial part, at the beginning of
  the body of the message" (16 CFR 316.3(a)(2), quoted in full with its address in
  `transactional-messaging`, opened 2026-09-13). Add an offer to the apology and lead with it, or name it in
  the subject line, and the correction takes on the requirements of commercial mail, the unsubscribe among them. **Who
  this does not bind:** channels other than email, whose rules this skill does not survey.
- **Canada, a correction as an electronic message.** CASL's consent exemption holds only for a
  commercial electronic message that "solely" does one of the things section 6(6) lists, such as
  confirming a transaction the person agreed to, and the sender identification, contact details
  and unsubscribe mechanism stay required (`transactional-messaging` quotes the section, opened
  2026-09-13). A correction that adds an offer is no longer solely a service message, and it does
  not restore a basis that was never there. **Who this does not bind:** messages that are not
  commercial electronic messages at all, which is a question for counsel about your own messages.
- **EU, the incident log.** Incident logs and exports of affected people are personal data, so the
  GDPR's purpose limitation and storage limitation principles in Article 5(1)(b) and (e) apply to
  them (`consent-and-preferences` quotes both, opened 2026-09-14). Keeping them indefinitely in case
  they turn out useful is itself a decision you have to defend. **Who this does not bind:** counts
  and fault records kept in a form that identifies nobody, since storage limitation reaches only
  data "kept in a form which permits identification of data subjects"; and regimes outside the EU and UK, whose retention rules
  this skill does not survey.

## Sources

**Sources, each opened 2026-09-16.**

- Regulation (EU) 2016/679 (GDPR), Articles 4(12), 33 and 34:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679

16 CFR 316.3 and CASL section 6(6) are quoted, with their addresses, in `transactional-messaging`;
GDPR Article 5(1) in `consent-and-preferences`.
