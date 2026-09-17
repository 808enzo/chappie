---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-05
---

# Segmentation vocabulary

The terms the three mechanics assume. These definitions are scoped to this skill. The general
dictionary of marketing metrics, with formulas and denominators, belongs to `metric-definitions`.

The word *segment* means different things to different people in the same meeting. Settle it
before the rest of the conversation.

## Segment

A rule for selecting people, not the people it selected. The list is the rule's output at the
moment it last ran, and it is stale as soon as it exists. Everything in this skill follows from
that distinction: you can reproduce, review and retire a rule, and you can only re-export a
list.

## Segment definition

The written form of the rule. Six parts: the attribute, the operator, the threshold, the
observation window, the source system that owns the value, and the behavior when there is no
value. People leave out the sixth part, and its absence is why the same definition returns
different populations in different systems.

## Attribute

A value held at the level of one person, on which you can make a cut. Three kinds by provenance:

- **Declared.** The person stated it. Accurate about intent, sparsely filled, and it goes stale
  in silence.
- **Derived.** Computed from behavior when it is read. Fills more widely and survives an
  inaccurate declared value. It misreads accounts shared by several people, and it goes empty
  once the events behind it age out.
- **Computed.** Recalculated by the platform on a schedule and stored. Fills as wide as the data
  behind the calculation reaches, requires a schedule, and freezes without any signal when the
  job fails.

`martech-stack` calls both of the last two a derived attribute, computed on read or stored.

Provenance is not an implementation detail. It determines the attribute's failure mode, and the
failure mode determines what the segment does wrong when it goes wrong.

## Fill rate

The share of the base for which a given attribute holds a value. Its own quantity, measured
separately from the size of any segment built on it. An attribute with a low fill rate cannot
support a segment for the whole base however you set the threshold. It can only describe the
part of the base it happens to describe.

Counted on people, and on the base. `personalization` takes the same quantity and counts it on the
population receiving one message, which gives a different answer for people who arrived yesterday,
and it keeps a separate number of its own, the **resolved share**, counted on evaluations of a
place rather than on people. Fill rate says how many people hold a value; resolved share says how
many evaluations of one place got one. Neither substitutes for the other.

## Set coverage

The share of the base falling into at least one segment of a set. Measured against the whole
base rather than the reachable base (`list-building`), so that people with no working contact
stay visible in the count.

Coverage counts membership, not receipt. A member who lost every collision, cannot be reached, or
was held back by contact policy is covered and received nothing. That count is taken per wave
and read beside the remainder share.

## Remainder

The people falling into no segment of the set. You name it explicitly, give it a route (default
content, an attribute-collection touch, or deliberate exclusion with a revisit date), and count
it every cycle. An unnamed remainder receives nothing, indefinitely, without producing a single
signal that it is happening.

## Partition and overlapping tags

Two disciplines for a set, chosen deliberately and declared before the wave:

- **Partition.** Groups do not overlap, and together with the remainder, named as a group of its
  own, they cover the base. Required when sends go out in parallel and one person could receive
  several.
- **Overlapping tags.** A person carries several attributes at once. This works only when
  selection happens one send at a time, so each send can subtract the audiences already taken.

## Minimum readable size

Also called the **readable floor**. The smallest group whose response you have historically been
willing to act on, derived from your own response rate and your own variance, and counted against
the reachable base (`list-building`). It sets the floor for building a segment and the trigger for
merging one. It is a property of a particular base: the same figure is generous for one and
meaningless for another.

## Observation window

The span of history the rule reads to evaluate its attribute. A multiple of the category's
median interpurchase interval, never a calendar period. `experiments-and-holdouts` says *outcome
window* for the span in which a test counts results, which is a different span.

## Recompute cadence

How frequently the rule gets applied again. Set it from how fast the attribute moves, not from
what is convenient to schedule. An attribute that changes faster than it recomputes describes a
person who no longer exists, and reports nothing unusual while doing so. It has a ceiling from
underneath: an attribute built from events cannot recompute more often than the freshness class
of those events (`martech-stack`).

## Drift

Change in a segment's membership while its definition stays fixed. Ordinary in a moving base.
Read it against that segment's own historical spread rather than a shared threshold, since a
volatile cut and a stable one drift at different rates. A segment rebuilt by hand that no longer
matches its written rule has not drifted. It has diverged from its definition, and that is a
failure.

## Separation

The difference in the target metric between a segment and the rest of the base, with both sides
counted on the reachable base and read under the same treatment, over the target metric's own
window, one value per review cycle. **The control metric of this skill.** It answers whether the
cut carries information at all.

Each condition closes one way to misread the number:

- **The rest of the base.** The whole base contains the segment, so a difference against it
  shrinks as the segment grows. A teaching example: a base of 10,000, a segment of 8,000
  responding at 5% and the other 2,000 at 1%. The whole base responds at 4.2%, so the segment
  sits 0.8 points above the whole base and 4 points above the rest. Against the whole base, this
  cut shows a fifth of its real difference.
- **The reachable base.** Records no channel can reach receive nothing the segment changes.
- **The same treatment.** A difference read after each side got its own send measures the send
  along with the cut, and an exclusion segment separates by construction.

Separation has no citable benchmark and will not be given one: it is a property of a specific
base and a specific job, so no market figure exists for it to have. Measure it against your own
history, eight to twelve review cycles, median and spread, and read later values against that.

## Boundary population

The people crossing a segment's boundary in and out from cycle to cycle. A large share means the
boundary runs through the dense part of the distribution, where small movements flip membership.
It is a signal about the boundary, not about the people.

## Exclusion segment

A cut you use to withhold a send rather than to target one. You verify it differently from every
other segment: against the same people, selected by the same rule, who did receive the send. Its
cost side shows up in the channel invoice and its revenue side stays invisible unless you run
that comparison.

## Terms that belong to neighbors

Named here so that nobody redefines them by accident:

- **RFM groups and behavioral scores.** `rfm-segments`.
- **Engagement tiers** (active, occasional, dormant, suppressed) and the engagement window
  behind them. `email-program`. A tier belongs to a channel program, not to the base.
- **Suppression list**, the technical and legal hold on sending to an address. `deliverability`
  and `consent-and-preferences`.
- **Cohort**, a group defined by when people entered and followed over time. An analytical unit
  rather than a targeting rule: `crm-reporting`.
