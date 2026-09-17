---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Vocabulary of the grid

Terms all three mechanics assume. Four of them are words other skills use for something else, and
this file separates those at the end.

The general construction of a segment, its definition, fill rate, readable floor, recompute
cadence and remainder, belongs to `segmentation` and is not restated here. Below is only what
this method adds on top of it.

## The grid

**Axis.** One of the three dimensions: time since the last purchase, number of purchases, money.
An axis is not a segment. A segment appears where bands on several axes cross.

**Band.** A range of values on one axis that has been given one value of the scale.

**Direction of the scale.** Which end of the scale holds the best value: the first or the last.
Both conventions are in use and they are mirror images. Write it into the group definition, and
never print a code without its legend.

**Cell.** The intersection of one band per axis. The unit of the grid and not the unit of work.

**Group.** One cell, or several merged cells, that has a name, a size above the readable floor,
an owner and a route. The unit of work.

**Quantile cut.** Bands of equal size. Answers where a person stands relative to everybody else;
holds sizes steady and lets the meaning move as the distribution shifts.

**Business fact cut.** Boundaries placed at named values: one purchase cycle, a shipping
threshold, a subscription term. Holds the meaning steady and lets the sizes move.

## Your own numbers

**Own interpurchase median.** The median gap between consecutive purchases, computed on people
with two or more purchases. Both the recency boundaries and the starting cadence come from it.

**Time to first purchase.** The median time from a record appearing to its first purchase,
computed on the people who bought. It splits the no history bucket.

**No history bucket.** People with zero purchases. They hold no value on any axis, so the grid
cannot place them. Split by tenure into people who arrived recently and people who never
converted, and the two have different routes.

## Freshness and movement

**Live axis and snapshot.** A live axis is read at the moment of selection; a snapshot is the
result of the last recompute. The class belongs to an axis together with the place it is computed
rather than to the axis by itself: recency is live wherever you can reach the last purchase date
at selection, frequency and money are live wherever the store answers at selection. One group can
carry axes of both kinds, and which is which is part of its definition.

**Deciding axis.** The axis whose band the group's route depends on: recency for a winback group,
frequency and money together for a group of second time buyers with a rising order value. Name it
in the group definition. Where several axes decide, **the group takes the worst freshness class
among them**, and counts as live only where every deciding axis is live. That is the freshness
question answered in one line of a definition, and the control metric counts against that line
rather than against the group as a whole.

**Recompute stamp.** The time of the last recompute, carried by every export and every audience
built from a group. A result read against a group with no stamp cannot be attached to the people
who produced it.

**Transition.** A person changing group between two readings. An occasion a mechanic can fire on,
not a line in a report.

**Boundary movement.** A change in a group's size caused by the boundary shifting rather than by
people moving. Possible whenever the axis is cut by quantile, since the band is defined relative
to a distribution that moves.

## Four words this skill shares with neighbors

**Segment.** In `segmentation` it is a rule for selecting people. A group here is such a rule and
inherits that construction whole: the six part definition, the fill rate, the readable floor, the
recompute cadence. This skill introduces no second word for it and no second construction.

**Separation.** The control metric of `segmentation`: the difference in the target metric between
a segment and the rest of the base, both counted on the reachable base and read under the same
treatment. This skill uses that same test to decide whether an axis earns
its place in the grid and which axis to merge along. It is borrowed, not redefined.

**Recency.** Here it is the axis, counted from the last purchase. In `email-program` an engagement
tier is counted from response in the channel. In `list-building` silence is counted across every
channel against the purchase cycle. Three clocks, three different populations at any moment, and
the word alone does not say which report you are reading. Somebody can be recent by purchase and
dormant by engagement at the same time, and both readings are correct.

**Owner.** Here it is the person answerable for a group and its route. `crm-program-design` holds
the full list of what the word names elsewhere in the library, and the sense closest to this one
is a row's owner in `scenario-map`: one person holds both in a small program, and they are named
apart because a group with nobody in it and a mechanic that never fires are different problems.
