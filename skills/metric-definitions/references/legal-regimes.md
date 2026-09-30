---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Legal regimes: the data a metric is computed on, stated and dated

`SKILL.md` says why the axis here is data rather than permission to send, and names the rules. This
file states each rule, ends it with the people it does not bind, adds one practice that is not law, and
says where every source is quoted, with its date. This is not legal advice.

## The rules

- **EU and UK, on the data: a metric reads only data collected for a purpose measurement is
  compatible with, and person-level rows are kept no longer than that purpose needs.** Data
  collected to fulfill an order does not automatically become material for profiling (GDPR
  Article 5(1)(b)), and retention is set on the row about a person, not on the aggregate (Article
  5(1)(e)). `consent-and-preferences` quotes both articles and keeps the register of purposes a
  report's basis is read from. **Who this does not bind:** a published aggregate from which no
  person can be identified; the rule reaches the rows it is computed from, not the figure.
- **EU and UK: a metric that indirectly reveals a special category does not become a reporting
  dimension.** Health, religion, ethnicity, sexual orientation and every other category Article
  9(1) lists stay special category data when a cut infers them from purchases under another name;
  `consent-and-preferences` gives the test for a proxy. A score that decides what a person is
  offered is profiling and needs its own recorded basis. Where the decision is made solely by
  automated means and has a legal or similarly significant effect, such as access to a price, to
  credit or to a service, the separate restriction `segmentation` describes applies. **Who this
  does not bind:** a dimension that reveals none of the categories, and a score whose only outcome
  is which message arrives.
- **Wherever a deletion right applies, the person leaves future computation.** Whether published
  historical aggregates get rebuilt is a rule you write in advance rather than invent when the
  request arrives. The GDPR's erasure article was not opened for this library, so open it before
  you rely on its terms; `consent-and-preferences` owns the erasure route. **Who this does not
  bind:** data a regime lets or requires you to keep, and people no deletion right reaches.
- **United States, CAN-SPAM: an opt-out moves populations, not arithmetic.** People who opt out of
  commercial email leave the sending denominator of marketing email and stay in the customer
  denominators. Say which of the two a metric uses. **Who this does not bind:** messages whose
  primary purpose is transactional or relationship, which keep reaching people who opted out
  (`transactional-messaging`); texts and calls, which other rules govern
  (`consent-and-preferences`); state law, not surveyed here.
- **Everywhere, as practice rather than law.** Pseudonymization inside the analytics environment,
  and the rule that person-level extracts do not leave it, belong in the metric definition rather
  than in a separate policy nobody reads next to the number.

## Sources

**Sources.** GDPR Articles 5(1)(b), 5(1)(e) and 9(1) and the FTC's CAN-SPAM compliance guide are
quoted, with their addresses, in `consent-and-preferences`, each opened 2026-09-14. The ICO page
on automated decision-making including profiling is quoted, with its address, in `segmentation`,
opened 2026-09-15.
