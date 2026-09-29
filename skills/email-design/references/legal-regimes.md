---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Legal regimes: required elements, disclosures and accessibility, stated and dated

`SKILL.md` says which skills own permission to send, the headers and the claims, names the rules below,
and says what this skill leaves to you. This file states each rule, ends it with the people it does not
bind, and lists at the end every source the skill rests on, the platform documentation behind the
template and rendering steps included. This is not legal advice.

## The rules

- **United States, required elements of commercial email.** The notice explaining how to opt out has
  to be clear and conspicuous, crafted so that an ordinary person can recognize, read and understand
  it, and the Federal Trade Commission's guide names type size, color and location as the means of
  making it clear. The commercial nature of the message is disclosed clearly and conspicuously, and
  the message carries a valid physical postal address.
  **Who this does not bind:** messages whose primary purpose is transactional or relationship
  content are exempt from most of these provisions, and the CAN-SPAM Act covers commercial email in
  the United States without granting permission to send any of it.
- **United States, disclosures in digital advertising.** A disclosure needed to keep an ad from being
  deceptive has to be clear and conspicuous on every device and platform a consumer may use to view
  it, and a platform that offers no way to make it so should not carry ads that require it. A
  disclosure too small to read on a mobile device, whose text cannot be enlarged, is not clear and
  conspicuous. A disclosure buried in a long paragraph of unrelated text is not effective. Written
  claims take written disclosures, because people may be unable to view a video clip on their device.
  **Who this does not bind:** this is Commission staff guidance from 2013, and it applies where a
  disclosure is needed to keep an ad from misleading. It is not a layout rule for messages that need
  no disclosure.
- **European Union, misleading omission.** Hiding material information, or providing it in an
  unclear, unintelligible, ambiguous or untimely manner, counts as a misleading omission, as does
  failing to identify the commercial intent where the context does not make it apparent. Where the
  medium limits space or time, those limits are taken into account together with whatever the trader
  made available by other means.
  **Who this does not bind:** the directive governs business-to-consumer practices, and for these
  provisions the practice has to cause, or be likely to cause, a decision the consumer would not
  otherwise have taken.
- **United States, accessibility.** The Department of Justice holds that the ADA's requirements for
  businesses open to the public apply to the goods and services they offer on the web. The
  Department has no regulation setting detailed technical standards for those businesses and points
  to WCAG as helpful guidance. Its guidance does not discuss email.
  **Who this does not bind:** the 2022 guidance does not reflect the 2024 requirements for state and
  local governments, and it does not settle whether any of this reaches a marketing message. That is
  a question for counsel.
- **European Union, accessibility.** The accessibility directive applies to e-commerce services
  provided to consumers after 28 June 2025. It defines them as services provided at a distance,
  through websites and mobile device-based services, by electronic means and at the individual
  request of a consumer, with a view to concluding a consumer contract. Microenterprises providing
  services are exempt.
  **Who this does not bind:** the definition names websites and mobile device-based services and
  does not name messages, so whether an email sent as part of such a service falls inside the scope
  is not settled by that text. That is a question for counsel.
- **The reference measure behind the template steps: WCAG 2.2.** Non-text content has a text
  alternative serving the equivalent purpose, and pure decoration is implemented so that assistive
  technology can ignore it (1.1.1). Color is not the only visual means of indicating an action
  (1.4.1). Text has a contrast ratio of at least 4.5:1, and large text at least 3:1, with logotypes
  and decoration exempt (1.4.3). Text rather than images of text wherever the technology can achieve
  the presentation (1.4.5). Content presented without loss and without scrolling in two dimensions at
  a width of 320 CSS pixels (1.4.10). A pointer target at least 24 by 24 CSS pixels, except where
  undersized targets are spaced apart, an equivalent control meets the size, the target sits inline in
  a sentence, the size is set by the user agent, or a particular presentation is essential or legally
  required (2.5.8).
  **Who this does not bind:** WCAG is a W3C Recommendation for web content. It binds nobody by
  itself, it binds where a law, a contract or your own policy adopts it, and it applies to a message
  by analogy.

## Sources

**Sources, each opened 2026-09-13.**

- FTC, *CAN-SPAM Act: A Compliance Guide for Business*:
  https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business
- FTC, *.com Disclosures: How to Make Effective Disclosures in Digital Advertising*:
  https://www.ftc.gov/system/files/documents/plain-language/bus41-dot-com-disclosures-information-about-online-advertising.pdf
- EUR-Lex, Directive 2005/29/EC, consolidated text, Article 7:
  https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:02005L0029-20220528
- EUR-Lex, Directive (EU) 2019/882, Articles 2, 3 and 4:
  https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32019L0882
- U.S. Department of Justice, *Guidance on Web Accessibility and the ADA*:
  https://www.ada.gov/resources/web-guidance/
- W3C, *Web Content Accessibility Guidelines (WCAG) 2.2*: https://www.w3.org/TR/WCAG22/
- W3C, *Understanding Success Criterion 2.5.8: Target Size (Minimum)*:
  https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
- Google, *CSS Support* (Gmail): https://developers.google.com/workspace/gmail/design/css
- Google, *Register with Google to send dynamic emails*:
  https://developers.google.com/workspace/gmail/ampemail/register
- Google, *Supported platforms* (dynamic email):
  https://developers.google.com/workspace/gmail/ampemail/supported-platforms
- Google, *Debug dynamic emails*:
  https://developers.google.com/workspace/gmail/ampemail/debugging-dynamic-email
- Google, *Turn images on or off in Gmail*: https://support.google.com/mail/answer/145919
- Microsoft, *Block or unblock automatic picture downloads in classic Outlook email messages*:
  https://support.microsoft.com/en-us/office/block-or-unblock-automatic-picture-downloads-in-classic-outlook-email-messages-15e08854-6808-49b1-9a0a-50b81f2d617a
- Microsoft, *Dark Mode in Outlook*:
  https://support.microsoft.com/en-us/outlook/mail/dark-mode-in-outlook
- Microsoft, *The animated graphic in my e-mail message doesn't work*:
  https://support.microsoft.com/en-us/office/the-animated-graphic-in-my-e-mail-message-doesn-t-work-a5e8a2a3-9d86-4203-8920-c88cb8739e34
- Apple, *Mail Privacy Protection*: https://www.apple.com/legal/privacy/data/en/mail-privacy-protection/
- WebKit, *Dark Mode Support in WebKit*: https://webkit.org/blog/8840/dark-mode-support-in-webkit/
- IETF, RFC 2046, section 5.1.4: https://www.rfc-editor.org/rfc/rfc2046#section-5.1.4
