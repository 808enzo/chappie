---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Legal regimes: the basis, profiling, special categories and deletion, stated and dated

`SKILL.md` names the baseline this skill assumes and the rules, and says what this skill leaves to
you. This file states each rule, ends it with the people it does not bind, and lists every source
with its date at the end. This is not legal advice.

## The rules

- **EU and UK, on the data: you name the lawful basis before the processing, not after.** A rule
  that reads a person's history is processing whether or not a message ever goes out, so you
  settle the basis before the first run. **Who this does not bind:** nobody. A segment that never
  receives a send is still processing, and no cut of the base sits outside the requirement.
- **EU and UK: profiling that produces legal or similarly significant effects is restricted
  separately.** The restriction covers a decision made solely by automated means, with no human
  involvement, that produces a legal effect or similarly significantly affects a person. The
  effect has to have a serious impact, and the regulator's examples are automatic refusal of an
  online credit application and e-recruiting without human intervention. Where a cut does not
  meet that definition, you may keep profiling, subject to the principles, a recorded basis and
  working routes for people to exercise their rights. **Who this does not bind:** a cut whose only
  outcome is which message arrives, with no serious impact on the person. A cut that decides
  access to a price, to credit or to a service is where the restriction can apply, and that is a
  different conversation with a different person in your organization. Draw the line before
  somebody reuses the rule there.
- **EU and UK: special category data does not become an attribute without its own basis, and an
  inference counts.** Every category Article 9(1) lists stays special category when you derive it
  from purchase history and give the group a different name: racial or ethnic origin, political
  opinions, religious or philosophical beliefs, trade union membership, genetic data, biometric
  data used to identify a person, health, sex life and sexual orientation. The standard example
  is pregnancy inferred from a shopping pattern, and renaming the segment does not change what it
  holds. `consent-and-preferences` quotes the article and gives the test for a proxy. **Who this
  does not bind:** an attribute inferred from purchases that reveal none of those categories.
- **United States, California: the opt-out of sale or sharing reaches the exports
  `consent-and-preferences` registers as sale or sharing**: a segment uploaded to an advertising
  platform, a matched list, data given to a partner who uses it for its own purposes. **Who this
  does not bind:** businesses under the law's thresholds, consumers outside California, and an
  attribute that leaves your systems by none of those routes. Other states' privacy laws are not
  surveyed here.
- **Wherever a deletion right applies, it reaches the exports the rule has already produced.** A
  segment file sitting in someone's spreadsheet is a copy of the data and does not delete itself,
  so you do not close the request by removing the person from the rule. Under the California rules
  a consumer may request deletion subject to exceptions, such as information the business is
  legally required to keep. The GDPR's erasure article was not opened for this library, so open it
  before you rely on its terms. `consent-and-preferences` owns the erasure route and the
  suppression entry that survives it. **Who this does not bind:** data the regime lets or
  requires you to keep, and businesses and people no deletion right reaches.

## Sources

**Sources, each opened 2026-09-15.**

- ICO, *Rights related to automated decision making including profiling*:
  https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/rights-related-to-automated-decision-making-including-profiling/

Article 9(1) of the GDPR and the California Attorney General's CCPA page are quoted, with their
addresses and dates, in `consent-and-preferences`.
