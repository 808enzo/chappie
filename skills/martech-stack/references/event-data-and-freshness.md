---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Events: the plan, the freshness class, and what outlives the event

An event is not a trace the system leaves behind. It is a product with a name, a shape, a delivery
time and an expiry, and every one of those four is a decision somebody has to make before the
first event is sent. Skip the decision and you collect events nobody
reads, and the only way to find out which ones those are is to go through them one at a time
later.

This mechanic covers what you record about an action, how you name it, how long it takes to become
visible, how long it stays visible, and what happens to an attribute derived from it once it is
gone.

## Entry conditions

The program needs to react to what people do, not only to what they are.

## Exit conditions

An event plan: each event with its name, the moment it fires, its properties, the mechanic that
consumes it, both freshness classes (the one its decision needs and the one its transport
delivers), and its retention window. A decision recorded for every derived attribute: stored, or
computed on read.

## Steps

**1. Write the plan before the first event is sent.** One row per event: the name, when it fires,
the properties it carries, the mechanic that reads it. **An event with no consumer does not get
built.** This is the same rule as the attribute plan in `list-building` and it holds for the same
reason: collected and unread costs storage, slows recomputation, and buries the events somebody
does need.

**2. Name an event by what the person did, not by where the code sits.** One action gets one name
across the site, the app and the register. Two names for one action are two events, and every
segment reading one of them is wrong by the size of the other. A name built from what the person did
survives a redesign and a change of platform. A name built from a template number or the label on
a button is tied to the thing that changes.

**3. Put into properties what the consumer reads.** Choose a property's format by the same rule as
a field's: enumerable values get an enumeration, free text stays where the value is open.
A property nobody reads comes off the plan rather than staying on it for later.

**4. Give every event a freshness class twice: the class its decision needs, and the class its
transport delivers.** Two classes, and both entries use the same pair of names:

- **Immediate.** The mechanic acts while the intent is alive: inside the session, inside the
  choice, inside the delivery window.
- **Periodic.** The decision holds for days, and a batch refresh costs nothing.

**The needed class comes from the decision the event feeds.** You buy real time where speed
changes the outcome. Writing the class down is what turns the cases where it does not into a
decision rather than an assumption. Three signals put an event in the immediate class: the
decision cycle is short, one action carries high value on its own, or the personalization has to
be right at the moment the person is active. None of the three present means the periodic class,
and that is an ordinary place for an event to sit rather than a compromise.

**The delivered class is a fact about the transport, and it is established rather than chosen.**
Take it from the owning system and the route between it and the consumer: an owner that exports on
a nightly schedule delivers the periodic class no matter what the mechanic needs. Establish it on
the test extract of step 5, by comparing the moment of the action against the moment the record
became selectable, and write the answer in the plan next to the needed class.

**The rule this produces, and the reason both entries are written down: a segment or a trigger
that reads an event cannot run faster than the class its transport delivers.** Every consumer
checks the delivered class before naming its own delay. Otherwise the failure is silent. A trigger
reading a field that refreshes once a day sends a message about yesterday's state and reports a
successful send.

**Where the delivered class is slower than the needed one, the mechanic does not get to average
them.** The gap is the finding, and it has the same three outcomes as any fact whose owner cannot
keep up (`system-map-and-ownership.md`, edge cases): change the transport, move the ownership of
the fact, or drop the mechanic. Writing only the needed class into the plan is how the gap
disappears, because the consumer then reads its own wish back as a property of the source.

**5. Check that events arrive before anything reads them.** A test extract in two passes. First a
few dozen records, which is cheap and checks that the names and the presence are right.
Then on the order of a thousand, which is where the substance shows up: values, the fill rate of
each property, and three kinds of damage. **Duplicates**, where one action produced two records.
**Anomalies**, values the business cannot produce, such as an order count for one person in a day
that your own process rules out, which points at a technical fault or at a workaround somebody has
adopted, such as staff putting anonymous sales through their own card.
**Garbage**, characters where a value should be.

Alongside the extract, write a list of **impossible states**: things that cannot happen in the
product, such as the third step of a registration with no second step. Finding one of them in the
data means the flow is wired wrong, and it costs less than learning the same thing from a
broken flow in production.

**6. Set event retention, and check it against the depth of your segments.** Event retention is
set separately from the retention of the person's record, and on any segment reading events the
shorter of the two windows wins. The check: take the deepest looking segment you use and compare
its window against how long events are kept. Where the window loses, either lengthen the retention
or rebuild the segment out of something kept longer, such as your own send history. `list-building`
carries the obligation to run this check before a segment is announced; the storage design is here.

**7. Decide, per derived attribute, whether it is stored or computed on read.** An attribute
derived from events, such as bought in this category or average order value this quarter, behaves
in two different ways when the events age out, and until the window passes the two are
indistinguishable.

- **Stored.** It is written down as a fact in its own right, outlives the events it came from, and
  carries the date it was computed. Without that date, nobody can say afterward what the value
  corresponds to.
- **Computed on read.** It dies with the events, and the segment built on it shrinks on the day the
  window rolls past, with no error and no notification.

Neither is the better one: the stored attribute goes stale, the computed one disappears. The
requirement is to know which one you have for each attribute and to write it in the plan.

## Thresholds and timings

- **The test extract goes in two passes, from a few dozen records to about a thousand**, rather
  than straight to full volume. Start at 10 to 100 records to check names, and move to the order
  of a thousand once the names agree. Those sizes are a starting point for any new flow; replace
  them once your own history shows the volume at which damage first appears in your data.
- **The event plan is reread on every release that touches the site, the app or the register.**
  An event does not break on its own. It gets broken by a deployment that did not know somebody
  was reading it.
- **The delivered class is re-established whenever a consumer shortens its delay, and whenever
  the transport under an event changes.** A trigger that moves from daily to hourly has to measure
  again whether its source keeps up, rather than reading the entry written when the flow was
  built.
- **Event retention is checked against a segment before the segment is announced**, not after its
  first empty run.

## Edge cases

- **One event, two sources with different properties.** The site knows more than the app. Keep one
  name, declare the extra properties optional, and require every consumer to have a defined behavior
  when the property is empty. Splitting the name by source is how you get two events and half a
  segment.
- **The platform computes an event for you, on its own definition.** One shape of this is the
  platform's own rule for when a cart counts as abandoned. Where that definition does not match
  the mechanic, send your own action and build on that instead of bending the mechanic around
  somebody else's constant. Bending it is cheaper exactly once and gets paid for at every later
  revision.
- **The event exists in analytics and not in the sending system.** The report can see it and the
  mechanic cannot. That is not a reporting problem: either the event is created where the mechanic
  reads, or there is no mechanic on it.
- **Retention was shortened without telling you.** A segment stops filling and nobody changed the
  segment. It is found by comparing the current window against the one recorded in the plan, which
  is one of the reasons the plan records it.
- **The event cannot be captured at all.** The source is closed and there is no access. Build the
  mechanic on the nearest event you can capture, and write in the plan what you substituted and
  what it costs you. A silent substitution comes back as an argument later.
- **The event carries data no mechanic needs.** Trim the property at the point of capture rather
  than later. Once it is in the store it lives by the rules of the store, and what you may
  keep is bounded by the purpose you collected it for rather than by what the store allows.

## Failure modes

- **An event was renamed and the segment stopped filling.** A quiet failure: no error, only a zero.
  Compare event counts against the previous period rather than waiting for somebody to complain.
- **Many events collected, few read.** The symptom is rows in the plan whose consumer column says
  something like will be useful. Run the check in the other direction: take the list of events
  being captured and find, for each one, the mechanic that reads it.
- **A property is filled for part of the base and the mechanic assumes all of it.** The message
  goes out with a gap in it, or does not go out at all, and both branches look normal from the
  outside.
- **A field arrives with one value for everybody.** One date of birth across the base, one city
  across the base. It is the signature of a default value being substituted somewhere upstream,
  and it is caught by looking at the distribution of values, not the average.
- **A mechanic depends on a freshness class its source does not have.** The failure is silent: the
  message goes out against a stale state. It has a specific cause worth naming, because the plan
  looks correct while it happens: only the needed class was written down, so the consumer read the
  requirement back as a capability. A cheap check is to compare the moment of the event against
  the moment of the send on a handful of real cases.
