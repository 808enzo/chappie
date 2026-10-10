---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-14
---

# Legal regimes: the rules a message to a person at an organization rests on, quoted from their sources

`SKILL.md` names the regimes and what this skill leaves to you. This file quotes each rule in its primary
source's words, ends it with the people it does not bind, and lists every source it quotes at the end.
This is not legal advice.

## The rules

- **United Kingdom, ICO, "Business-to-business marketing" and the PECR electronic mail guidance.** "Corporate
  subscriber covers subscribers that are a corporate body with separate legal status," including "companies,"
  "limited liability partnerships," "Scottish partnerships," "some government bodies"; "the email address or
  telephone number of an employee at a corporate body would constitute a corporate subscriber for the purposes of
  PECR because the 'subscriber' is their employer." "Sole traders," "certain types of partnerships" and "other
  unincorporated bodies of individuals" are individual subscribers. "You can send unsolicited electronic mail
  marketing to corporate subscribers without consent or a soft opt-in. You must not disguise or hide your identity
  in messages to either type of subscriber. You must provide a valid contact address for recipients to opt out or
  unsubscribe." The ICO adds that "you should comply with a corporate subscriber's opt-out request." And: "If you
  can identify an individual either directly or indirectly it will constitute personal data even if they are
  acting in their business capacity," with "their absolute right to stop their data being used for direct
  marketing purposes"; an address such as "info@company.com" with no name is not personal data. So a work address
  of the form initials.lastname at the company's domain is a corporate subscriber under PECR and personal data
  under UK GDPR at the same time, and an objection from the person stands even where PECR asks for no consent.
  **Who this does not bind:** senders outside the United Kingdom's jurisdiction; individual subscribers, who get
  consent or the soft opt-in with all its conditions; calls and faxes, which have their own rules on the same
  page.
- **European Union, Directive 2002/58/EC, Article 13.** 13(1): electronic mail "for the purposes of direct
  marketing may be allowed only in respect of subscribers or users who have given their prior consent." 13(2): a
  natural or legal person that "obtains from its customers their electronic contact details for electronic mail,
  in the context of the sale of a product or a service" "may use these electronic contact details for direct
  marketing of its own similar products or services provided that customers clearly and distinctly are given the
  opportunity to object, free of charge and in an easy manner." 13(4): mail "which disguise or conceal the identity
  of the sender" or "which do not have a valid address to which the recipient may send a request that such
  communications cease" "shall be prohibited." **13(5): "Paragraphs 1 and 3 shall apply to subscribers who are
  natural persons. Member States shall also ensure, in the framework of Community law and applicable national
  legislation, that the legitimate interests of subscribers other than natural persons with regard to unsolicited
  communications are sufficiently protected."** The regime for an address that belongs to a legal person is set by
  the member state, so "EU" does not fold into one flag.
  **Who this does not bind:** senders outside the Union; the form of protection for legal persons, which is the
  national law's question.
- **United States, FTC, "CAN-SPAM Act: A Compliance Guide for Business."** "The law makes no exception for
  business-to-business email." The requirements: "Don't use false or misleading header information," "Don't use
  deceptive subject lines," "Identify the message as an ad," "Tell recipients where you're located," "Tell
  recipients how to opt out," "Honor opt-out requests promptly": "Any opt-out mechanism you offer must be able to
  process opt-out requests for at least 30 days after you send your message. You must honor a recipient's opt-out
  request within 10 business days." And "you can't contract away your legal responsibility to comply with the
  law." No prior consent is required.
  **Who this does not bind:** a message whose primary purpose is transactional or relationship content, which is
  `transactional-messaging`'s question; senders outside the United States for messages not sent there.
- **Canada, CRTC, "Guidance on Implied Consent."** An existing business relationship gives implied consent "for the
  period specified (either 2 years or six months following the last transaction date)": a purchase or lease, an
  accepted opportunity, or a written contract in existence or expired within two years; "an inquiry or
  application on any of the items above within the six month period immediately before the message was sent."
  Conspicuous publication of an address gives implied consent only when "there is no statement in connection with
  the address that the person does not want to receive CEMs at that address" and "the content of your CEM is
  relevant to the recipient's business, role, functions, or duties in a business or official capacity." An
  address "disclosing their email address verbally or in writing, perhaps by providing their business card at a
  tradeshow" gives implied consent on the same terms, and "the confirmation email sent may be considered a CEM."
  "The sender of a CEM has the onus of proving consent." Between organizations, "the business to business
  exemption set out in the GIC Regulations at section 3(a)(ii)" applies where the organizations have a
  relationship and the message concerns "the activities of the organization to which the message is sent."
  **Who this does not bind:** messages not sent to an electronic address; senders and recipients outside Canada.
- **European Union, GDPR, Articles 6(1)(f), 14(3) and 21(2) and (3), Recital 47.** Processing is lawful where it
  "is necessary for the purposes of the legitimate interests pursued by the controller or by a third party, except
  where such interests are overridden by the interests or fundamental rights and freedoms of the data subject";
  "The processing of personal data for direct marketing purposes may be regarded as carried out for a legitimate
  interest." Where personal data have not been obtained from the data subject, the controller provides the
  information of Article 14 "(a) within a reasonable period after obtaining the personal data, but at the latest
  within one month"; "(b) if the personal data are to be used for communication with the data subject, at the
  latest at the time of the first communication to that data subject"; "(c) if a disclosure to another recipient
  is envisaged, at the latest when the personal data are first disclosed." "Where personal data are processed for
  direct marketing purposes, the data subject shall have the right to object at any time to processing of personal
  data concerning him or her for such marketing, which includes profiling to the extent that it is related to such
  direct marketing." "Where the data subject objects to processing for direct marketing purposes, the personal data
  shall no longer be processed for such purposes." A colleague's address obtained from the champion is data not
  obtained from the data subject: the first message carries the source and the basis. The intent grade is
  profiling in the sense of Article 21(2): a contact's objection removes that contact's signals from the grade.
  **Who this does not bind:** controllers outside the Regulation's territorial scope; the exceptions of Article
  14(5), including disproportionate effort, which the reader settles with counsel.

## The cut on purchased lists

**Cut on the law.** Purchased or scraped lists of contacts at target accounts as a way to a missing role: the ICO
writes that a buyer of a list "would breach the law if they sent marketing by email to addresses belonging to
individual subscribers," because consent must be given to them as the sender; CASL gives such a list no implied
consent; Article 14 requires the source to be told. The cut stands even where cold lists are routine. Only the
four ways of `references/buying-group-and-stalls.md`, step 4, ship.

## Sources

**Sources, each opened 2026-09-14.**

- ICO, Business-to-business marketing:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/business-to-business-marketing/
- ICO, Guidance on direct marketing using electronic mail, "How do we comply with the PECR electronic mail
  marketing rules?":
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/
- EUR-Lex, Directive 2002/58/EC, consolidated text of 2009-12-19, Article 13:
  https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02002L0058-20091219
- FTC, CAN-SPAM Act: A Compliance Guide for Business:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- CRTC, Canada's Anti-Spam Legislation, Guidance on Implied Consent: https://crtc.gc.ca/eng/com500/guide.htm
- EUR-Lex, Regulation (EU) 2016/679: https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679
