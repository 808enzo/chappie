---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# Legal regimes: the rules a reminder to buy again rests on, quoted from their sources

`SKILL.md` names the regimes and what this skill leaves to you. This file quotes each rule in its primary
source's words, ends it with the people it does not bind, and lists every source it quotes at the end.
This is not legal advice.

## The rules

- **US, commercial email: no prior consent is required, and the exemption for service messages does
  not reach this far.** Most of the requirements are lifted for a narrow set of transactional or
  relationship categories, the first of which covers a message that facilitates, completes or
  confirms a transaction the recipient has already agreed to. A message saying it is time to buy
  again does not describe a transaction already agreed; it proposes a new one, which leaves it
  commercial email with the truthful header, subject line, advertisement identification, physical
  address and opt out that go with it. The opt out is honored within ten business days and the
  mechanism keeps working for at least thirty days after the message goes.
  **Who this does not bind:** those transactional and relationship categories themselves, so an
  order confirmation or a delivery status about a transaction already agreed stays service even
  when it names the same item; and any channel other than email, since a message to a mobile number
  and a call sit under other US regimes with their own consent rules.
- **EU: the existing customer exception is the one this mechanic sits inside, so its edge is the
  one you touch.** Where a seller obtains electronic contact details from its
  customers in the context of the sale of a product or a service, it may use them for direct
  marketing of **its own similar** products or services, provided customers are clearly and
  distinctly given the opportunity to object, free of charge and in an easy manner, at the time of
  collection and on the occasion of each message. A reminder about the same consumable is the
  textbook case of "own similar". An add on reaching into a distant category is a question, and it
  is a question to ask before sending rather than after.
  **Who this does not bind:** somebody who never bought, since a registration without a sale does
  not meet that wording; and the directive is implemented in national law, so the shape and the
  edges of the exception differ by country. The rule is written for electronic mail and does not
  name push; the definition and the open question are in `push-notifications`.
- **UK: the soft opt in needs all five of its conditions, and the one this mechanic puts at risk
  is the collection condition.** The products and services soft opt in requires that you obtained the contact
  details yourself, did so while selling or negotiating to sell, market only your own similar
  products and services, offered an opt out when you collected the details, and offer one in every
  subsequent message. The temptation in this skill is to hang the reminder off the order
  confirmation; an opt out offered in an order confirmation does not satisfy the collection
  condition, and the regulator gives that exact case as bad practice.
  **Who this does not bind:** corporate subscribers, to whom unsolicited electronic mail marketing
  may be sent without consent and without a soft opt in; and the second soft opt in, the charitable
  purposes one, which covers different content, is open only to charities, and does not extend to
  products and services even for them. The electronic mail rules do not name push; the open
  question is in `push-notifications`.
- **Canada: the interval can outlive the basis for sending.** Implied consent from an existing
  business relationship runs for **two years** from a purchase or lease of goods, services or land,
  from an accepted business, investment or gaming opportunity, or from a written contract still in
  existence or expired within that period, and for **six months** from an inquiry or application,
  counted to the day the message is sent. A category bought once every two or three years produces
  a reminder date by which the basis has already lapsed: the model computed correctly and you may
  not send on it.
  **Who this does not bind:** express consent, which is not time limited and ends only when the
  recipient says so; and each new qualifying transaction restarts the period, so a second purchase
  inside the term extends the basis. Whether a push endpoint is a "similar account" under the Act
  is open; the definition is in `push-notifications`.

## Sources

**Sources, each opened 2026-09-10.**

- FTC, CAN-SPAM Act: A Compliance Guide for Business:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- Directive 2002/58/EC (ePrivacy), consolidated text of 2009, Article 13(2):
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219
- ICO, Guidance on direct marketing using electronic mail, "How do we comply with the PECR
  electronic mail marketing rules?", sections on the soft opt ins and on subscriber type:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/
- CRTC, Guidance on Implied Consent, section "What is an existing business relationship (EBR)?":
  https://crtc.gc.ca/eng/com500/guide.htm
