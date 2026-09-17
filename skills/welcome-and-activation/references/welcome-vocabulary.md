---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-08
---

# Vocabulary for the first weeks

The terms all three mechanics assume. Four of them are shared with neighboring skills under
different meanings, and those are marked.

**Arrival.** The event that made a person known to the program: a subscription, a registration, an
enrollment, a first purchase without registration. Counted once per record. A second arrival is a
case of its own, handled in `exit-break-and-second-entry.md`.

**Entry point.** Not a traffic source and not a form, but a promise: what the person believes they
received in exchange for the contact. Two entry points are the same one only when the promise and
the target action both match.

**Promise of the entry point.** What was offered in exchange for the contact, written down verbatim
before the first touch is written. Kept by the first touch, before anything else.

**Welcome series.** A finite sequence of touches that begins at an arrival and ends in one of four
outcomes. Being finite is a property of it and not a setting: a series with no named ending is the
regular program under another name.

**Touch.** One message of the series, carrying a send condition and a skip condition.

**Send condition, skip condition.** The first says which state lets a touch go out. The second says
which state stops that touch while the series continues. A skip removes one touch; a break closes
the series.

**Target action.** One action per series, the thing it exists for and breaks on.
`triggered-messages` uses the same term for the same idea on a different unit: there it is measured
per entry into a flow, here per arrival of a person, and a person has many of the first and one of
the second.

**Window.** The length of the series, equal to your own median time to first purchase computed on
the people who did buy. `rfm-segments` computes the same figure for a different purpose, to decide
who is not in the grid yet, and calls the result a boundary of population rather than a length.

**Arrival cohort.** Everybody who arrived in a named period through a named entry point. The
denominator of the control metric. It differs from entries into the series by exactly the people the
series never got.

**Silent loss.** The gap between arrivals and entries: people who arrived and received nothing. A
report built on a flow cannot show it, because everybody in that report entered the flow.

**Break.** Ending the series because the target action happened. Checked before the send rather than
at assembly, since the action lands in the gap between the two.

**Handover.** Naming the mechanic a person belongs to next, for each outcome of the series. "Stayed
in the base" is not a name.

**Second entry.** A second arrival by the same person. Whether the series replays is decided by the
record's state, meaning whether the target action was ever completed, and not by the flow.

**Activation.** Here: the event by which somebody got a first value out of the product, written as
"X actions in Y days from arrival". **`loyalty-program-launch` uses the word for something else**, a
confirmed contact channel, meaning the record is reachable. There, activation is about whether a
message will arrive; here, about whether the person got what they came for. Both vocabularies carry
the split.

**Two-sided criterion.** How well an activation event separates: the share who succeeded among those
who did the event and the share who did not succeed among those who did not, both read against the
base rate of all arrivals. It says nothing about whether a series can lead people to the event. That
is a third number, the reach.

**Setup step.** An action between arrival and the activation event, without which the event cannot
happen or happens to no effect. A target for touches in its own right.

**First value.** What somebody came for, received at least once. Not the same as finishing the
onboarding: a product tour clicked through to the end counts as finished and is not a value.
