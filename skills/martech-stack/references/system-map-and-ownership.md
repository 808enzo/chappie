---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# The system map: who owns which fact

A program runs on facts that live in other people's systems. The order sits in the system that
took the money, the loyalty balance sits wherever the processing runs, the profile sits in the
platform that sends, and every one of them holds a copy of the person. When two of those
disagree, somebody has to be right, and where nobody has decided who, the argument gets
settled by whoever is more senior in the room.

This mechanic covers listing the systems by the job each does, naming one owner per fact,
deciding what gets copied at all, and fixing the formats before anything is loaded.

## Entry conditions

The program uses at least two systems, and at least one fact about a person exists in more than
one of them.

## Exit conditions

A register of facts: each one naming its owning system, who may write it, and what the copies are
for. A diagram of the flows. A written list of what is deliberately not copied into the marketing
stack.

## Steps

**1. List the systems by the job each does, not by the product name.** Six classes recur: the
system of record for orders and money, the customer profile store, the sending platform, web and
product analytics, the support desk, and the point of sale. One product can cover several classes,
and then it appears in the list once per class. The list exists to feed step 2, not to
inventory licenses.

**2. Give every fact exactly one owning system.** A fact is a field or an object the program
uses: the person, the order, the product, the location, a consent, a loyalty balance, an event.
One owner, any number of copies; a copy is read and not edited. The register row is: the fact,
its owner, who may write it, what the copy is for, and how the copy refreshes.

Name the owner explicitly even where it looks obvious. Money and loyalty points sit in the
accounting system in some stacks and in the marketing platform in others, and an assumption here
is the expensive kind: it holds until the day two systems both write, and by then both have
history.

Two consequences of this step reach other skills. A shared store of what has already been sent,
which `contact-orchestration` needs to avoid repeating one argument in a second channel, is a
fact like any other and needs an owner; where no system owns it, say that out loud rather than
designing around a store you do not have. The assignment of a person to a test group, which
`experiments-and-holdouts` needs to hold still, is also a fact with an owner and a retention of
its own.

**3. Build the data set backwards from the mechanics, and cut the rest.** A field enters the
stack when a named mechanic stops working without it. The instinct to send everything because it
is technically easier costs three ways: storage, slower segment recomputation, and the loss of
any answer to who fills this field. The second reason is not cost: what you may keep at all is
bounded by the purpose you collected it for, which the legal section of `SKILL.md`
sets out.

This is the seam with `list-building`. Which attributes the base should carry is that skill's
decision, taken from the decisions each attribute serves. Where each attribute lives, who may
write it, and how it is stored is this one's.

**4. Fix the format and the system name of every field before the first load.** Anything
enumerable gets an enumeration; free text stays only where the value is open. A city
stored as free text arrives as three spellings of one city, and after that no send can target
geography at all.

Treat this as close to one-way. Renaming a field or changing its type means removing it and
declaring it again in every filter, segment and template that references it, so the cost is a
pass over all of them rather than an edit.

**5. Draw the flows: source, transport, destination, one line per object.** The diagram is not
documentation. It is what somebody opens at the moment a fact stops arriving, and it answers
the question of where the break is faster than reading logs does.

**6. Say out loud what does not get copied.** Data with no consumer, data collected for a
different purpose, anything carrying elevated risk that no mechanic needs. An empty answer here
and a missing answer are different things: the first is a decision, the second means nobody asked.

## Thresholds and timings

- **The register is revisited when a system joins the stack or a mechanic is retired**, not on a
  calendar. A calendar review of a register nobody changed turns into a ritual.
- **A field format change is planned as a pass over every consumer of that field.** Size it by
  listing the places the field is used, before the work starts rather than during it.
- **Preparing the data set is its own stage, finished before the technical specification is
  written.** Size it from your own stack, roughly the number of objects times the number of source
  systems. Doing it after development has started means the list arrives as change requests.

## Edge cases

- **Two systems both claim a fact.** The signal is that both can write it and both do. Settle it
  by asking where the fact comes into existence, not by seniority: an order comes into existence
  where it was taken, a consent at the point that collected it, a balance where the processing
  runs. Where a fact does arise in two places, such as a registration that happens both
  offline and online, the owner is the system that sees both streams.
- **The owner can only export on a schedule.** Then the delivered freshness class of every fact it
  owns is the periodic one (`event-data-and-freshness.md`, step 4), whatever the consumers need,
  and every consumer has to know it. A mechanic that needs more freshness than the owner provides
  has three outcomes to choose between: change the transport, move the ownership, or drop the
  mechanic.
- **One object lives in two catalogs.** One shape of this is an offline and an online product
  catalog kept apart for historical reasons. While they are apart, any mechanic needing both
  cannot be built, and merging the catalogs is preparatory work rather than an integration detail.
- **The platform's data model has no object like yours.** Map your object onto the nearest entity
  the model has and **write the mapping down**: what the platform calls a product is, in your
  case, an article, a lesson or a booking. The requirement is that the mapping is recorded rather
  than held by one person.
- **Several legal entities or brands in one stack.** Ownership of a fact is decided by the object,
  not by the brand, and brand membership is an attribute of the record rather than a reason for a
  second stack. What may not be pooled across brands is settled by `list-building`.
- **A system is being retired.** Before it goes, the facts it owns need new owners named, one at a
  time. Retiring a system without reassigning ownership leaves fields that nobody writes and
  nobody notices for a quarter.

## Failure modes

- **Two systems disagree and nobody can say which is right.** The visible symptom is that the
  argument is settled by seniority rather than by a rule. It means the register either does
  not exist or is not being read.
- **A mechanic was built on a field that is filled for a small share of records.** A test extract
  before development catches this; a launch catches it afterward. Check the fill rate of the
  field, not the presence of the field in the schema.
- **The register exists and the last integration is not in it.** The symptom is a system that has
  been sending data for a month and appears nowhere in the diagram. From that point the diagram
  lies, and it lies at the worst moment, which is while somebody is looking for a break.
- **One field was created twice under similar names.** Both get filled, and segments are built on
  different ones. It is found by comparing the platform's field list against the register, not by
  looking through the interface.
- **Nobody can say what would break if a system were switched off.** Ask three people which flows
  depend on the accounting system. Different answers mean the flow diagram is not doing its job.
