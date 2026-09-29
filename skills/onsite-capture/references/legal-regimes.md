---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Legal regimes: collection, tracking, overlays and accessibility, quoted and dated

`SKILL.md` names the baseline this skill assumes, names the rules below, and says what this skill leaves to
you. This file states each rule, ends it with the people it does not bind, and lists every source it rests on
at the end. This is not legal advice.

## The rules

- **EU.** Marketing consent must be freely given, specific and confirmed by an affirmative act
  (GDPR, Article 4(11)). A pre ticked box is not consent, and consent has to be demonstrable after
  the fact (Article 7(1)). Whether marketing email may be sent at all is the ePrivacy question,
  Article 13, and `consent-and-preferences` holds both texts. **Who this does not bind:** a message
  that is not direct marketing.
- **UK.** The same standard for consent, plus a question the EU regime does not ask: the type of
  subscriber. **Who this does not bind:** a corporate subscriber, for the consent rule only: you
  may send them unsolicited marketing email with neither consent nor the soft opt-in. Not for the
  rest of the regime. The ICO asks you not to hide your identity in messages to either type of
  subscriber, to give a valid contact address for opting out, and to comply with a corporate
  subscriber's opt-out request; a named work address is also personal data, and the person's right to
  object stands where PECR asks for no consent (`b2b-lifecycle` holds the quotes). A B2B form and
  a consumer form therefore do not collect the same permission, and a form that serves both
  collects the stricter one.
- **Both, on the device.** Reading and writing on the device needs its own permission, separate
  from permission to be emailed. In the EU, Article 5(3) of the ePrivacy Directive allows "the
  storing of information, or the gaining of access to information already stored, in the terminal
  equipment of a subscriber or user" only where the person "has given his or her consent, having
  been provided with clear and comprehensive information". In the UK, regulation 6(1) of PECR, as
  substituted by the Data (Use and Access) Act 2025 from 2026-02-05, reads: "Subject to Schedule A1,
  a person must not store information, or gain access to information stored, in the terminal
  equipment of a subscriber or user." Schedule A1, paragraph 2, allows it where the person "is
  provided with clear and comprehensive information about the purpose of the storage or access" and
  "gives consent to the storage or access." That has a practical consequence for this skill: a
  display rule that depends on visit history does not run for someone who refused, so every point
  needs a fallback that works on current session signals alone. **Who this does not bind:** storage
  or access "for the sole purpose of carrying out the transmission of a communication", or strictly
  necessary to provide a service the person requested (in the EU, "explicitly requested"; in the UK,
  Schedule A1 paragraph 4, whose examples include "maintaining a record of selections made on a
  website"). The UK adds two exceptions without consent, each needing clear information and "a
  simple means of objecting, free of charge": statistics about how the service or website is used,
  with a view to improving it (paragraph 5), and adapting how the website appears or functions to
  the person's preferences (paragraph 6). None of them names targeting, and whether remembering that
  a person closed a point fits one is a question for counsel, not a permission. The Directive runs
  through national law.
- **United States.** Email runs on an opt-out model, but the promise made at the point of capture
  binds you: someone who signed up for a digest has not agreed to a daily promotion. Phone is a
  different regime. Marketing calls and texts carry a consent requirement of their own and a
  federal delivery window of 8:00 to 21:00 local to the recipient, so a phone field pulls all of
  that into the form. State law adds disclosure and opt-out requirements; Florida, for one,
  narrows the window to 20:00. We have not surveyed all fifty, so treat that as a question for
  your own list of states rather than a pattern. **Who this does not bind:** the phone rules do
  not reach email or push at all; the delivery window is written for telephone solicitation, and
  its definition excludes anyone who gave prior express permission or sits inside an established
  business relationship; and the *written* consent rule covers telemarketing only. An
  informational or transactional message sits outside that one and not outside the regime: a text
  sent by an automated system to a mobile number needs the person's prior express consent whatever
  it says (`consent-and-preferences` quotes paragraph (a)(1)), so a phone field collected for
  service texts still needs its own consent line.
- **Canada.** Express consent, with a record of when it was given, how, and for what. Implied
  consent exists there too, and its life runs from the event that created it: two years from a
  purchase or a written contract, six months from an inquiry. A capture point that records the
  address without recording the event leaves you unable to count either period. **Who this does
  not bind:** express consent, which does not expire and ends only with an unsubscribe.
- **Children.** Every regime opened in this library draws an age line, and they differ: the GDPR
  line, the UK line, COPPA and California each sit at a different age, and `consent-and-preferences`
  keeps the lines. A point whose audience may include children asks the age before it writes any
  record; where the line runs is the neighbor's, placing the gate is this skill's. **Who this does not
  bind:** a point whose audience cannot include children; `consent-and-preferences` states whom each age
  line binds and whom it does not.
- **Platforms.** Two documents written by a search engine and by an industry coalition rather than
  by law, and only one of them reaches a capture point. Google Search Central, *Avoid intrusive
  interstitials and dialogs*, covers overlays "usually for promotional purposes" and names newsletter
  sign-up prompts among them. It says intrusive ones "make it hard for Google and other search
  engines to understand your content, which may lead to poor search performance", recommends
  "banners that take up only a small fraction of the screen" in place of full-page interstitials,
  and lists two mistakes: "Don't obscure the entire page with interstitials" and "Don't redirect the
  user to a separate page for their consent or input." It names no size, no delay and no device, so
  those stay parameters you set and test. The Better Ads Standards of the Coalition for Better Ads
  list pop-up ads among the experiences Google's Ad Experience Report flags, and Chrome filters the
  ads on a site that fails that review. They do not reach your own capture point: for the report,
  an ad is "promotional content displayed on a website as the result of a commercial transaction
  with a third party." **Who this does not bind:** the search guidance exempts interstitials a site
  is legally required to show, such as an age gate; the Standards and the filtering bind third-party
  ads only, so a capture point is judged against the search guidance and not against them.
- **Accessibility.** A modal dialog and an inline form need opposite rules here, and one sentence
  covering both leaves you with the wrong instruction for one of them.
  - *Modal dialog.* Move focus into the dialog when it opens. Let Tab and Shift+Tab cycle inside
    it. Make Escape close it, and give the close control a visible target the keyboard can reach.
    On close, return focus to whatever opened the dialog. While it is open, make the rest of the
    page inert for the mouse and for the screen reader. Holding focus inside the dialog is the
    correct behavior for a modal. The standards forbid something else: a trap the keyboard
    cannot leave.
  - *Inline form.* Do not take focus. The form sits in the page's normal tab order where it sits
    in the markup, and it does not pull in a reader who never opened it.
  - *Both.* Give the dialog and every field an accessible name. Tie each error message to the
    field it belongs to instead of leaving it as loose text nearby. Before the point ships, walk
    it once on the keyboard alone, from display through submit and back to where you started.

  Get this wrong and part of your audience cannot use the page at all.
  **Standards, each opened 2026-09-07.** W3C ARIA APG, *Modal Dialog Pattern*,
  https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/, for focus on open, the Tab cycle,
  Escape, focus return, `aria-modal` and the inert background. WCAG 2.1, criterion 2.1.2
  *No Keyboard Trap*, https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html, which
  requires a keyboard way out and permits confining focus to a subsection of the page.
  **Who this does not bind:** both documents are technical standards, not law. They bind you
  where your country's law or an industry requirement points at them, and only for the
  organizations that law reaches. Everywhere else, this is a quality bar the library holds
  itself to.

## Sources

**Legal sources, with the date each was last opened.**

- Regulation (EU) 2016/679 (GDPR), Articles 4(11) and 7, opened 2026-09-14 by
  `consent-and-preferences`:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679
- Directive 2002/58/EC (ePrivacy), consolidated text of 2009-12-19, Article 13, opened 2026-09-14
  by `consent-and-preferences`, and Article 5(3), opened 2026-09-16:
  https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219
- The Privacy and Electronic Communications (EC Directive) Regulations 2003, regulation 6, opened
  2026-09-16: https://www.legislation.gov.uk/uksi/2003/2426/regulation/6
- The same regulations, Schedule A1, paragraphs 2 to 6, opened 2026-09-16:
  https://www.legislation.gov.uk/uksi/2003/2426/schedule/A1
- FCC, 47 CFR § 64.1200, restriction at (c)(1) and definition at (f), opened 2026-09-16:
  https://www.ecfr.gov/current/title-47/chapter-I/subchapter-B/part-64/subpart-L/section-64.1200
- Florida Statutes § 501.616(6)(a), opened 2026-09-16:
  https://www.flsenate.gov/Laws/Statutes/2026/501.616
- CRTC, *Guidance on Implied Consent*, opened 2026-09-07:
  https://crtc.gc.ca/eng/com500/guide.htm
- ICO, *Guidance on direct marketing using electronic mail*, opened 2026-09-16:
  https://ico.org.uk/for-organisations/direct-marketing-and-privacy-and-electronic-communications/guidance-on-direct-marketing-using-electronic-mail/how-do-we-comply-with-the-pecr-electronic-mail-marketing-rules/

**Platform documents, with the date each was last opened.**

- Google Search Central, *Avoid intrusive interstitials and dialogs*, page last updated 2025-12-10,
  opened 2026-09-16:
  https://developers.google.com/search/docs/appearance/avoid-intrusive-interstitials
- Coalition for Better Ads, *The Initial Better Ads Standards*, opened 2026-09-16:
  https://www.betterads.org/standards/
- Google Web Tools Help, *Introduction to the Ad Experience Report* and *Chrome ad filtering*,
  opened 2026-09-16: https://support.google.com/webtools/answer/7159932 and
  https://support.google.com/webtools/answer/7308033
