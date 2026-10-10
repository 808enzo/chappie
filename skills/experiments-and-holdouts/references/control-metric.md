---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Control metric: the read date of the incremental effect

`SKILL.md` defines the incremental effect: the difference in the decision metric between the treated arm
and its control, per unit assigned, with no credit rule in the numerator, and says what to answer when
someone asks for a normal value. This file holds the read date, before which the figure is provisional,
and the form in which the figure leaves this skill.

## The read date

- **A read date.** The last assignment, plus the outcome window, plus finalization
  (`references/test-design.md`, step 8). Before that date the figure is provisional. It leaves
  this skill with its interval and its read date, which is the form `crm-reporting` places on a
  report line.
