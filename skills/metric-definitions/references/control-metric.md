---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Control metric: when and how to read definition coverage

`SKILL.md` defines definition coverage: the denominator counted where decisions are taken, the numerator,
and the metrics to read beside it, and says why no benchmark exists for it. This file holds on which day a
reading is taken, when a new metric enters it, and which movement against your own history to act on.

## When and how to read it

- **When to read it:** on the day of each review of the set (`the-metric-set.md`), as a snapshot
  of that date. A metric added between reviews enters at the next one.
- **Read it:** against your own history, by direction rather than against a band, so the signal
  rule of `SKILL.md` does not apply to it. Coverage that stalls below full while the metric count
  grows is the movement to act on; it means new metrics arrive faster than definitions are written
  for them.
