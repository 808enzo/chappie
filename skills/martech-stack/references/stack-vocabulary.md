---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Vocabulary of the stack

Terms all three mechanics assume. Two of them are words other skills also use for something else,
and this file separates those at the end.

## Facts and the systems that hold them

**Owning system.** The one system where a fact comes into existence and where it is edited. Every
other system holds a copy. Ownership is decided by where the fact arises, not by which system is
oldest or largest.

**Copy.** The value of a fact in a system that does not own it. A copy is read and not edited, and
it carries two things: what it is for and how it refreshes. A copy missing either of those is the
raw material of an argument rather than data.

**Register of facts.** The table of fact, owning system, who may write it, what the copy is for,
and how the copy refreshes. It is the document that settles a disagreement between two systems,
which is what it has to be current for.

**Field format.** How a system stores a value: enumeration, number, date, boolean, free text.
Chosen before the first load, because changing it later means removing the field and declaring it
again everywhere it is referenced.

**Data flow.** One route: source, transport, destination, object, schedule. The unit of the
diagram and the unit of a migration, which is why a flow is cut over whole rather than in halves.

## Events

**Event.** A recorded action by a person, carrying a name, the moment it happened, its properties,
a freshness class and a retention window. Here an event is the record. What it becomes for a
message is `triggered-messages`.

**Event property.** A value attached to an event and read by a named mechanic. A property with no
reader comes off the plan.

**Event plan.** The list of events with their names, firing moments, properties, consumers,
freshness classes and retention windows. Written before the first event is captured, because those
entries are decisions rather than readings, and none of them is recoverable from the data
afterward. The one exception is the delivered freshness class, which is measured on the test
extract and written back into the plan.

**Freshness class.** How long after the action the event becomes visible to selection. Two:
**immediate**, where the mechanic acts while the intent is alive, and **periodic**, where the
decision holds for days. Every event carries the class twice, because the two answer different
questions: the **needed** class comes from the decision the event feeds, the **delivered** class
from the transport that carries it. A consumer cannot run faster than the delivered class, and a
consumer that tries fails silently rather than erroring.

**Event retention.** How long an event stays available for selection. Set separately from the
retention of a person's record, and on any segment that reads events the shorter of the two
windows is the one that applies.

**Derived attribute.** A value computed from events, such as bought in this category. Either
**stored**, in which case it outlives the events and carries the date it was computed, or
**computed on read**, in which case it disappears when the events age out. Until the retention
window passes, the two are indistinguishable from the outside.

**Impossible states.** The list of things that cannot happen in the product, such as the third step
of a registration with no second step. One of them appearing in the data means a flow is wired
wrong, and the list is the cheapest check that finds it.

## Verification and change

**Reconciliation.** Comparing the same counts on both sides of a flow. How you learn that a
transfer has broken before a recipient does. Read per flow, and no sooner than the freshness
class of the slowest fact in that flow.

**Test extract.** A deliberately small export used to check a new flow before anything reads it:
a first pass of a few dozen records for names and presence, a second on the order of a thousand
for values, fill rates and damage.

**Cutover.** The moment a flow starts running on the new platform and stops running on the old
one. The unit of a migration. **`loyalty-program-launch` uses the word for an interval**, the four
stages of moving a loyalty program from an old construction to a new one; one program cutover in
that sense contains many cutovers in this one.

## Two words this skill shares with a neighbor

**Event.** Here it is the record: name, properties, freshness, retention. In `triggered-messages`
it is the occasion that starts a message, with its own eligibility filter and delay. The same word for two
different objects, tied together by one rule: a trigger cannot run faster than the class its
source delivers.

**Retention.** Here it means how long an event stays queryable. In `list-building` it means which
storage tier a person's record sits in and what survives removal from the active base. The two
windows are set separately, and on any segment reading events the shorter one wins.
