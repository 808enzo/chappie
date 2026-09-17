---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Ownership, team shape, and where the promo budget goes

Split a team by task and you get people who are busy. One person runs manual sends, another runs
automated ones, a third helps out. Every number in the program then belongs to everyone, which
means nobody plans its movement, because planning it is not anyone's job.

This mechanic covers how each number gets exactly one person, why the split runs along lifecycle
stages rather than along task types, what happens where two owners reach for the same person, who
carries the infrastructure work, what a program looks like at one, two and three people, and how
the promo budget is divided.

## Entry conditions

The goal and the key results are named (`program-goals-and-metrics.md`).

## Exit conditions

An ownership map: one person against every metric and every segment. A named infrastructure owner,
separately. The promo budget split across segments. A written rule for who yields where two owners
overlap.

## Steps

**1. List everything the program answers for.** The target metric, the key results, the balancing
metrics, the leading metrics, plus the live mechanics if the program is not starting from scratch.

**2. Give every metric exactly one owner, a person rather than a team.** A metric owned by everyone
gets reported and does not grow.

**3. Split the work by lifecycle stage, not by task type.** A task split puts a person in front of
an operational queue and leaves the number unclaimed. A stage split ties a person to a number.
Set the boundary between two stages by a rule rather than by feel: the construction of the cuts
belongs to `segmentation`, and the silence and lapse thresholds to `lapse-and-winback` and
`list-building`.

**4. Attach a segment to each owner, not the whole base.** While everyone works the whole base,
offers from different owners land on the same person and cannibalize each other, and afterwards
nobody can establish whose result it was.

**5. Decide in advance who yields when two owners reach for the same person.** Write the rule by
stage: a person belongs to the stage they are in now. Where the overlap is deliberate, a joint
mechanic on the boundary between two stages, name in advance whose metric measures it.
A collision between two messages at send time is not this: that is `contact-orchestration`.

**6. Name an infrastructure owner separately.** Integrations, monitoring, technical debt, taking
apart what broke. While nobody holds that role, whoever owns a metric does the infrastructure
work, and growing the metric gets whatever time is left. If you cannot staff the role, account for
it when you size the cycle rather than discovering it at the end of one.

**7. Fit the program to the team on hand, and name the model out loud.**

- **One person.** The ownership map does not disappear; it becomes the list of what is deliberately
  not being worked on this cycle, each line with a date to revisit. Without that list, one person
  owns everything and moves nothing.
- **Two people.** The first takes intake and the first weeks. The second takes the active base and
  winning people back.
- **Three people.** The third takes revenue growth on the active base.
- **Work arrives from other departments and priorities are set above you.** That is a service
  model. Split the operational stream from the project stream between people, and accept that the
  program's metric here is delivery time and quality, not growth.

**8. Split the promo budget from the gap, not evenly.** At the start of the period, forecast how
many people come back on their own, with no promotion; the share comes from your own history. The
gap between that forecast and the goal is what the budget is for. Then fund the segments in order
of what a result costs in each, cheapest first, and fund winning back lapsed people from what
remains. Start from the assumption that a returned lapsed person is the dearest result you buy,
because money spent there first is money the cheaper segments do not get, and hold that
assumption only until your own arithmetic replaces it: divide last period spend per segment by
results in that segment, and take the order from that. Discount depth and the economics of the offer belong to `offer-design`.

**9. Agree the plan over a horizon longer than one launch.** Check segments and offers from
different owners against each other before anybody builds anything. Otherwise the overlap surfaces
at send time, where the only remaining tool is suppression.

**10. Re-read the map when the team changes.** Someone leaves and their number is nobody's. That is
a program event rather than a staffing question: before the cycle ends, give the metric a new owner
or move it into the observed, and write down which you did.

## Thresholds and timings

- **One owner per metric.** A construction, not a number. A second owner means that when the two
  disagree, the decision is made by someone other than the person answerable.
- **The shapes at one, two and three people** are constructions too. They say what splits first as
  a second and third person arrive, not how many people a program needs.
- **Planning horizon:** longer than the longest launch inside it, measured from your own launches.
  Until you have that measurement, start with a plan two weeks ahead, revisited weekly. That holds
  for teams where a launch takes days. Once you know your own longest launch, take the horizon from
  it instead.
- **Budget:** forecast at the start of the period, the gap to the goal is the budget's job,
  segments funded in the order of what a result costs in each, winning people back from the
  remainder. The order is computed from your own spend and results, not taken from this text.

## Edge cases

- **One person for the whole program.** The map becomes a list of what is not being done this
  cycle, with a return date against each line.
- **Service model.** The program executes requests from other departments and does not own growth.
  A growth goal here fails by construction, because the lever belongs to the requester. The
  program's metric is delivery time and quality, and that is said before goals are set, not after
  they are missed.
- **An owner who cannot move their metric.** The lever sits with product, price or logistics. While
  there is neither a lever nor a change of metric, the ownership exists only on paper, and at the
  review it looks like a person performing badly rather than a decomposition that was wrong.
- **The overlap is deliberate.** A joint mechanic between two owners: name whose metric measures it
  in advance. Otherwise both count the success and neither counts the failure.
- **The budget belongs to another department.** The program plans in requests rather than in money,
  and prices each request in its own metric. Otherwise the gap gets calculated and there is nothing
  to close it with.
- **The team changes mid cycle.** Cycle goals are not rewritten around a new person; the ownership
  map is. Rewrite the goals instead, and two cycles later the program holds no comparable pair of
  numbers to read the change against.

## Failure modes

**The team is reorganized before the metrics are named.** The signature: the same people under new
titles, and the numbers exactly where they were. What to do: stop the reorganization and go back to
`program-goals-and-metrics.md`. Structure is built for metrics that already exist. In the other
order it is cosmetic, and the tell is that after the change nobody can say whose number moved.

**Ownership goes to teams rather than to people.** The signature: every metric has an owner
on paper, and every discussion of a miss ends in a discussion of process. What to do: put a name
against each number. Where you cannot put a name against it, nobody owns the metric, and saying so
is worth more than a map that claims otherwise.
