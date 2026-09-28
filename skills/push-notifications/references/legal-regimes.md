---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Legal regimes: push under platform rules and marketing law, quoted and dated

`SKILL.md` says which skill owns the basis for sending, names the rules below, and says what this skill
leaves to you. This file states each rule, ends it with the people it does not bind, and lists every source
it rests on at the end. This is not legal advice.

## The rules

- **App Store: promotional pushes need their own opt-in.** Guideline 4.5.4 says push notifications
  "must not be required for the app to function, and should not be used to send sensitive personal
  or confidential information", and that they "should not be used for promotions or direct marketing
  purposes unless customers have explicitly opted in to receive them via consent language displayed
  in your app's UI, and you provide a method in your app for a user to opt out from receiving such
  messages."
  **Who this does not bind:** web push, and apps distributed outside the App Store. It is a platform
  rule that Apple enforces through review, not a statute. The Google Play ads policy, as opened on
  the same day, has no counterpart: its one sentence on notifications forbids ads that imitate them.
- **EU and UK: the marketing rule is written for "electronic mail", and push is not named.** The
  ePrivacy Directive allows direct marketing by electronic mail only to people who gave prior consent,
  and defines electronic mail as "any text, voice, sound or image message sent over a public
  communications network which can be stored in the network or in the recipient's terminal equipment
  until it is collected by the recipient". The ICO uses the same definition for PECR, says the
  electronic mail rules apply to direct messages on social media, and says PECR sets no specific
  rules for display or banner ads. Neither text names push notifications, and whether a promotional
  push falls inside the definition in your country is a question for counsel.
  **Who this does not bind:** service pushes that are not direct marketing. The marketing article
  does not reach them, whichever way the definition is read.
- **UK: the children's code switches off non-essential push by default.** The ICO's guidance says
  that where push notifications based on personal data are non-essential, "for example, encouraging
  users to return to the app after a period of inactivity", you need to turn these settings off by
  default for child users, while notifications essential to the service's core function may be on
  by default.
  **Who this does not bind:** general service notifications pushed to all users without using
  personal data to target them, which the ICO places outside the scope of the code.
- **US: the email statute is defined by an email address.** CAN-SPAM defines an electronic mail
  message as a message sent to a unique electronic mail address, and that address as a destination
  consisting of a user name or mailbox and a reference to an Internet domain. A push token is
  neither. The federal phone rules are covered in `contact-orchestration`, which records that they do
  not reach push.
  **Who this does not bind:** state law and general consumer protection law, which are not surveyed
  here.
- **Canada: whether a push endpoint is "any similar account" is open.** CASL prohibits sending a
  commercial electronic message to an electronic address without express or implied consent, and
  defines an electronic address as an address used for an electronic mail account, an instant
  messaging account, a telephone account, or any similar account. The text does not say whether a
  push endpoint is a similar account.
  **Who this does not bind:** messages that are not commercial electronic messages under the
  definition in subsection 1(2).

## Sources

**Sources, each opened 2026-09-11.**

- Apple, App Review Guidelines, guideline 4.5.4 (Push Notifications):
  https://developer.apple.com/app-store/review/guidelines/
- Google Play Console Help, Ads policy (the sentence on notifications):
  https://support.google.com/googleplay/android-developer/answer/9857753
- Directive 2002/58/EC (ePrivacy), consolidated text of 2009-12-19, Articles 2(h), 5(3) and 13(1):
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219
- ICO, Guide to PECR, Electronic mail marketing:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/
- ICO, FAQs on the 15 standards of the Children's code:
  https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/faqs-on-the-15-standards-of-the-children-s-code/
- 15 U.S.C. § 7702, paragraphs (5) and (6) (CAN-SPAM definitions):
  https://www.govinfo.gov/content/pkg/USCODE-2023-title15/html/USCODE-2023-title15-chap103-sec7702.htm
- Canada's Anti-Spam Legislation (S.C. 2010, c. 23), subsections 1(1), 1(2) and 6(1):
  https://laws-lois.justice.gc.ca/eng/acts/E-1.6/page-1.html
