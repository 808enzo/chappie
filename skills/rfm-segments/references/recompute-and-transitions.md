---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Recompute, staleness, and reading a transition

A group here is a computed attribute, and a computed attribute is a photograph. The question
nobody asks until it costs something is how old the photograph is at the moment somebody sends to
it. The answer decides whether a winback message reaches a person who bought yesterday, which is
the one failure of this method that the recipient notices and remembers.

The question gets asked at the wrong level, as "is the group live or is it a snapshot".
Groups are not the unit that has a freshness class. **Axes are.** Recency is a function of one
stored date and today's date, and it changes for everybody every day without any event happening.
Frequency and money are aggregates over history that change only when somebody buys, and
computing them takes a pass over the orders. Those are different objects with different costs,
and treating them as one is what produces a stale group. The class belongs to an axis as your
stack computes it rather than to the axis in the abstract, and a group takes the worst class among
the axes its route depends on.

This mechanic covers declaring the freshness of each axis, setting the cadence from the axes that
need a pass, reading a group against its stamp, treating a move between groups as an occasion,
telling a first reading apart from a change of reading, and telling boundary movement apart from
people movement.

## Entry conditions

Groups are in use (`groups-and-routes.md`).

## Exit conditions

Each axis declared live or snapshot in the group definition, and the deciding axis of each group
named. A named cadence for the axes that need a pass. A recompute stamp on every export and
audience. A written rule for what fires on a transition, what gets re-checked before it does, and
what happens when the re-check disagrees. The first recompute on a new set of boundaries marked as
a baseline. Boundary re-cuts dated.

## Steps

**1. Declare each axis live or snapshot, and put the declaration in the group definition.** This
is `martech-stack`'s rule applied here: a consumer does not run faster than the freshness class of
its source. A group whose definition does not say this cannot be reproduced, and cannot be
defended after a mis-send. Name the deciding axis in the same line: the route depends on its band,
the control metric counts against it, and where several axes decide, the group takes the worst
class among them and counts as live only where every one of them is live.

**2. Recompute recency at selection wherever the platform allows it.** It costs one stored date
and today's date, and it is the axis that goes stale fastest, because it moves without anything
happening. Where the platform cannot do it, that is a fact about your stack rather than a
property of the method, and it goes into the definition as a snapshot so the routes that depend
on it can be written accordingly.

**3. Set the cadence from the aggregate axes and from how fast your base moves.** Frequency and
money need a pass, so they are what the cadence is for. Recency does not wait for it. The general
rule that a cadence follows the speed of the attribute rather than the convenience of the
schedule belongs to `segmentation`; what is added here is that one group has axes at two speeds
and the cadence describes only the slower ones.

**4. Read a group against its stamp.** Every export and every audience carries the time of the
last recompute. A group without a stamp cannot be matched to a result afterward: the result
belongs to whoever was in the group when the message went, and that population no longer exists
anywhere.

**5. Treat a move between groups as an occasion rather than a line in a report.** Leaving the
active buyer group for the lapsing one is an event a mechanic can fire on. It is the one thing the
grid gives you that a photograph of the grid does not: a moment when something changed, rather
than a state that has been true for a while. The construction of that flow belongs to
`triggered-messages`, and whether the row exists at all belongs to `scenario-map`.

**6. Re-check the axis that produced the transition before anything fires on it.** A transition
produced by a snapshot older than the axis's own movement is not a transition, it is a stale
read. This is the same rule as step 2 seen from the other end: the cheap check is worth running at
the moment it decides whether a message goes.

**7. A transition exists only between two finished recomputes on the same boundaries.** The
first recompute after the grid goes live, after history is loaded in behind it, and after a
boundary moves gives a person a first value rather than a change of value. Record it as a baseline
and fire nothing off it. Without this rule, the day you switch the grid on you tell the whole base
its state changed when nothing happened, and the day you move a boundary you send to everybody the
boundary passed over.

**8. Separate boundary movement from people movement.** When a group grows, one of two things
happened, and the repairs point in opposite directions: people moved across a fixed boundary, or
the boundary moved because it is a quantile and the distribution shifted under it. Read which one
before deciding anything, because a quantile band that "grew" grew by construction.

**9. Re-cut boundaries on the program revision cycle, and write down the date.** Any number read
across a boundary change is being compared against a different definition. The date in the record
is what lets somebody notice that a year later, when the change is invisible in the numbers
themselves.

## Thresholds and timings

- **Recency at selection; frequency and money at the cadence.** Where recency has to be a
  snapshot, the routes where being wrong is expensive re-check the last purchase date before
  sending.
- **Cadence, as a starting point: no longer than your own median interpurchase interval**, so
  that a person cannot cross the whole recency axis between two recomputes. That holds where the
  interval is stable. Replace it once you know your own share of people changing group per cycle,
  and take the cadence from that instead.
- **Boundary re-cut:** the program revision cycle, with the date recorded.
- **The first recompute on new boundaries is a baseline and no occasion comes off it.** That is
  not a starting figure you replace later; it follows from the construction, because no earlier
  reading on those boundaries exists to compare against.
- **An unfinished recompute means the group is not sent to.** Watching for a recompute that
  stopped is `program-audit-and-ops`, which carries a segment with a stalled recompute as a class
  of object on duty. This skill adds what that particular stall does: the group keeps returning
  people and keeps sending them a route matched to a state they have left.

## Edge cases

- **The recompute stopped and nobody noticed.** The group keeps returning people, which is
  exactly why nobody noticed. The sign of life is a completed recompute on schedule rather than a
  non empty export (`program-audit-and-ops`).
- **A person crosses a boundary and back every cycle.** That is the boundary population
  (`segmentation`). Either the boundary sits in the dense part of the distribution or that
  person's purchases do straddle it. Read the share of people doing it before you move anything:
  a boundary moved because of a handful of visible cases moves the whole base.
- **The base grew and every quantile band shifted.** By construction: a quantile is relative. If
  what you need is a stable meaning, that axis wants a business fact cut instead
  (`cutting-the-axes.md`, step 3).
- **Somebody changes group mid wave.** The assignment freezes at assembly, which is
  `segmentation`'s rule. This skill adds one exception: on the routes where being wrong is
  expensive, you re-check recency at send, even though the assignment itself stays frozen. When
  the re-check disagrees with the group, the message does not go and the group is not reassigned:
  the person stays where the assembly put them until the next recompute, and the cycle records a
  suppression rather than a transition. Write that consequence into the rule, because a re-check
  with nothing attached to it feeds a log and stops nothing.
- **A seasonal shift moves the whole base down a band.** That is the distribution moving, not the
  people. It is repaired by computing the interval within the season, not by rewriting the routes.
- **A transition produced by a boundary that moved.** The same test as a group that grew (step 8)
  tells it from a person who moved, but the cost differs: you read a size change in a report, and
  a transition sends a message. Until you hold two comparable recomputes on the new boundaries, no
  occasion comes off them, and the same rule covers switching the grid on and loading history in
  behind it.
- **A boundary re-cut lands in the middle of a running mechanic.** Finish the mechanic on the old
  boundary and start the next cycle on the new one, with both dates in the record. A mechanic that
  changes its audience definition halfway produces a result that belongs to neither definition.

## Failure modes

- **A winback message reached somebody who bought yesterday.** It is not caught by a report; it
  is prevented by step 2, and where step 2 was skipped it arrives as a complaint, which is late
  and from the wrong direction.
- **A result was read across a boundary re-cut.** The signal is a jump in a group's share landing
  in exactly the cycle the boundary moved, and an explanation built on the jump.
- **Transitions fired off a monthly snapshot in a base with a weekly interval.** The signal is a
  flow that fires in batches the day after each recompute, which is a schedule wearing the costume
  of a behavioral trigger.
- **The grid is recomputed and only the current state gets read.** Nobody looks at movement, so
  no transition exists as an occasion, and the recompute pays for a photograph nobody compares to
  the previous one.
- **A batch of transitions the day after a boundary moved.** The signal is a volume of firings
  close to the size of a band, all on one day. It differs from a seasonal shift by the date: it
  lands on the date of the re-cut you recorded.
- **Every axis was declared a snapshot because the platform documentation called the attribute
  computed.** The signal is a stale group send rate above zero on groups where recency decides,
  with no attempt to read the stored date at selection.
