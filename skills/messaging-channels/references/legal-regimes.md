---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Legal regimes: the platform and carrier layer, quoted and dated

`SKILL.md` says which skill owns the basis for sending, names the rules below, and says what this skill
leaves to you. This file states each rule, ends it with the people it does not bind, and lists every source
it rests on at the end. This is not legal advice.

## The rules

Eight rules, each with the boundary it does not cross.

- **WhatsApp: opt-in before contact, opt-out honored anywhere, templates outside the window.** The
  WhatsApp Business Messaging Policy allows contact "only" if "(a) they have given you their mobile
  phone number; and (b) you have received opt-in permission from the recipient confirming that they
  wish to receive subsequent messages or calls from you". You "must respect all requests (either on or
  off WhatsApp) by a person to block, discontinue, or otherwise opt out of communications from you via
  WhatsApp, including removing that person from your contacts list". You "may reply to a user message
  without use of a Message Template as long as it's within 24 hours of the last user message"; outside
  that window "you may only send messages via approved Message Templates".
  **Who this does not bind:** other messaging platforms and SMS, which have their own rules. It is a
  platform rule that Meta enforces through standing and access, not a statute.
- **WhatsApp: what the opt-in has to say.** Meta's opt-in guidance says businesses "must clearly state
  that a person is opting in to receive communication from the business", "must clearly state the
  business's name", and that the opt-in covers "the different categories of messages that a business
  will send"; the supported methods are "SMS, Website, By phone (using an interactive voice response
  (IVR) flow), In person or on paper". The same page says "Our systems will rate limit businesses if
  the business's quality is low for a sustained period of time."
  **Who this does not bind:** the lawful basis itself, which is the neighbor's question under the
  person's country; this is a condition of the platform.
- **WhatsApp: limits, categories, pauses, time-to-live and pricing are platform rules.** Each number
  in `references/` carries its page and date. Effective July 1, 2025, "Meta charges on a per-message
  basis" and "you are only charged when a template message is delivered"; templates "must be
  categorized as authentication, marketing, or utility"; a template at the lowest quality is paused for
  3 hours, then 6 hours, then disabled; marketing template messages to one person are limited by the
  platform across all businesses.
  **Who this does not bind:** other messaging apps, RCS and SMS. A release after the date on the page
  means opening the page again.
- **United States, carriers: A2P 10DLC registration.** Twilio's compliance documentation states that
  A2P 10DLC "is the standard that United States telecom carriers have put in place to ensure that SMS
  traffic to US end users through long code phone numbers is verified and consensual", that "anyone
  sending SMS/MMS messages over a 10DLC number from an application to the US must register", with a
  brand and a campaign, and that registration requires "information about how end users can opt-in,
  opt-out, and receive help" and "a description of the purpose of your messages"; senders who do not
  register "will receive additional carrier fees for sending unregistered traffic".
  **Who this does not bind:** short codes and toll-free numbers, which run their own programs; other
  countries. It is a carrier standard applied through providers, not a statute; what a carrier does
  with unregistered traffic beyond the fee is what your provider reports.
- **United States, industry: the CTIA Messaging Principles and Best Practices (May 2023).** Consent
  follows the content: for promotional messaging "the Consumer should agree in writing to receive
  promotional texts", while informational messaging needs the person to "agree to receive texts for a
  specific informational purpose when they give the Non-Consumer their mobile number" (Exhibit II). A
  recurring program sends an opt-in confirmation with "(1) the program name or product description;
  (2) customer care contact information"; "(3) how to opt-out; (4) a disclosure that the messages are
  recurring and the frequency of the messaging; and (5) clear and conspicuous language about any
  associated fees" (5.1.2.1). "A Consumer opt-in should apply only to the campaign(s) and specific
  Message Sender for which it was intended or obtained" (5.1.2.2). Senders "should acknowledge and
  honor all Consumer opt-out requests by sending one final opt-out confirmation message per campaign",
  after which "no further messages should be sent"; "Standardized 'STOP' wording should be used",
  and opt-out "with normal language (i.e., stop, end, unsubscribe, cancel, quit, 'please opt me out')
  should also be read and acted upon", with no effect from "capitalization, punctuation, or any
  letter-case sensitivities" (5.1.3). Senders "should not use opt-in lists that have been rented, sold,
  or shared" (5.1.4), "should process telephone deactivation files regularly (e.g., daily)" (5.1.5),
  and "should not engage in Snowshoe Messaging, which is a technique used to spread messages across
  many sending phone numbers or short codes" (5.5.2); shared numbers "may require special
  arrangements" (5.5.1).
  **Who this does not bind:** senders outside the United States. They are industry principles, not a
  statute; carriers apply them through their own terms, and the FCC rule below is the law.
- <a name="us-tcpa-revocation"></a>**United States, 47 CFR 64.1200(a)(10) through (12): revocation at the origin.**
  FCC 26-67 takes effect November 25, 2026. For earlier requests, check the rule in force at receipt.
  This rule covers revocation of prior express consent, including written consent, for calls and texts
  under (a)(1) through (3) and (c)(2). `consent-and-preferences` owns the basis and recorded scope.

  **Route, (a)(10) and (11).** A caller can designate one or more exclusive methods: an automated
  interactive voice or key-press opt-out on a call, a reply to an incoming text with `stop`, `quit`,
  `end`, `revoke`, `opt out`, `cancel`, or `unsubscribe`, or a website or phone number the caller
  provides for opt-outs. "The caller must clearly and conspicuously disclose the designated method to
  revoke consent on the call or in the text." For exclusive keyword replies, disclose at least one of
  the words in each text and accept all seven. If the caller properly designates an exclusive method,
  the FCC rule does not require processing requests by other means. Otherwise, (a)(11) says callers
  "must process revocation requests made by any reasonable means." For a method outside the list,
  evidence from the recipient that they made the request creates a rebuttable presumption absent
  contrary evidence. A dispute turns on the totality of the circumstances. If the texting protocol
  cannot receive replies, disclose that technical limitation and give reasonable alternatives, both
  clearly and conspicuously in each text. Honor valid requests within a reasonable time, no later than
  ten business days from receipt.

  **Scope, (a)(10).** The caller may limit a revocation in response to an informational call or text
  to the category it targets, unless the request expressly reaches further. A valid revocation in
  response to a call or text containing advertising or telemarketing stops all covered advertising
  and telemarketing calls and texts from that caller. The provider's pool block can have a different
  scope. Verify the remaining basis and channel rules before keeping any separate stream.

  **Confirmation, (a)(12).** This paragraph addresses (a)(1) and (2) only. The FCC does not require a
  confirmation. To qualify, the text "merely confirms the text recipient's revocation request and
  does not include any marketing or promotional information." The rule says: "If the confirmation
  text is sent within five minutes of receipt, it will be presumed to fall within the consumer's prior
  express consent. If it takes longer, however, the sender will have to make a showing that such delay
  was reasonable." Apply the recorded scope without a question in the confirmation or a wait for a
  reply. Check carrier and platform rules separately.

  **Who this does not bind:** traffic outside the cited TCPA provisions, including email and push.
  Ask counsel how the federal definitions, state law and separate do-not-call rules apply to your setup.
- **Google, RCS for Business: consent, STOP in the agent's language, brand-wide revocation.** The
  Acceptable Use Policy requires that "you must first provide end users with notice and obtain consent
  prior to soliciting any end user"; "all agents must comply with a user's request to opt-out (for
  example, 'STOP' message or equivalent in agent's language) and be able to promptly process and
  adhere to users' request to opt-out"; "brands must comply with a user's revocation of consent across
  all of their promotional agents"; and agents "only communicate with users who have explicitly opted
  into receiving your messages".
  **Who this does not bind:** SMS and WhatsApp; RCS delivered through a carrier's own platform rather
  than Google's. It is a platform rule.
- **Twilio: how one provider executes keywords and reports statuses.** Twilio handles "STOP,
  UNSUBSCRIBE, END, QUIT, STOPALL, REVOKE, OPTOUT, and CANCEL" by default; "stop", "start", "unstop" and
  "help" are reserved and cannot be removed; after a stop keyword Twilio "adds this phone number to a
  list of blocked numbers" and "any subsequent outgoing messages from your account to this user will
  fail with Error Code 21610", the configuration applying "to all senders (long codes, short codes,
  and toll-free numbers) in your sender pool"; when a message matches a configured keyword, Advanced
  Opt-Out "returns the confirmation message". Its message status "sent" means "the nearest upstream
  carrier accepted the outbound message", and "delivered" means confirmation "from the upstream
  carrier, and, where available, the destination handset".
  **Who this does not bind:** any other provider, which documents its own keywords, block scope and
  statuses. It is product behavior, not a norm, and it stands here because the mechanics need one
  worked example of where the block lives.

## Sources

**Sources, opened 2026-09-15 unless dated separately.**

- WhatsApp Business Messaging Policy: https://whatsappbusiness.com/policy/
- Meta, WhatsApp Business Platform, Getting opt-in:
  https://developers.facebook.com/docs/whatsapp/overview/getting-opt-in
- Meta, WhatsApp Business Platform, Pricing (message categories, per-message pricing from July 1,
  2025, the 24 hour customer service window, the 72 hour free entry point window in which every message
  is free, utility templates free inside the window): https://developers.facebook.com/docs/whatsapp/pricing
- Meta, WhatsApp Business Platform, Messaging limits (set per business portfolio and shared by its
  numbers): https://developers.facebook.com/docs/whatsapp/messaging-limits
- Meta, Template fundamentals (statuses, review):
  https://developers.facebook.com/docs/whatsapp/message-templates/guidelines
- Meta, Template categorization (mixed content, recategorization):
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-categorization
- Meta, Template quality rating:
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-quality
- Meta, Template pausing:
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/template-pausing
- Meta, Per-user marketing template message limits:
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/marketing-templates/per-user-limits
- Meta, Time-to-live:
  https://developers.facebook.com/documentation/business-messaging/whatsapp/templates/time-to-live
- Twilio, A2P 10DLC (compliance): https://www.twilio.com/docs/messaging/compliance/a2p-10dlc
- CTIA, Messaging Principles and Best Practices, May 2023 (sections 5.1.2.1, 5.1.2.2, 5.1.3, 5.1.4,
  5.1.5, 5.5.1, 5.5.2; Exhibit II):
  https://api.ctia.org/wp-content/uploads/2023/05/230523-CTIA-Messaging-Principles-and-Best-Practices-FINAL.pdf
- FCC, FCC 26-67, final rule, FR Doc. 2026-21821, Final Rules, 47 CFR 64.1200(a)(10) through (12),
  opened 2026-11-21: https://www.federalregister.gov/documents/full_text/html/2026/10/26/2026-21821.html
- Google, RCS for Business, Acceptable Use Policy:
  https://developers.google.com/business-communications/rcs-business-messaging/terms-and-policies/aup
- Google, RCS for Business, How it works (capability check, fallback to SMS):
  https://developers.google.com/business-communications/rcs-business-messaging/guides/get-started/how-it-works
- Twilio, Advanced Opt-Out (default keywords, reserved keywords, the block and error 21610):
  https://www.twilio.com/docs/messaging/tutorials/advanced-opt-out
- Twilio, Message resource (status values):
  https://www.twilio.com/docs/messaging/api/message-resource
- Twilio, What is the SMS character limit (GSM-7 and UCS-2, segments):
  https://www.twilio.com/docs/glossary/what-sms-character-limit
- Vonage, SMS concatenation and encoding:
  https://developer.vonage.com/en/messaging/sms/guides/concatenation-and-encoding
