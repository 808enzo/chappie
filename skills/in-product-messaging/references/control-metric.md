---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Control metric: how to read the wasted interruption share

`SKILL.md` defines the wasted interruption share: the session, the blocking display, the completion event by
class, what counts as closed, the numerator and the denominator; why sessions and not displays, why not
click rate, why the first sessions of an install sit apart, what lowers it without better work, and what it
cannot see. This file holds what moves it and the lines read beside it.

## What moves it

**Where it moves.** Down when blocking displays are moved to passive formats, when eligibility narrows
to a state, when a slot moves to the screen where the message can be answered, when repeated pitches are
suppressed, when expiry is applied.
Up after a release that broke a destination on one platform (the split by platform shows it), when a
campaign got the service setting "every session", and when the register lives in three systems (displays
with no decision record and the budget breach share show it).

## Read beside it

**What to read beside it, and promote neither.**

- **Reach of appearances**, per message: the people shown it at least once among the eligible people
  with at least one appearance in its window. It catches an idle channel and a crowded budget: when
  more of those people end the window with the message expired unseen than shown, the message did
  not arrive.
- **Budget breach share**: the sessions with two or more blocking displays among all sessions,
  counted from the surfaces' display events like the numerator. It reads whether the rule executes,
  not whether it is any good.
- **A holdout on the conversion of the screen itself**, mandatory before a display rolls out to a
  slot at the bottom of the funnel, the cart or the checkout. `experiments-and-holdouts` builds it;
  the population is the people who reached the slot.
