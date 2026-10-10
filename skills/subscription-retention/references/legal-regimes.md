---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Legal regimes: the rules a notice, a retry and an exit rest on, quoted from their sources

`SKILL.md` names the regimes and what this skill leaves to you. This file quotes each rule in its primary
source's words, ends it with the people it does not bind, and lists every source it quotes at the end. Seven
rules, each with the boundary it does not cross. Every quotation comes from a page opened on 2026-09-15. This
is not legal advice.

## The rules

- **United States, federal: ROSCA, 15 U.S.C. § 8403.** It is unlawful "to charge or attempt to charge any
  consumer for any goods or services sold in a transaction effected on the Internet through a negative
  option feature" unless the seller "provides text that clearly and conspicuously discloses all material
  terms of the transaction before obtaining the consumer's billing information", "obtains a consumer's
  express informed consent before charging", and "provides simple mechanisms for a consumer to stop
  recurring charges". The FTC's amended Negative Option Rule of 2024 was vacated: the Commission's own
  notice records that "On July 8, 2025, shortly before businesses would need to comply with all parts of
  the Rule, the United States Court of Appeals for the Eighth Circuit vacated the amended Rule", and on
  March 11, 2026 the FTC opened an advance notice of proposed rulemaking on amendments to its "Rule
  Concerning the Use of Prenotification Negative Option Plans" (16 CFR part 425). On the day these pages
  were opened, the federal law for online subscriptions was ROSCA and section 5 of the FTC Act; the 1973
  rule covers prenotification plans.
  **Who this does not bind:** transactions not effected on the Internet; the content of "simple
  mechanisms" is set by FTC practice, not by the statute's text; state law is a separate layer, and a
  new federal rule may follow the 2026 rulemaking, so open the FTC's page again before you build.
- **California: Business and Professions Code §§ 17600 to 17606, as amended by AB 2863.** Before
  the charge: the offer terms "in a clear and conspicuous manner", the consumer's "express affirmative
  consent", an acknowledgment "capable of being retained by the consumer", verification of consent kept
  "for at least three years, or one year after the contract is terminated, whichever period is longer".
  Notices: for a free gift or trial "lasting for more than 31 days" or a promotional price that applied
  "more than 31 days", a notice "at least 3 days before and at most 21 days before the expiration" of that
  period; for an initial term "of one year or longer", a notice "at least 15 days and not more than 45
  days before" the renewal; the notice states that the service "will automatically renew unless the
  consumer cancels", the length of the renewal period, "the amount or range of costs", "one or more
  methods by which a consumer can cancel", and, if electronic, "a link that directs the consumer to the
  cancellation process". A fee change: "no less than 7 days and no more than 30 days before the fee change
  takes effect". An annual reminder under an annual agreement, "in the same medium that resulted in the
  activation", disclosing the product, "the frequency and amount of charges" and "the means to cancel".
  The exit: a business that lets a consumer accept online "shall allow a consumer to terminate the
  automatic renewal or continuous service exclusively online, at will, and without engaging any further
  steps that obstruct or delay"; a discount or retention benefit is "not considered an obstruction or
  delay, provided that the consumer remains able to cancel", which online means the business
  "simultaneously displays a prominently located and continuously and proximately displayed direct link
  or button entitled 'click to cancel,' or words to that effect"; by telephone the business "first clearly
  and conspicuously informs the consumer that they may complete the cancellation process at any time by
  stating that they want to 'cancel'"; a voicemail is answered "within one business day"; cancellation
  is available "in the same medium that the consumer used in the transaction". Section 17601(b): the
  amendments "shall only apply to a contract entered into, amended, or extended under this article on or
  after July 1, 2025."
  **Who this does not bind:** the article speaks of "a consumer in this state", and "consumer" means an
  individual acquiring goods or services "for personal, family, or household purposes": people outside
  California and business customers are outside it. Other states have automatic renewal laws of their
  own, not surveyed here.
- **Card networks: Visa, two rules.** The subscription merchant policy (article AI09067, effective
  April 18, 2020) requires, at enrollment, "an electronic copy (i.e., email or SMS / text, if agreed with
  the cardholder) of the terms and conditions of the subscription service", "even if no amount was due at
  the time", carrying confirmation of the subscription, the start date, the goods, "ongoing transaction
  amount and billing frequency / date" and a "link or other simple mechanism to enable the cardholder to
  easily cancel"; "an electronic reminder notification (i.e., email or SMS / text) a link to online
  cancellation at least seven (7) days before initiating a recurring transaction if" a trial or
  promotional period "has expired" or "the nature of the recurring agreement has changed (for example, the
  price or billing period)"; and "an easy way to cancel the subscription or payment method online,
  regardless of how the cardholder initially interacted with the merchant", with ease "similar to
  'unsubscribing' from an email distribution list". The resubmission rule (article AI10325, effective
  April 17, 2021): when a "Category 1 (Issuer will never approve) decline code is used, the merchant is
  not permitted to reattempt the transaction"; Category 2, "Issuer cannot approve at this time", allows
  merchants "to reattempt up to 15 times in 30 days"; after response code 14, "Merchants must not
  reattempt any transaction using the same account number".
  **Who this does not bind:** other networks, which have rules of their own; a network rule reaches you
  through your acquirer's agreement, not as a statute, and the full Visa Core Rules were not opened.
- **Card networks: Mastercard, read through one acquirer's developer documentation.** J.P. Morgan
  Payments lists the merchant advice codes: code 03 "Do not try again. Obtain another type of payment from
  consumer."; code 21 "Do not try again. Issuer has blocked recurring payment transaction"; codes 24 to 30
  "Retry after 1 hour", "Retry after 24 hours", "Retry after 2 days", "Retry after 4 days", "Retry after 6
  days", "Retry after 8 days", "Retry after 10 days".
  **Who this does not bind:** this is an acquirer's rendering, not Mastercard's text, which did not open;
  Mastercard's own reattempt ceiling and its fees come from your acquirer.
- **Germany: BGB § 309 no. 9 and § 312k** (German text; the rendering below is our own, so nothing in
  it is a quotation except the German labels). Under § 309 no. 9, in a contract for the regular delivery
  of goods or the regular provision of services, standard terms are void if they bind the customer to an
  initial term longer than two years, to a tacit extension of a fixed length (an extension is allowed only
  for an indefinite period with a right to terminate at any time on at most one month's notice), or to a
  notice period longer than one month before the end of the initial term. Under § 312k, a consumer
  contract concluded through a website that creates a continuing obligation against payment has to be
  terminable through a cancellation button labeled with nothing other than "Verträge hier kündigen" (cancel
  contracts here) or an equally unambiguous wording, leading directly to a confirmation page with fields
  for the kind of termination, the consumer's identification, the contract, the date on which the
  termination is to take effect and an address for the confirmation, and a confirmation button labeled
  "jetzt kündigen" (cancel now); the buttons and the page have to be permanently available and directly
  and easily reachable; the trader confirms the content, the date and time of receipt and the end date at
  once, electronically, in text form; where the buttons and the page are missing, the consumer may
  terminate at any time without a notice period.
  **Who this does not bind:** consumers outside Germany; contracts whose termination the law subjects to
  a form stricter than text form; financial services; business customers, whom § 312k does not address.
  The European directive behind the member-state text (Directive 2011/83/EU, amended by Directive (EU)
  2023/2673 with a withdrawal function) did not open on the day these pages were checked and is left to
  you.
- **United Kingdom: Digital Markets, Competition and Consumers Act 2024, Part 4 Chapter 2, sections
  253 to 281, not yet in force.** Section 258: the trader "must give to the consumer a notice (referred
  to in this Chapter as a 'reminder notice') in respect of each renewal payment that relates to the end of
  a relevant six-month period", and where the contract includes a concessionary period, in respect of "the
  first renewal payment for which the consumer will become liable". Section 260: arrangements to end the
  contract "in a way which is straightforward" and "without having to take any steps which are not
  reasonably necessary", and for a contract entered into online, arrangements that "enable a consumer to
  bring the contract to an end online" with instructions "displayed online in a place or places that a
  consumer seeking to end the contract is likely to find them". Every section of the chapter carries the
  note "not in force at Royal Assent" on legislation.gov.uk, and the government's response to its
  consultation, published April 2, 2026, says: "We will legislate when parliamentary time allows and we
  anticipate that the regime will commence in spring 2027."
  **Who this does not bind:** nobody, until commencement; after it, the contents and timing of notices
  come from regulations under sections 259 and 277, which did not exist on the day opened; business
  customers. Until then the Consumer Contracts (Information, Cancellation and Additional Charges)
  Regulations 2013 and the general law on unfair practices apply, and their cooling-off arithmetic is left
  to you.
- **Platforms: Apple, Google Play, Stripe, Chargebee, Paddle.** Grace periods, retry windows,
  subscription statuses, pauses, access after cancellation, price-change consent, automatic emails: each
  number in `references/` carries its page and the day it was opened.
  **Who this does not bind:** any other platform, and any of these after a release later than the page's
  date. It is product behavior, not a norm.

## Sources

**Sources, each opened 2026-09-15.**

- California Business and Professions Code § 17601 (definitions; subdivision (b) on the July 1, 2025
  applicability) and § 17602 (the article's duties):
  https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17601. and
  https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=BPC&sectionNum=17602.
- 15 U.S.C. § 8403, Restore Online Shoppers' Confidence Act (Legal Information Institute):
  https://www.law.cornell.edu/uscode/text/15/8403
- Federal Trade Commission, Negative Option Rule (rule page):
  https://www.ftc.gov/legal-library/browse/rules/negative-option-rule
- Federal Trade Commission, Rule Concerning the Use of Prenotification Negative Option Plans, advance
  notice of proposed rulemaking (16 CFR part 425; the vacatur of July 8, 2025 in its background):
  https://www.ftc.gov/system/files/ftc_gov/pdf/p064202negativeoptionruleanprm.pdf
- Visa, Updated Policy for Subscription Merchants Offering Free Trials or Introductory Promotions,
  article AI09067 (June 20, 2019; effective April 18, 2020):
  https://usa.visa.com/dam/VCOM/global/support-legal/documents/subscription-merchants-visa-public.pdf
- Visa, Updates to Rules for Declined Transaction Resubmission and Use of Authorization Response Codes,
  article AI10325 (September 3, 2020; effective April 17, 2021):
  https://usa.visa.com/dam/VCOM/global/support-legal/documents/updates-to-rules-for-declined-transaction-resubmission-and-use-of-authorization-response-codes.pdf
- J.P. Morgan Payments Developer Portal, Authorization retry logic (Visa categories; Mastercard merchant
  advice codes):
  https://developer.payments.jpmorgan.com/docs/commerce/online-payments/capabilities/online-payments/payment-methods/cards/authorization
- Bürgerliches Gesetzbuch § 309 (no. 9) and § 312k: https://www.gesetze-im-internet.de/bgb/__309.html and
  https://www.gesetze-im-internet.de/bgb/__312k.html
- Digital Markets, Competition and Consumers Act 2024, Part 4 Chapter 2 (sections 253 to 281):
  https://www.legislation.gov.uk/ukpga/2024/13/part/4/chapter/2
- Department for Business and Trade, Government response to consultation on the implementation of the new
  subscription contracts regime (April 2, 2026):
  https://www.gov.uk/government/consultations/consultation-on-the-implementation-of-the-new-subscription-contracts-regime/outcome/government-response-to-consultation-on-the-implementation-of-the-new-subscription-contracts-regime-web-accessible-version
- Apple, App Store Connect Help, Enable Billing Grace Period for auto-renewable subscriptions:
  https://developer.apple.com/help/app-store-connect/manage-subscriptions/enable-billing-grace-period-for-auto-renewable-subscriptions
- Apple, StoreKit, Reducing involuntary subscriber churn (billing retry up to 60 days, grace period
  behavior, expiration intent):
  https://developer.apple.com/documentation/storekit/reducing-involuntary-subscriber-churn
- Apple, App Store Connect Help, Manage pricing for auto-renewable subscriptions (price increase consent
  and notice):
  https://developer.apple.com/help/app-store-connect/manage-subscriptions/manage-pricing-for-auto-renewable-subscriptions
- Google Play Billing, Subscriptions, and Subscription lifecycle (grace period, account hold, pause,
  cancellation, restore): https://developer.android.com/google/play/billing/subscriptions and
  https://developer.android.com/google/play/billing/lifecycle/subscriptions
- Stripe, Automate payment retries (Smart Retries, hard decline codes, custom schedules, the end of the
  window): https://docs.stripe.com/billing/revenue-recovery/smart-retries
- Stripe, How subscriptions work (statuses): https://docs.stripe.com/billing/subscriptions/overview
- Stripe, Automate customer emails (failed payment, trial ending, renewal, expiring card, the hosted
  link): https://docs.stripe.com/billing/revenue-recovery/customer-emails
- Stripe, How cards work (automatic card updates):
  https://docs.stripe.com/payments/cards/overview
- Stripe, Pause payment collection: https://docs.stripe.com/billing/subscriptions/pause-payment
- Stripe, Configure the customer portal (cancellation, reasons, retention coupons):
  https://docs.stripe.com/customer-management/configure-portal
- Chargebee, Dunning: https://www.chargebee.com/docs/2.0/dunning.html
- Chargebee, Pause subscription: https://www.chargebee.com/docs/2.0/pause-subscription.html
- Paddle, Retain, Cancellation flows: https://developer.paddle.com/concepts/retain/cancellation-flows-surveys/
