---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Maintenance: reachability, decay, and two tiers of storage

A base nobody cleans reports a growing number every month and loses the ability to reach anybody.
This mechanic covers how you tell apart the three different things people call inactive, where the
silence threshold comes from, what leaves the active base, what survives that, and how somebody
comes back.

## Entry conditions

The base exists, and provenance is stamped on at least part of it.

## Exit conditions

A written decay rule: which signals make a record dead, what happens before removal, what you
remove, what survives, and which event brings a record back.

## Steps

**1. Count the reachable base, not the base.** The working number is how many records you could
reach today through at least one channel on a basis that still holds, **counted inside the active
base of step 5**. A record parked in the second tier has a live address and a live basis and is
still not reachable: nothing sends to it until the return event of step 6 brings it back. Base
size only ever grows, which is why it reports nothing.

**2. Separate the three states people file under inactive.** They look identical in a report and
they have opposite consequences.

- **Unreachable.** Delivery is technically impossible: the address rejects mail, the channel is
  switched off, the number is dead. `deliverability` sets this state and hands over its class with
  it, and you decide here what to do with the record. Read the class before you decide anything:
  one of the four is a provider blocking your whole flow, which turns every address at that
  provider unreachable at once, live ones included. Those records are not a base problem and take
  no decision here until the incident closes.
- **Silent.** Messages arrive and the person does nothing for a named length of time.
- **Refused.** They unsubscribed, complained, or withdrew consent.

Never reactivate a refused person. Try a second channel for an unreachable one, once the class
says the address itself is the reason. Only the silent one
is a candidate for a win-back, and treating all three as one segment is how a program mails
somebody who told it to stop.

**3. Derive the silence threshold from your own purchase cycle.** The construction: **two median
interpurchase intervals with no reaction and no purchase.** Somebody who has missed two of their
own cycles rarely returns in the third.

The number comes out of your data and moves with the category, which is the point. A fixed figure
borrowed from elsewhere cuts off living customers in any category that buys slowly: where people
buy once a year, a threshold set for a category that buys monthly falls due months before anybody
would expect a second purchase. Where you have no purchase history at all, use the interval
between reactions instead and say that is what you did.

A person in a control group receives nothing and so reacts to nothing. Their silence is the test's,
not theirs: the threshold does not run for them while they are in the control, and they keep the
state they had on the day of assignment (`experiments-and-holdouts`).

**4. Run the win-back before deletion, not instead of it.** The sequence itself belongs to
`lapse-and-winback`. Two requirements come from the base side and belong here:

- **It has an end.** A sequence with no end turns the silent group into a permanent segment nobody
  removes, and it distorts every denominator while it sits there.
- **The last message says what happens next**, plainly, because after it the record leaves the
  active base and you have nowhere left to say it.

**5. Split removal from the active base and deletion of the record.** Two tiers, and this split is
what makes step 4 affordable.

- **The active base** is what the segment engine reads and what sends go out to. Records leave it
  under the rule in step 3, and you can put them back.
- **The record of the person** is what you keep longer: purchases, obligations, and the evidence of
  a consent or a refusal. It survives removal from the active base.

**A refusal outlives the record it belongs to.** Delete somebody who unsubscribed, and you have
deleted the fact that they unsubscribed, and the next intake writes them back in as new. No single
step in that sequence looks like a mistake, which is why it survives review.

**6. Name the return event.** A record returns to the active base by itself, on a named event: a
purchase, an account login, a contact left, a reply in any channel. The return does not reset the
history. The person is not a new customer, and their earlier purchases stay theirs, which matters
the first time a report counts them.

**7. Check that event retention allows the segments you build.** Events carry their own retention,
set separately from the retention of the record. Read both numbers: where the event window is the
shorter of the two, you cannot build a segment that looks further back than it, and you find that
out on a running flow rather than at configuration time. The check: take the deepest looking
segment you use and compare its window against how long you keep events. Where the window loses,
either lengthen the retention or rebuild the segment out of something you keep longer, such as your
own send history.

## Thresholds and timings

- **The silence threshold is two median interpurchase intervals** (step 3), computed on your own
  data and revisited when the category or the composition of the base changes.
- **Clean at least once per planning period.** Rare cleaning accumulates dead records, and then the
  first big cleanup looks like the base collapsing and frightens people more than it should.
- **A spike in the volume being cleaned is a signal about intake, not a success.** Records that
  fall due together were collected together, one silence threshold earlier, so an unusually large
  batch points at one earlier period of intake. Read removals by their provenance and the answer
  goes straight back to `intake-and-provenance.md`.
- **Keep a refusal without a time limit.** It is the one field in this mechanic with no retention
  ceiling on it.
- **After changing the decay rule, read no sooner than one silence threshold.** Sooner than that you
  are reading a base the rule has not finished applying to.

## Edge cases

- **The person is owed something.** An open order, unspent points, a live warranty. They leave the
  active base, and the record does not go anywhere: you cannot delete an obligation by deleting the
  person who holds it.
- **A seasonal category.** People buy once a year, so two intervals is two years. The rule from step
  3 still holds and gets expensive in storage. The honest trade is to keep the record and remove it
  from the active base earlier, rather than shortening the threshold and cutting off people who were
  going to come back.
- **Reactions yes, purchases no, for years.** Somebody reads and never buys. This is not a decay
  case: they are reachable and the basis holds. It is a question about what you send them.
- **Manual cleaning erases reporting history too.** In some systems a manual delete removes the
  person from reports already produced, and a year over year comparison stops agreeing with itself
  afterwards. Check which kind of delete you have before the first cleanup, not after.
- **Records came back in a wave.** Switching on the return event makes the base jump. That is not
  intake, and it does not belong in the intake number: count returns on their own line.
- **The base is small.** Apply the rule and defer the deletion: at a small base the cost of a wrong
  deletion is higher than the cost of storage. Removal from the active base still works normally.
- **Somebody is silent in one channel and active in another.** They are not silent. Reachability is
  a property of the person across channels, not of one channel, and a rule applied per channel
  removes people who are still answering somewhere else.

## Failure modes

- **The reachable base falls while the base grows.** The headline signal that nobody is running this
  mechanic: intake happens and nobody is alive at the end of it. Two numbers, one period.
- **The inactive segment has existed for a year and never empties.** The exit sequence has no end,
  so you announced the decay rule and never applied it.
- **Somebody who unsubscribed is receiving mail again.** Either the refusal does not outlive the
  record, or intake writes over the state (`intake-and-provenance.md`, step 2). Both show up in the
  same place: pull the record and look at whether the refusal is still on it.
- **Nobody can state the size of the reachable base.** They state base size instead. The difference
  between those two numbers is exactly what this mechanic manages, so if the second is not computed
  there is nothing to manage with.
- **A flow stopped finding people after a retention change.** A silent flow is
  `program-audit-and-ops` territory, and it comes back here only when the cause turns out to be the
  event retention window in step 7. Worth naming because the two look nothing alike from where the
  flow is being watched.
