---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Legal regimes: the data of a test and the messages it withholds, stated and dated

`SKILL.md` says why a control group creates no new obligation and removes none, and names the rules.
This file states each rule, ends it with the people it does not bind, and lists every source with its
date at the end. This is not legal advice.

## The rules

- **EU and UK, on the data: a model that assigns people to arms is profiling and needs its own recorded
  basis.** A purchase probability or a churn score that decides who enters a test evaluates the person.
  Where arm membership decides access to a price, to credit or to a service and no human is involved,
  the separate restriction `segmentation` describes can apply. **Who this does not bind:** a random
  split, which evaluates nothing about the person, and an arm whose only outcome is which message
  arrives.
- **EU and UK: a group is not built on an attribute that reveals a special category, and an inference
  counts.** Every category Article 9(1) of the GDPR lists stays special category data when a cut infers
  it from purchases under another name: racial or ethnic origin, political opinions, religious or
  philosophical beliefs, trade union membership, genetic data, biometric data used to identify a person,
  health, sex life and sexual orientation. `consent-and-preferences` gives the test for a proxy. **Who
  this does not bind:** an attribute that reveals none of those categories.
- **EU and UK: an objection to direct marketing takes the person out of a marketing test.** The right to
  object covers profiling related to direct marketing (GDPR Article 21(2) and (3)). The person leaves
  their arm, treated or control, on the day of the objection, and the assignment log records the removal
  with its date (`references/control-groups-and-holdouts.md`). **Who this does not bind:** a test of a
  service row that rests on another basis, such as an optional reminder inside an order the person
  placed.
- **EU and UK: the assignment log is kept until the reading is frozen, and no longer.** Rows that
  identify a person are kept no longer than their purpose needs (GDPR Article 5(1)(e)); a reading is
  frozen once the test log holds its result and read date, and what survives is the aggregate. A global
  control keeps its log while it is live. **Who this does not bind:** a test log entry from which no
  person can be identified.
- **Wherever a deletion right applies, it reaches the assignment log.** The person leaves the log and
  every future reading; whether a reading already frozen gets recomputed is a rule you write before the
  first request, not after. The GDPR's erasure article was not opened for this library, so open it
  before you rely on its terms. `consent-and-preferences` owns the erasure route. **Who this does not
  bind:** data the regime lets or requires you to keep, and people no deletion right reaches.
- **United States, CAN-SPAM: the treated arm gets the same message rules as any send.** You honor an
  opt-out within ten business days, and every commercial email carries your valid physical postal
  address. Being in a test does not change a message's class. **Who this does not bind:** a message
  whose primary purpose is one of the five categories of transactional or relationship message, and a
  message with neither commercial nor transactional content.
- **Canada, CASL: consent is required before sending to the treated arm exactly as for any campaign, and
  implied consent has a clock.** Two years from a purchase, a lease or an accepted business opportunity;
  for a written contract, while it is in force and for two years after it expires; six months from an
  inquiry or an application. A test that runs longer than the clock can outlive the basis part of the
  treated arm started on, so check the basis at each send, not at assignment. **Who this does not
  bind:** express consent, which does not expire and ends only with an unsubscribe.
- **Price: a test that charges different people different prices is checked with counsel before it
  runs.** Pricing transparency, disclosure of personalized prices and non-discrimination rules exist in
  several regimes, and this library has not opened a document on them, so it names no rule. The safer
  form of the same experiment holds the price constant and varies the offer. **Who this does not bind:**
  a test in which every arm pays the same price.
- **Children: nobody below the age line of their regime is assigned to a marketing test.** The ages by
  regime are in `consent-and-preferences`. **Who this does not bind:** a parent assigned on the parent's
  own data, including a child's birthday the parent gave for the parent's own message.
- **Required messages are never withheld.** A row a law or a contract requires (a notice before a
  renewal or a charge, a suspension notice) goes to the control group like everyone else, and so do
  access, confirmation and the first message of an exception (`transactional-messaging`). **Who this
  does not bind:** an optional service row that repeats what was already delivered, which can be tested
  against its absence, randomized by case.

## Sources

**Sources.** GDPR Articles 5(1)(e), 9(1) and 21, the CAN-SPAM compliance guide of the FTC and CASL
section 10(10) are quoted, with their addresses, in `consent-and-preferences`, opened 2026-09-14;
the FTC guide was opened again for `triggered-messages` on 2026-09-16. The ICO page on automated
decision-making including profiling is quoted, with its address, in `segmentation`, opened
2026-09-15. CRTC, *Guidance on Implied Consent*, opened 2026-09-07:
https://crtc.gc.ca/eng/com500/guide.htm
