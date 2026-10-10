---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Legal regimes: displays, the device and the store, quoted and dated

`SKILL.md` says which skill owns the basis for marketing, names the rules below, and says what this skill
leaves to you. This file states each rule, ends it with the people it does not bind, and lists every source
it rests on at the end. This is not legal advice.

## The rules

- **The marketing message rules are written for "electronic mail", and a display inside the product
  is not named in them; the notification center is where the definition comes closest.** Directive
  2002/58/EC, Article 2(h), defines electronic mail as "any text, voice, sound or image message sent
  over a public communications network which can be stored in the network or in the recipient's
  terminal equipment until it is collected by the recipient". The ICO uses the same definition for
  PECR, applies the electronic mail rules to direct messages on social media, and says that "PECR do
  not set out specific rules on other types of online marketing such as display or banner ads",
  pointing to the rules on cookies instead. A modal does not fit the definition; an item in a
  notification center, stored on the device until the person opens it, is a question for counsel in
  your country.
  **Who this does not bind:** displays that are not direct marketing: service, mandatory notices,
  guidance.
- **Storing and reading on the device: Article 5(3) of the ePrivacy Directive.** The layer that
  decides displays reads identifiers and stores state on the device. Storing information, or gaining
  access to information already stored, in the terminal equipment "is only allowed on condition that
  the subscriber or user concerned has given his or her consent, having been provided with clear and
  comprehensive information", except for what is "strictly necessary in order for the provider of an
  information society service explicitly requested by the subscriber or user to provide the
  service". In the UK the same question sits under the ICO's rules on cookies and similar
  technologies.
  **Who this does not bind:** storage strictly necessary for the requested service: session state,
  the person's own settings.
- **California: a discount for personal data is a financial incentive.** Cal. Civ. Code
  §1798.125(b): a business may offer financial incentives for the collection, sale, sharing or
  retention of personal information; it has to notify consumers of them under §1798.130; it may enter
  a consumer into such a program "only if the consumer gives the business prior opt-in consent ...
  that clearly describes the material terms of the financial incentive program, and which may be
  revoked by the consumer at any time"; "if a consumer refuses to provide opt-in consent, then the
  business shall wait for at least 12 months before next requesting that the consumer provide opt-in
  consent"; and it "shall not use financial incentive practices that are unjust, unreasonable,
  coercive, or usurious in nature". A birthday-for-a-discount ask inside the app is this case.
  **Who this does not bind:** businesses below the CCPA thresholds; residents of other states, whose
  laws are not surveyed here; asks that offer nothing in return.
- **UK: standard 13 of the children's code, nudge techniques.** "Do not use nudge techniques to
  lead or encourage children to provide unnecessary personal data or turn off privacy protections."
  Nudge techniques are "design features which lead or encourage users to follow the designer's
  preferred paths in the user's decision making", and the code tells you to use pro-privacy nudges
  where appropriate. The code applies to "information society services likely to be accessed by
  children" in the UK, and "it is not restricted to services specifically directed at children":
  a retail app adults and teenagers both use is in scope.
  **Who this does not bind:** services not likely to be accessed by children in the UK; nudges
  toward privacy protection and wellbeing.
- **Platform rules on the store rating request.** Apple's App Review Guidelines, 5.6.1: "Use the
  provided API to prompt users to review your app; this functionality allows customers to provide an
  App Store rating and review without the inconvenience of leaving your app, and we will disallow
  custom review prompts." 3.2.2(x): "Apps must not force users to rate the app, review the app,
  download other apps, or other store-related actions in order to access functionality, content, or
  use of the app." Apple's StoreKit documentation: "the system displays the review prompt to a user a
  maximum of three times within a 365-day period", people "can disable requests for reviews from
  ever appearing on their device", and the request should not come at launch or "as the result of a
  user action". Google Play's In-App Reviews API: the app "shouldn't ask the user any questions before
  or while presenting the rating button or card, including questions about their opinion (such as
  'Do you like the app?')"; Google Play "enforces a time-bound quota on how often a user can be shown
  the review dialog", the quota "is subject to change", and there should be no call-to-action button
  of your own that triggers the flow; the card is surfaced as is and not removed programmatically.
  **Who this does not bind:** web products; apps distributed outside the stores; a link to the store
  page that the person opens on their own.
- **App Store guideline 4.5.4** puts the consent language for promotional push in the app's
  interface; the pre-permission screen displayed here carries it, and the rule is
  `push-notifications`'s.
  **Who this does not bind:** web push, and apps distributed outside the App Store; it is a
  platform rule enforced through review, not a statute.

## Sources

**Sources, each opened 2026-09-13.**

- Apple, App Review Guidelines, 5.6.1 App Store Reviews, 3.2.2(x), 4.5.4:
  https://developer.apple.com/app-store/review/guidelines/
- Apple Developer Documentation, StoreKit, Requesting App Store reviews:
  https://developer.apple.com/documentation/storekit/requesting-app-store-reviews
- Google Play In-App Reviews API, When to request an in-app review, Design guidelines, Quotas:
  https://developer.android.com/guide/playcore/in-app-review
- Directive 2002/58/EC (ePrivacy), consolidated text of 2009-12-19, Articles 2(h) and 5(3):
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219
- ICO, Guide to PECR, Electronic mail marketing:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guide-to-pecr/electronic-and-telephone-marketing/electronic-mail-marketing/
- ICO, Age appropriate design code, Services covered by this code:
  https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/age-appropriate-design-a-code-of-practice-for-online-services/services-covered-by-this-code/
- ICO, Age appropriate design code, standard 13, Nudge techniques:
  https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/age-appropriate-design-a-code-of-practice-for-online-services/13-nudge-techniques/
- California Civil Code §1798.125:
  https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1798.125.
