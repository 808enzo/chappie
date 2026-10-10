---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Legal regimes: bot disclosure, liability and replies, quoted and dated

`SKILL.md` says which skill owns the basis for sending, names the rules below, and says what this skill
leaves to you. This file states each rule, ends it with the people it does not bind, and lists every source
it rests on at the end. This is not legal advice.

## The rules

- **California: a bot used to mislead about its artificial identity in order to sell must disclose
  it.** Section 17941 of the Business and Professions Code makes it unlawful "to use a bot to
  communicate or interact with another person in California online, with the intent to mislead the
  other person about its artificial identity for the purpose of knowingly deceiving the person about
  the content of the communication in order to incentivize a purchase or sale of goods or services in
  a commercial transaction or to influence a vote in an election", and a person using a bot is not
  liable under the section if they disclose that it is a bot. The disclosure must be "clear,
  conspicuous, and reasonably designed to inform persons with whom the bot communicates or interacts
  that it is a bot". Section 17940 defines a bot as "an automated online account where all or
  substantially all of the actions or posts of that account are not the result of a person".
  **Who this does not bind:** people outside California; a bot that discloses it is a bot;
  conversations without the intent the section describes; and, under section 17942(c), service
  providers of online platforms, including web hosting and internet service providers. Replies an agent sends from saved answers are the result of a person, which that definition
  leaves out.
- **EU: people must be told they are interacting with an AI system.** Article 50(1) of the Artificial
  Intelligence Act requires providers to "ensure that AI systems intended to interact directly with
  natural persons are designed and developed in such a way that the natural persons concerned are
  informed that they are interacting with an AI system, unless this is obvious from the point of view
  of a natural person who is reasonably well-informed, observant and circumspect, taking into account
  the circumstances and the context of use". Article 50(5) requires that information "at the latest at
  the time of the first interaction or exposure". The Act applies from 2 August 2026 under Article
  113, and the consolidated text after the 2026 amendment keeps that date for Article 50(1).
  **Who this does not bind:** a system where it is obvious to such a person that they are interacting
  with an AI system; AI systems authorized by law to detect, prevent, investigate or prosecute criminal
  offenses, unless they are available for the public to report one. Whether a scripted bot is an AI
  system under the Act, and whether you are the provider of the bot you run or only its deployer, are
  questions for counsel.
- **British Columbia: the business answered for its chatbot.** In Moffatt v. Air Canada, the Civil
  Resolution Tribunal held the airline liable for what its chatbot told a customer: "While a chatbot
  has an interactive component, it is still just a part of Air Canada's website. It should be obvious
  to Air Canada that it is responsible for all the information on its website. It makes no difference
  whether the information comes from a static page or a chatbot." The tribunal added that the airline
  did not explain "why customers should have to double-check information found in one part of its
  website on another part of its website".
  **Who this does not bind:** anyone beyond that claim. It is one tribunal's decision on one small
  claim in one Canadian province, and how far its reasoning reaches in your jurisdiction is a question
  for counsel. The operating rule this skill draws from it is its own: treat every bot answer as a
  statement by the company (`references/bot-first-line.md`, step 2).
- **UK: a reply about the person's own purchase is not direct marketing unless it carries
  promotion.** The ICO's guide to PECR says that "Routine customer service messages do not count as
  direct marketing", describing them as "correspondence with customers to provide information they
  need about a current contract or past purchase", and that "if the message includes any significant
  promotional material aimed at getting customers to buy extra products or services or to renew
  contracts that are coming to an end, that message includes marketing material and the rules apply".
  **Who this does not bind:** a reply that carries significant promotional material, which falls under
  the marketing rules; a reply to a prospect about something they have not bought, which the quoted
  guidance does not address; and every regime outside the UK, where the question goes to
  `consent-and-preferences`.

## Sources

**Sources, each opened 2026-09-12.**

- California Legislative Information, Business and Professions Code, Division 7, Part 3, Chapter 6
  (Bots), sections 17940 to 17943:
  https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?lawCode=BPC&division=7.&title=&part=3.&chapter=6.&article=
- Regulation (EU) 2024/1689 (Artificial Intelligence Act), consolidated text of 2026-07-27, Articles
  50(1), 50(5) and 113: https://eur-lex.europa.eu/eli/reg/2024/1689/2026-07-27/eng
- Civil Resolution Tribunal of British Columbia, Moffatt v. Air Canada, 2024 BCCRT 149:
  https://decisions.civilresolutionbc.ca/crt/crtd/en/item/525448/index.do
- ICO, Guide to PECR, Electronic and telephone marketing, "What is direct marketing?":
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/
