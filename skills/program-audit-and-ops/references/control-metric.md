---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-16
---

# Control metric: what shortens time to detect

`SKILL.md` defines median time to detect: from the first failure to the moment somebody knew about it,
and which moment closes the interval. It says what decides whether the number means anything, why it
improves when detection gets worse, what to answer when someone asks what is normal, and the two numbers
to read beside it. This file says which part of this skill shortens the number, and for which objects.

## What moves it

Everything in this skill works on that one number. The roster shortens it for objects that have a
heartbeat, alerting shortens it for objects too expensive to leave until the next slot and for every
object whose failure would land in a severity class, and the audit shortens it for objects nobody
was watching at all.
