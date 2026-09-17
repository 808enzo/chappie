---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Segment sets and the remainder

Segments rarely live alone. As soon as you have more than one, two questions appear that a
single cut never raised: **who landed in several at once, and who landed in none.**

Nobody asks the second one. People in no segment send no signal. They do not complain and they
do not unsubscribe. They stop receiving anything, and then they leave. Every other failure in
this library shows up somewhere in a report. This one shows up only if you go looking, so the
count belongs in the mechanic rather than in anyone's good intentions.

## Entry conditions

- More than one segment is in use in the same wave or the same period.
- You can count the whole base, not only its reachable part.

## Exit conditions

You have measured coverage, declared the set's discipline, resolved collisions by a written
priority, and given the remainder a named route and a named owner.

## Sequence

**1. Lay the set over the base and measure coverage.** Three shares: people in exactly one
segment, people in several, people in none. Count against the whole base rather than the
reachable base (`list-building`), or people with no working contact disappear from the arithmetic
along with the problem of reaching them.

Then take a fourth count, per wave: members of the set who received nothing from it. A member who
lost every collision to the priority order, a member no channel can reach, and a member held back
by contact policy all count as covered, and each of them received nothing, exactly like an
unnamed remainder. Read this count beside the remainder share. Coverage counts membership, and
this count is what membership delivered.

**2. Declare the set's discipline, once, for the wave.** Two options:

- **Partition.** The groups do not overlap, and together with the remainder, named as a group of
  its own, they cover everyone. Use it when sends go out in parallel and one person could receive
  each of them. Without a named remainder, a partition covers everyone only through a catch-all
  rule, which is an edge case below.
- **Overlapping tags.** A person carries several attributes at once, and each send picks the
  audience it needs. This works only when selection happens one send at a time, in sequence, so
  each send can subtract whoever the previous one took.

The choice is not stylistic. Overlapping tags with parallel sends is the arrangement that
delivers three emails on the same morning to the person who buys across three categories. Teams
discover the distinction on that morning rather than at the planning stage.

**3. Resolve collisions by a written priority order.** Fix it before the wave, not while you
assemble the send. A priority settled per send is a queue of whoever asked most recently.

**4. Merge groups below the readable floor upward** into their parent. Split finer than the base
supports and you get many segments and no conclusions. Two adjacent groups that are each too
small do not become readable by staying apart.

**5. Name the remainder and give it a route.** Three legitimate routes, and the third counts as
a decision rather than a leak:

- **Default content.** What goes out with no cut applied, with an owner assigned to it like any
  other send.
- **An attribute-collection touch.** A send whose purpose is to make these people classifiable:
  ask what they want, or offer choices whose clicks resolve into an attribute.
- **Deliberate exclusion.** With a written reason and a date to revisit.

Only these three. Leaving the remainder unnamed is the failure mode of this mechanic, and it
looks identical to the first three routes until someone counts.

**6. Put the remainder share on a standing count.** Read the direction rather than the level. A
remainder growing cycle over cycle means your definitions are falling behind the base. Several
things produce that, and they need different repairs: new customers arriving with attributes no
rule mentions, a source system that stopped delivering an attribute, or definitions narrowed at
the last review. Check which before you widen anything.

**7. Recompute coverage every cycle.** The base changes faster than the definitions do.

## Thresholds and timings

- **Merge floor.** The same minimum readable size you used when defining the segment. One
  number, applied in both mechanics, or the two will disagree.
- **Priority order.** Fixed before the wave and held for the whole period. Change it mid-period
  and the period's results stop being comparable with themselves.
- **Campaign messages per person per wave.** The ceiling that determines how many parallel cuts a
  set can carry. It comes from contact policy, as whatever the cap in `contact-orchestration`
  leaves for campaign sends in the wave, and this skill does not set it. Work backwards from it: if
  the ceiling is one and the set can produce four sends to one person, the set is wrong, not the
  calendar.
- **Coverage recomputation.** No less than once per program cycle.
- **Revisit date on a deliberate exclusion.** Assign it at the moment of exclusion. Without a
  date the exclusion turns permanent by default, which is a different decision from the one you
  made.

## Edge cases

- **The remainder is the largest group.** Normal at the start, and fine for exactly as long as
  you have named it. Not knowing is the problem. A set covering a minority of the base is a
  first cut rather than a failure, so treat it as one and say so out loud.
- **The remainder is mostly people with no purchase history.** They are a known group rather than
  a remainder, and `rfm-segments` routes them by tenure: people who arrived recently and have not
  had time to buy go to `welcome-and-activation`, and people who arrived long ago and never bought
  get a first-purchase route. No behavior exists yet to build a cut on, and inventing one produces
  a segment defined by absence.
- **One person qualifies for two segments with contradictory offers.** A discount and a raised
  free-shipping threshold reaching the same person on the same day reads as a mistake, because
  it is one. The priority order resolves it, not whoever pressed send first.
- **Coverage looks complete because one segment is a catch-all.** A rule shaped like "everyone
  else" closes the arithmetic without closing the job. Measure coverage without it, then decide
  whether the catch-all is the default-content route under another name. It frequently is, and
  then it needs an owner.
- **The remainder shrank because you widened the definitions.** Not an improvement. Verify
  against response rather than against the share: a wider definition returning the same
  behavior as the base has moved people out of the remainder and into a segment that does not
  separate.
- **Parallel waves for two brands or two markets on one platform.** The sets run independently
  and a person can sit in both. Count collisions between sets as well as inside each one.
  Treating the two as one list is how someone receives the same offer twice with different
  branding.
- **A person moves between segments mid-wave.** Freeze the assignment at assembly time and
  record it with the send. Otherwise the audience you reported is not the audience you reached.

## Failure modes

- **The remainder is named nowhere.** The silent failure: people stop receiving anything, and
  nothing in the reporting changes shape as they go. By the time channel revenue reflects it,
  the population that left is large and old.
- **Default content has become the largest send and has no owner.** Segmentation is formally in
  place, and in practice the base is back on one broadcast, with extra steps and a worse cadence.
- **Someone suspends the priority order for an important launch.** Every launch is important to
  whoever requested it. The second suspension establishes that no priority order exists, and the
  collision counts you planned around turn into fiction.
- **Coverage gets measured against the reachable base.** The figure looks healthy, and the
  people with no usable contact have vanished from view along with the job of re-permissioning
  them.
- **The remainder share rises every cycle and nobody reads it.** The definitions have fallen
  behind the base. The longer this runs, the more of the base is described by rules written for
  a business that no longer exists.
- **Collisions get counted and priority gets applied, and nobody checks who keeps yielding.**
  One group can lose every collision every wave and end up receiving nothing while appearing
  fully covered. The fourth count in step 1 is where it shows.
