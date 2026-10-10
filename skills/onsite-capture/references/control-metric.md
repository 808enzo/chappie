---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-06
---

# Control metric: how to read the usable capture rate

`SKILL.md` defines the usable capture rate: the numerator, the three kinds of row kept out of it, the fixed
population, why the denominator is fixed, the pair with the primary action, the answer to a question about a
normal pop-up rate, and the diagnostics of one point. This file holds how to read it.

## When a period's reading closes

A contact belongs to the period of its submission, and the numerator of a period is read only after the
two clocks that can still remove a row have run out: the confirmation window
(`intake-and-usable-contacts.md`, step 5), and the first message, which is what proves the address
deliverable. Until then the period is open, and a pending row that outlives its window leaves the
numerator as if it had never been submitted.

## The known share

The fixed denominator has a cost of its own, and you read it rather than hide it. Sessions of people
who already gave what the points ask for are in the population and can never produce a new usable
contact, so as the base matures the rate drifts down with nothing changing on the site. Report the
**known share**, sessions recognized as already in the base over the fixed population, next to the
rate: a fall in the rate with a rising known share is the base maturing, not the points failing.
Recognition runs on the device, so the known share undercounts on new devices; it is a floor, and
you read its trend rather than its level.

## Read next to it

Report the local efficiency of the rule next to the rate and never in its place: eligible share
(eligible sessions over the fixed population), impression rate, submit rate, confirmation rate, and
the absolute count of new usable contacts. The last one is what the base received, and it is the
number a narrowing has to answer to. The two readings are separate conclusions: the rule got
better at converting the sessions it kept, and the site produced fewer contacts.

## Measuring a change to a point

To measure a change to a point rather than watch a ratio, randomize on entry to the fixed
population, before you apply the targeting you are changing, and name the primary action metric
before the test starts. The unit of assignment is the visitor identifier the site holds, the cookie
or device, so that a returning visitor stays in the arm they were assigned to; a session that
carries no identifier is assigned on entry, and its share of the population is read next to the
result, because at that share the comparison is between two mixtures. `experiments-and-holdouts`
owns the design and says the same about the unit. A before-and-after comparison of a ratio whose
denominator moved with the change answers nothing.
