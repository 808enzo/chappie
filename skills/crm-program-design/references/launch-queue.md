---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# The first queue: what gets built when nothing exists yet

A list of mechanics worth having invites an order by how promising each one sounds. Order it that
way and the first three items turn out to need the same missing field, the same integration or the
same decision from a department that has not heard about any of this, and the team waits in front
of a full queue.

This mechanic covers the queue a program cuts before it has a roster: what has to exist before the
first mechanic at all, how you write an item so its cost is visible before build day, why the queue
runs in two lanes, how much you build at once, and when the program stops running its own queue and
starts running the roster's. Once a roster exists and more rows are admitted than can be built,
order among them comes from `scenario-map`, and so does every verdict on a row that is already
live.

## Entry conditions

The goal is named, the owners are named, and the program has no planned roster yet: either nothing
runs, or what runs was never composed on purpose.

## Exit conditions

A queue where every item carries its dependencies. A separate list of blocked items, each with an
owner outside the program and a date. A handover point: the roster `scenario-map` takes over, and
the date the program stops cutting its own order.

## Steps

**1. Check the floor.** Four things have to exist before any mechanic: records you can write to
(`list-building`), a basis to send on (`consent-and-preferences`), somewhere the facts come from
with a known delay before they are visible (`martech-stack`), and a way to read the result
(`metric-definitions`). Whatever is missing is item zero, and the rest of the queue waits for it.
Check the floor before cutting the queue, because an item standing on a floor that is not there
looks cheap right up to build day.

**2. Write every item together with what it needs.** An attribute, an event, a consent, a template,
a change in a system you do not own. An item with no dependency list does not go into the queue.
The taxonomy of dependencies, data, mechanic and promise, belongs to `scenario-map`; use that one
here rather than inventing a second.

**3. Split the queue into two lanes by dependency, not by expected effect.** One lane is what the
team builds with its own hands in the stack it already has. The other is what needs a change in a
system the program does not own. The lanes run in parallel: while an item in the second lane sits
in somebody else's queue, the first lane is being built. The split is by dependency rather than by
duration because duration is known only after the build and the dependency is known before it.

**4. Inside a lane, the goal sets the order, and only while the queue is the first one.** First
goes the item that moves the target metric by the shortest path and can be read soonest. Where two
are equal, take the one whose dependencies already exist. This rule holds for the first pass over
an empty slate, where you have a goal and no roster to read from. From the moment a roster exists,
order comes from `scenario-map` instead: it sorts by firing volume and by dependency, which is
information about rows rather than about the goal.

**5. Do not start a new item until the previous one has been read.** Cap the work in progress at as
many items as there are owners. Otherwise a cycle later there are many live mechanics, none of them
read, and not one can be switched off, because what any of them contributes is unknown.

**6. Test the item on yourself and on colleagues before the first send to customers**, and where
the platform offers it, in a test mode that shows who would have received what and when.

**7. Launch on a slice of the base before the whole base.** Read the response, and read complaints
and unsubscribes beside it: those are the price the item charges the base. Size the slice so the
result is legible; the sizing belongs to `experiments-and-holdouts`. An item that cannot be read on
a slice launches to the whole base with the date of its first read named in advance.

**8. Read the item on its own metric, on the date named beforehand.** Not when somebody gets round
to it: picking the date after launch means picking it while you can already see the result.

**9. Re-cut on the calendar, on the same cycle as the goal revision, and re-cut only what is
yours.** The program re-cuts three things: the goal, the resource envelope behind it, and the
blocked list, where every item either gets a date or leaves the queue. Verdicts on rows that are
already live, keep, rework, merge and retire, belong to the roster review in `scenario-map`, and so
does the route by which an audit finding becomes one. Two of the library's three reviews meet
here: the program reviews what it is for and what it can afford, the roster reviews what runs. The
third, the audit in `program-audit-and-ops`, reads an object and feeds the roster.

**10. Hand the queue over at a test, not at a date.** The program stops being an empty slate the
first time more candidates are admitted than this queue can build in one cycle. That is the entry
condition of build order in `scenario-map`, and using it as the switch means the two skills change
places on the same event rather than on two opinions about when the program grew up. What moves at
the handover is the order, and only the order. **Admission belongs to `scenario-map` from the first
candidate**, empty slate included: every item in this queue is a row that passed the admission test
there, and its occasion, its stated firing volume and its status live on the roster rather than in
a list of your own. What this skill adds to each row, before the handover and after it, is the goal
it serves and the owner who answers for it. What it stops doing at the handover is sorting them.

Write down the date the test fired. An item you drop before building it goes back to
`scenario-map` as a candidate with the reason it was dropped, so that it gets rejected once rather
than re-proposed every quarter. A program that keeps cutting its own order after the handover ends
up with two orders, and the one people follow is whichever was written last.

## Thresholds and timings

- **Work in progress:** as many items at once as there are owners. That is a starting heuristic,
  for a team where each owner reads their own item. Once you know how many items the team reads in
  a cycle, take the cap from that number instead. This is a cap on what is being built, not on how
  many rows may be live at once: the ceiling on the live set is a roster question and belongs to
  `scenario-map`.
- **First read of an item:** no earlier than the point where it has fired enough times for the
  difference to be legible. How many that is comes from `experiments-and-holdouts` and from your
  own data.
- **Slice size for a first launch:** your own, derived from the size at which the result can be
  read.
- **Handover:** the first cycle in which more candidates are admitted than this queue can build.
  Not a count of live mechanics and not a calendar date.
- **Re-cut:** the same cycle as the goal revision, for the same reason. A queue re-cut more often
  than the goals loses its order; re-cut less often, it holds items the goal no longer asks for.
  The roster review runs on its own cycle, set by when rows finish their ramp-up window.

## Edge cases

- **There is nothing to segment yet.** No purchase history, nothing to build cuts on. The queue
  starts with capturing contacts and with service messages; everything that needs history waits,
  and the wait is set by the purchase cycle rather than by a marketer's decision.
- **Every item needs the same missing attribute.** The real first item is that attribute, and its
  owner is outside the program. Until it is named and has a date, do not cut the queue: any order
  you choose is equally unbuildable.
- **A platform migration is under way.** The queue freezes for the cutover window
  (`martech-stack`). Items built on the old platform during it will be built twice.
- **A blocked item is holding the queue.** Move it into the separate list with its external owner
  and a review date, and let the queue continue without it. A blocked item left in the main list
  stops the items behind it in its lane, not only itself.
- **An item that cannot be read on the target metric.** A service message, a brand send, a feedback
  request. Either it has a named metric of its own or it does not enter this cycle's queue: an item
  nobody read gives the roster review nothing to give a verdict on.
- **Everything has to launch by a date.** Lanes do not help when the second lane is longer than the
  time available. Cut the scope rather than the schedule, and let the owner of the goal do the
  cutting rather than whoever is building.

## Failure modes

**The queue grows and nothing gets read.** The signature: the list of live mechanics is longer than
the list of read ones, and the target metric is flat. What to do: stop building, read what is live,
switch off what does not move, and only then go back to the queue.

**The queue was cut by expected effect with the dependencies left out.** The signature: the first
several items are waiting on the same decision somewhere else, and the team is idle in front of a
full queue. What to do: re-sort by dependency without dropping anything. The order changes, the
contents do not.
