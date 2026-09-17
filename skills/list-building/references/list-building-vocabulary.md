---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-07
---

# Vocabulary of the base

Terms all three mechanics assume. Two of them are words other skills also use for something else,
and this file separates those at the end.

## The base itself

**Base size.** The count of records. It grows on any intake at all and reports nothing about
whether you can do anything with them. It appears here only so the next term has something to sit
against.

**Reachable base.** The records inside the active base that you could get a message to through at
least one channel on a basis that still holds. Three things have to be true at once, and each one
fails on its own: a working address with an expired basis is not reachable, a live consent with no
channel attached is not reachable, and neither is a record parked in the second tier, which nothing
sends to until it returns. This is the denominator the skill's control metric uses.

**Active base.** The tier the sending systems and the segment engine read from. Records enter it on
intake and leave it under the decay rule, and you can put them back.

**Record of the person.** The tier that survives removal from the active base: purchases,
obligations, and the evidence of a consent or a refusal. Its retention is set by the purpose you
collected the data for. A refusal is kept without a time limit and outlives the record it sits on,
because deleting the refusal is how you mail somebody after they asked you to stop.

**Return event.** The named action that brings a record back into the active base by itself: a
purchase, an account login, a contact left, a reply. Returning does not make the person new, and
their earlier history stays attached.

## Where records come from

**Intake point.** One place a person leaves a contact, together with what you collect there, who
owns it, and which system receives the result. Four kinds: your own online, your own offline,
service, and external.

**Provenance.** Three values stamped on a record at the moment it arrives: the intake point, the
date of the event that created the basis, and what the person was told. A fixed property. Later
contact does not overwrite it, and a merge carries both sides of it rather than picking one.
Without the date there is nothing to count a basis expiry from; without the third value there is
nothing to answer a question about basis with.

**Attribute plan.** The list of attributes the base should carry, each naming the decision that
needs it. Built backwards from decisions, never forwards from what you could ask. An attribute with
no named consumer does not belong on it.

**Rung.** A position in the order you ask for attributes. The first rung is the minimum that makes
contact possible: an address in one channel plus a basis with its promise recorded.

## Identity

**Key.** An attribute that is unique to one person and does not change over time, confirmed either
by the person or by your own system: an internal account identifier, a confirmed channel address, a
contract or card number. Only a key can justify a merge.

**Hint.** An attribute that raises the probability of a match without reaching uniqueness: a device,
a browser marker, a matching name, a matching delivery address, closeness in time. A hint justifies
a link.

**Contradiction.** Two non-empty values of one field that cannot both belong to one person: two
dates of birth, two surnames against two different delivery addresses, two active loyalty cards
each carrying a balance. A matching key with a contradiction present routes to review rather than
merging. A **conflict** is the weaker case and a different job: an empty value against a filled
one, a short name against a full one, two spellings of one street. A conflict does not block a
merge, and `identity-and-merging.md`, step 4 settles it by the kind of field.

**Merge.** The combination of two records into one. Whether your system can undo it is a capability
to check rather than assume, and where it cannot, a combined history does not decompose back into
two. What makes it reviewable either way is the snapshot taken before it.

**Link.** A reversible marker that two records are probably the same person, without combining
them. What you do on a hint while waiting for a key.

**Snapshot.** The copy of both records plus the reason for the decision, stored before a merge. The
only route back from a wrong one, and bounded by the same purpose limit as the record itself.

## Silence

**Unreachable.** Delivery is technically impossible. `deliverability` sets this state in four
classes and hands the class over with it, and `base-maintenance.md` decides the fate of the record
by that class. The class in which the provider blocked the flow rather than the address is the one
that carries no decision here.

**Silent.** Messages arrive and the person does nothing for a named length of time. The only one of
the three states a win-back applies to.

**Refused.** Unsubscribed, complained, or withdrew consent. You do not reactivate them, and you
keep the state without a time limit.

**Silence threshold.** The length of silence after which a record leaves the active base. Derived as
two median interpurchase intervals in your own data, so that it moves with the category rather than
being carried in from one.

## Two words this skill shares with a neighbor

**Deduplication.** Here it means merging several records of one person into one. In
`contact-orchestration` the same word means not repeating one argument to a person in a second
channel. Both are correct in their own file and the word is the only thing they have in common, so
ask which one somebody means before you start the work.

**Hygiene.** Here it means deciding who stays in the base. In `deliverability` it means the
discipline of arriving in the inbox: bounce handling, sender reputation, list validation before a
send. The boundary is one sentence: **`deliverability` sets the unreachable state, this skill
decides what happens to the record that carries it.**
