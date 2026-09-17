---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# Building one segment

A segment is a rule you apply again, not a list you exported once. So this mechanic ends with a
written definition someone else can reproduce, not with a file of customer ids. If the only
artifact is the file, you are holding a snapshot of a base that has already changed.

## Entry conditions

- A job exists that requires treating part of the base differently from the rest.
- Attributes are available at the level of a person, not only as aggregates. A report telling
  you what share of the base is young does not let you address them.

## Exit conditions

The definition is written down, you have counted the size, you have set a recompute cadence, the
behavior for a missing value is stated, the rule has passed the three checks at the end of step 4,
and you have named the condition for retiring the segment. Deciding not to build the segment is a normal outcome of steps 1, 2 and 6.

## Sequence

**1. Start from the decision, not from the attribute.** Name what changes for a person who lands
in this segment: a different offer, a different channel, a different rhythm, or exclusion from a
send. No decision means no segment. A cut that no action depends on is a reporting breakdown,
and it belongs to `crm-reporting`.

Attribute-first is the common failure, and it looks productive: the data holds gender, someone
splits on gender, and nothing downstream changes. Ask what the two halves would receive. If the
answer is the same thing, stop here.

**2. Count what you hold, and how full it is.** For each candidate attribute, take the share of
the base carrying a value. Fill rate is its own quantity, and it almost always comes in lower
than people assume, because teams reach first for the attributes that sit in optional fields. An
attribute filled for a minority does not give you a segment. It gives you a pilot, and the
honest move is to call it one.

**3. Choose the attribute's provenance deliberately.** Three kinds, each with its own weakness:

- **Declared.** The person told you. Accurate about intent, sparse, and it goes stale in silence:
  someone picked their interests once and has changed since.
- **Derived.** Computed from behavior when it is read. Fills much wider, and it survives a wrong
  declared value. It misreads shared accounts, and it goes empty once the events behind it age
  out of retention.
- **Computed.** Recalculated by the platform on a schedule and stored. Fills as wide as the data
  behind the calculation reaches, which is not automatically wider than a derived attribute: a
  score built from purchase history is empty for everyone whose history is shorter than the
  window it needs. Needs a schedule, and freezes without warning when the job fails.

`martech-stack` calls both of the last two a derived attribute, computed on read or stored. Keep
them apart in the definition, because they fail in opposite directions: one empties, the other
freezes.

Prefer derived when the declared value would be optional. Prefer declared when the attribute is
about intent rather than behavior, because behavior cannot tell you what someone is shopping
*for*. Mixing them is normal, so use declared where present and fall back to derived, but write
the fallback order into the definition.

**4. Write the definition as a rule.** Six parts, and people skip the sixth:

1. the attribute;
2. the operator;
3. the threshold;
4. the observation window;
5. the source system that owns the value;
6. **what happens when there is no value.**

The missing-value branch is part of the rule rather than an edge case. Leave it unstated and
each system resolves it its own way: one treats absent as "does not match", another as "unknown,
include", and the same definition then returns two different populations depending on where it
ran.

Three checks from `consent-and-preferences` apply before the rule runs for the first time. An
attribute on a field the purpose register does not name gets its register line first. No part of
the rule may name a special category, or a proxy that a reader of the definition would take for
one. A marketing segment reads the person's objection field before it selects, so a person who
objected leaves the segment and is not selected again.

**5. Express the threshold against your own distribution.** A percentile of the base, a fraction
of average order value, a multiple of the median interval between purchases. Never an absolute
sum and never a calendar period. Use an absolute only where a channel or a law dictates it, and
then say which.

The reason is portability. "Customers who spend a lot" written as a fixed amount stops being
true the moment prices move, and it was never true across categories.

**6. Count the size before you build it.** Run the rule as a count first, against the reachable
base rather than base size: records you can no longer reach still satisfy the rule, and they
inflate every count they enter. The difference between the two belongs to `list-building`. If the
group comes in smaller than what has produced a readable response in your own history, the cut is
too fine: widen the window, move the threshold in whichever direction admits more people, or
merge it into a neighboring segment. Read the direction off the operator: a spend rule admits
more people when the amount comes down, a recency rule when the day count goes up. Build it
anyway and you own a segment you can send to and cannot learn from.

**7. Set the recompute cadence from how fast the attribute moves**, not from what is convenient
to schedule. An attribute that changes faster than it recomputes describes yesterday's person,
and it does so invisibly.

There is a ceiling on this from underneath. Where the attribute is built from events, the
recompute cannot be more frequent than the freshness class of those events: the class is how long
after the action the event becomes visible to selection, and a recompute that runs ahead of it
reads a person who has not arrived yet. `martech-stack` owns the class and writes it beside the
event; what belongs here is checking it before you name a cadence.

**8. Name the retirement condition now.** State what would have to be true for this segment to
stop earning its maintenance. A condition you invent at build time gets written down. A
condition left for later never gets invented, which is why segment counts only ever rise.

## Thresholds and timings

- **Minimum readable size.** The smallest group that has produced a response you were willing to
  act on, derived from your own response rate and your own variance. It is a property of your
  base, and nobody can hand you the number.
- **Fill-rate floor.** The share of the base carrying the attribute, below which you declare the
  cut a pilot and keep it out of the regular set. Set it once, apply it to every candidate.
- **Three recompute cadences**, matched to volatility:
  - static attributes, meaning captured facts that do not change on their own: write them at
    capture;
  - calculated metrics such as average order value, purchase frequency and favorite category:
    recompute no less often than the sends that select on them run, and no more often than the
    purchase records behind them land (step 7). Once per day is a starting point, not a property
    of the method: it fits a base whose purchase records land at least daily and whose sends
    select no more than daily, and you revise it when either of those changes;
  - behavioral events such as a view, a basket addition or a session: as close to the moment as
    the stack allows, because a same-day segment built on yesterday's events is wrong about
    exactly the people it exists to catch.
- **Observation window.** A multiple of the category's median interpurchase interval, never a
  calendar period. The same rule then yields days in a weekly-purchase category and months in an
  annual one, which is the point of writing it that way.
- **Boundary revision.** Triggered when the underlying distribution shifts, not when the segment
  shifts. Rising average order value moves everyone up, and boundaries fixed against the old
  distribution then reclassify people in silence: nobody edited the rule, so nothing in the
  interface marks the day the groups stopped meaning what they meant.
- **Declared-attribute shelf life.** The age past which asking again costs less than being
  wrong. Set it per attribute: a stated size changes rarely, a stated interest changes fast.

## Edge cases

- **The attribute is filled for a minority.** Do not build the segment. Build the mechanic that
  fills the attribute: a question in the signup form, a send whose links map to different
  interests, separate capture points per topic. The collection belongs to `list-building`, and
  you specify the reason to collect here, because only the intended cut knows which attribute is
  missing.
- **One account, several people.** A household card, a shared address, a workplace login. The
  declared attributes then belong to the wrong person systematically, and no threshold repairs
  that. Derive from the composition of purchases instead, and accept that some share of the base
  will not divide on that attribute at all. Saying so beats a confident wrong split.
- **A declared attribute nobody revisits.** Give it a shelf life and a reason to ask again.
  Without one, the segment fills up with people it once described accurately.
- **The base is too small to cut.** Then segmentation is not the first job, inflow is. Splitting
  a small base yields groups you cannot conclude anything from, while producing the appearance
  of sophistication.
- **The attribute lives in one system only.** A cut you cannot reproduce where the sending
  happens has to be assembled by hand every time, and hand-assembled segments diverge from their
  own definition without anyone noticing. Either move the attribute or change the cut.
- **A seasonal business.** The activity window runs wider than blended frequency suggests. A
  customer who buys twice a year has not lapsed in month four, and a window derived from an
  average files them as lost.
- **A long consideration cycle.** The conversion arrives after the reporting period closes. Judge
  the cut on an intermediate response, and write down that you are doing so. An intermediate
  metric borrowed in silence ends up treated as the target metric, and by then nobody remembers
  it was a stand-in.
- **A B2B base where the account is the unit, not the person.** Decide which one the segment
  describes before you write the rule. A definition that mixes them returns accounts when you
  count and people when you send.

## Failure modes

- **The number of segments grows and the sends do not change.** The cuts exist in the interface
  and not in the work. This is the most common outcome, and from the inside it does not look
  like a failure, because activity is visible and inaction is not.
- **The definition lives in one person's query.** Test it: ask someone else to assemble the same
  segment from the written description. If the two populations differ, you have a habit rather
  than a definition.
- **One name, two meanings.** "Active" in the report and "active" in the send come from
  different rules. The argument about the numbers never resolves, because both sides are right
  about different people. Check the definitions before you check the data.
- **Someone rebuilds the segment by hand before each send.** It will diverge from the written rule,
  and nobody will be able to say when that started, because no earlier version exists to compare
  against.
- **Someone chose the attribute because it exists.** A split that changes nothing downstream
  costs as much to build and maintain as one that does, and it occupies the slot where a working
  cut would have gone.
- **Nobody wrote the missing-value branch.** The symptom: the same definition returns different
  counts in two systems, and the gap is about the size of the population carrying no value.
