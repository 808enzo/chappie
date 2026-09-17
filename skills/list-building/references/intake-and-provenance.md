---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Intake: the register, provenance, and the attribute plan

A base does not have one source. It has several, some of them written down nowhere, and they do not
produce the same quality of contact. This mechanic covers where rows come from, what you record
with them, which attributes the base should carry at all, and how you find out that one of your
sources is filling the base with people who will never do anything.

## Entry conditions

At least one working way to obtain a contact, and somewhere to put it.

## Exit conditions

A register of intake points; provenance stamped on new records; a written attribute plan that names
which attribute serves which decision and on which rung you ask for it.

## Steps

**1. Build the register of intake points.** One row each: where the person leaves a contact, what
you collect there, who owns the point, and which system receives the result. A point that is not in
the register keeps filling the base and answers to nobody.

Four kinds show up:

- **Your own, online.** A form, a registration, an account, a checkout.
- **Your own, offline.** The register at the counter, a desk, a card enrollment, guest network
  access.
- **Service.** A support contact, a booking, a repair request. These collect contacts as a side
  effect and nobody thinks of them as intake, which is why they are the kind that goes missing.
- **External.** A partner promotion, a joint giveaway, a marketplace, an event list.

**2. Stamp three things on the record, at the moment it arrives.** Not later, not derived
afterwards.

- **The intake point.** Which register row this came from.
- **The date.** Of the event that created the basis, not of the import.
- **What the person was told.** What they signed up for and what you promised them.

The third one has no other home: nothing else in the record holds it, so if the point does not
write it down it is gone. It is what you have when somebody asks what basis you were sending on,
and it fixes the frequency you promised, which `contact-orchestration` treats as part of that
basis. Without the second one you cannot count how long the basis has left to live.

Provenance is a **fixed property of the record**. Later contact does not overwrite it, and a merge
carries both sides of it rather than picking one (`identity-and-merging.md`, step 4).

**3. Write the attribute plan from decisions backwards.** List attributes by asking which decision
you cannot make without them, not by asking what you could reasonably ask for. Every attribute in
the plan names its consumer: the mechanic, the segment or the channel that stops working without
it.

An attribute with no consumer comes off the plan. It costs form completion to collect and it
unlocks nothing. `segmentation` is one place consumers come from: it names which attribute is
missing and which decision needs it.

**4. Spread the plan across rungs.** The first rung is the minimum that makes contact possible at
all: an address in one channel, plus a basis with its promise recorded. After that, attributes get
collected one at a time, each at a moment when the person can see why you are asking. Three routes
work:

- **A question inside the subscription form.** Use it where the answer changes the very first
  message. A supplier that asks which trade a business is in can make the first email specific to
  that trade instead of generic.
- **A separate capture point built around one topic.** Use it where the attribute matters to some
  people and there is no reason to ask everyone.
- **A send whose only job is to collect the missing field.** The answer writes back to the record.

The form itself, its display rule and the wording of the exchange belong to `onsite-capture`. What
arrives here is only which attribute sits on which rung.

**5. Read each source through its own cohort.** Once a period: take the records one point produced
in one period and read three numbers against them.

- The share that reached a first meaningful action.
- The share still reachable at the end of the window.
- The share that complained or unsubscribed.

Compare between points, and against your own median across the base. Not against an outside figure:
the composition of your intake is specific to your business, and no published number describes it.

This step is the reason step 2 exists. Without provenance you cannot assemble the cohort, and every
judgment about a source is a hunch.

**6. Give each point one of four verdicts.** The last two get their reason written down.

- **Leave it.**
- **Change the exchange** (what the person receives for the contact) and re-read after a period.
- **Narrow it.** Keep the point, stop feeding its output into general sends. Useful when a source
  produces contacts that are real but not yours in any meaningful sense.
- **Close it.**

## Thresholds and timings

- **The cohort window runs no shorter than the time a first meaningful action takes in your
  category.** For a purchase that is the median interpurchase interval, a construction that belongs
  to `repeat-purchase` and is only applied here. Read it sooner and you have measured how fast
  people check out, not what the source is worth.
- **The alarm threshold on a source is distance from your own median, not an absolute value.** A
  point whose share reaching a first action sits at half the base median, at a comparable volume,
  goes to investigation before the next period. Half is a starting cut you can tighten once you can
  see the spread between your own points; in a base with few points the spread is wide and this cut
  fires constantly, so widen it and rank sources instead.
- **Re-read every planning period, and out of turn on a volume spike.** A jump in volume from one
  point is a reason to re-read its cohort immediately. Volume spikes and quality drops arrive
  together.
- **Compare the first period after a point opens against nothing.** It is the baseline.

## Edge cases

- **There is only one point.** No base median to compare against. Read the cohort against that same
  point's own earlier periods, and take the closing verdict off the table until a second point
  exists. Closing your only intake is not a judgment about quality.
- **An external source will not give you provenance.** A partner hands over a list with no point and
  no date. Stamp it as external and undetailed, and keep it out of general sends until the person
  confirms for themselves. An honest marker and an empty field are not the same thing, and the
  distinction survives every later argument about that list.
- **An offline point cannot connect the person to anything online.** The counter knows the purchase
  and not the address. Then the point collects an **identifier** you can find the contact by later,
  such as a card number, rather than a contact. Register it that way, and read its cohort by
  purchases instead of by reachability.
- **One mechanic needs one attribute, and it costs a whole rung.** Decide for the mechanic only when
  it does not run at all without the attribute. If it runs worse but runs, the attribute moves to a
  later rung.
- **Consent is there and a channel is not.** The person agreed and left only a name. The record
  lives, does not count toward the reachable base, and goes to the front of the queue for filling
  in.
- **The same person arrives through two points.** Both provenances are true and both stay. Keep them
  as a list on the record rather than overwriting one with the other, or the earlier basis
  disappears along with its date.

## Failure modes

- **The base grows and the reachable base does not.** Intake for the period is positive, the number
  of records you can reach through at least one channel is flat. The source is collecting something
  that dies on arrival.
- **Nobody can name every intake point.** Ask three people for the list and compare. Any difference
  means nobody is watching part of your intake.
- **Provenance covers part of the base and the share is not growing.** Step 5 is impossible until it
  does, and every claim about source quality stays a hunch.
- **The attribute plan has become a questionnaire.** The symptom: rows in the plan whose consumer
  column says something like useful later. You collect those attributes and never read them, and
  every form pays for them in completion.
- **Somebody judges a source by volume.** The symptom is a source that everyone praises and nobody
  has read a cohort for. The two independent signals that catch it late are a spike of deletions
  arriving months afterward (`base-maintenance.md`) and a large intake that produced no purchases.
