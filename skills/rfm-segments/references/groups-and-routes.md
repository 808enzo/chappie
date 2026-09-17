---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# From a grid to groups somebody works

A cut grid is not yet a set of segments. It is a set of cells, and a cell is an arithmetic
result: the people who happened to land where two or three bands cross. Some of those cells hold
enough people to read and some do not, and every one of them is equally easy to name.
Naming them all is the standard failure of this method, and it produces a report with twenty
seven lines that nobody acts on, because acting on a line requires somebody to own it.

This mechanic covers the step from cells to groups: sizing before naming, which axis to merge
along, how a group gets named so the name survives a change of plan, where the group's route
comes from, and the one group the grid cannot produce at all.

## Entry conditions

The axes are cut (`cutting-the-axes.md`).

## Exit conditions

A named set of groups. Each one is above the readable floor, has one owner and one route. Every
person in the base sits in exactly one group. The people with no purchase history are named as a
group and split into the two populations inside it.

## Steps

**1. Size the cells before giving any of them a name.** Cells below the minimum readable size
(`segmentation`) get merged. Merging is the normal outcome rather than the exception: the number
of bases that can carry twenty seven readable cells is small, and knowing whether yours is one of
them takes one count.

**2. Merge along the axis that separates least, not along the one that is easiest to explain.**
Money attracts the easy explanation, because its labels read as obvious. The right merge is
decided by which axis makes the least difference to the target metric, which is the same
separation test that decided whether to carry the axis at all.

**3. Name a group by the state it describes, not by the verdict you have in mind.** "Two
purchases, the last one inside one interval" survives a change of plan. "To be reactivated" does
not: it fixes the action inside the name, and when the action changes the group gets renamed,
which ends the comparability of every number attached to it. It also quietly turns the group set
into a plan of work, and the plan of work is a roster owned by `scenario-map`.

**4. Give each group one route, and take the content of that route from whoever owns it.** Winning
back people who used to buy is `lapse-and-winback`. Moving somebody from a first purchase to a
second is `repeat-purchase`. The offer and what it costs belong to `offer-design`, and the words
belong to `email-copy`. You decide here which group exists and who is in it, and nothing about
what it hears. The published tables merge those two decisions into one line per cell, which is
why they read as configuration.

**5. Split the no purchase bucket by tenure rather than by silence.** Two populations sit in it
and they look identical from the purchase side, because neither has bought:

- people who arrived recently and have not had the time yet;
- people who arrived long ago and never did.

The boundary is your own median time to first purchase, computed on the people who did buy.
Below it, they belong to the welcome mechanic (`welcome-and-activation`) and they are not in RFM
at all until a first purchase exists. Above it, they are a group of their own: reachable, holding
a basis, and never converted, and their route is a first purchase route. A winback offer to
somebody who never bought reads to the recipient as a mistake, and it is one.

**6. Check the set covers everybody once.** RFM is a partition by construction only once the no
purchase group is part of it; without that group the arithmetic looks complete because the cells
add up, while a population with no value on any axis sits outside the count. The partition
discipline itself is `segmentation`'s.

**7. Write each group's definition in the six parts `segmentation` requires, plus the two this
method adds:** the direction of the scale, and which axes were read live at selection versus
taken from the last recompute (`recompute-and-transitions.md`). Two teams reproducing one group
from a definition without those two parts will produce different people and both will be
following the definition.

**8. Give every group an owner** (the ownership map in `crm-program-design`). A group with no
owner produces a line in a report, then produces it again next cycle.

## Thresholds and timings

- **The floor for a group** is `segmentation`'s minimum readable size, derived from your own
  response rate and variance. This skill does not redefine it and adds only where it applies:
  to the group after merging, not to the cell before it.
- **How many groups to start with: as many as there are routes somebody can run.** A starting
  point. It applies where each route has a named owner who reads it. Replace it once you know how
  many routes your team gets through in a cycle, and take the number from that rather than from
  the number of cells the grid produced.
- **The tenure boundary inside the no purchase bucket:** your own median time to first purchase,
  computed on people who bought, in arrival cohorts old enough to have finished buying. A cohort
  younger than the boundary you are estimating cannot show its own late buyers, so the median comes
  back short and the boundary moves people out of the welcome mechanic early. A parameter of your
  data. Recompute it when the acquisition mix changes, because a channel that delivers slower buyers
  moves it without anything else moving.

## Edge cases

- **A group clears the floor and is still larger than one person can work.** Same answer as the
  roster: the set is bounded by whoever works it (`scenario-map`), and the bound is a question
  rather than a number.
- **Two groups end up with the same route.** Merge them, or say out loud what differs. Two groups
  on one route report separately and behave as one, which makes both readings weaker than the
  pooled one would have been.
- **The best group is the smallest and the money sits in the middle.** An ordinary distribution.
  Size the effort by what a group can produce rather than by what it is called.
- **A person's RFM group and their engagement tier disagree**: bought last week, has not opened
  an email in a year. Two different objects. The tier belongs to `email-program` and describes the
  channel; the group here describes purchasing. Neither overrides the other, and the decision
  about the send itself is `contact-orchestration`'s.
- **Never purchased and unreachable.** Not a marketing group at all. What happens to the record
  is `list-building`'s decision, and carrying those people inside a group here inflates its size
  and depresses everything measured on it.
- **A group loses its owner mid cycle.** Before the cycle ends it gets a new one or it leaves the
  set. An unowned group keeps sending, which is the part people forget while treating it as a
  staffing question.
- **The grid produces a cell that is large, readable and meaningless**, because it is where two
  wide bands cross. Splitting it is a boundary decision, not a merge decision, and it goes back to
  `cutting-the-axes.md`.

## Failure modes

- **All twenty seven cells were named and none were merged.** The signal is a count of groups
  below the readable floor that nobody made, plus a report nobody opens. The cost is not the
  report: it is that a number read on an unreadable group still gets used in an argument.
- **The no purchase bucket received a winback message.** The recipient is being asked to come
  back to something they never did, and they can see that. It is caught by reading the group
  definition rather than the campaign.
- **Group names are verdicts.** The signal is renaming every planning cycle, after which no two
  cycles can be compared and the history of the group is gone.
- **Everybody is in the middle group.** The bands are too wide, or the axis does not separate.
  Both repairs are in `cutting-the-axes.md`; nothing in this file will fix it, and merging further
  makes it worse.
- **The set was built from the cells that had interesting names.** The signal is coverage well
  below the whole base and nobody able to say who is outside it.
