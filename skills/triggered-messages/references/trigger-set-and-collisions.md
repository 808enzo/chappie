---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# The flow set: collisions, priority, retirement

You design flows one at a time, and the person receives them all at once. Each flow is polite on
its own. Twenty polite flows produce a load nobody ordered and nobody sees, because your reporting
splits by flow and the person does not.

This mechanic is about the set: what is live, which flow wins when two fire together, how close
two automated messages may land, and what it takes to switch one off.

## Entry conditions

- More than one flow is live.
- You can count touches per person, not only sends per flow. Without that count the argument about
  load is an argument about impressions.

## Exit conditions

You have the set written out as a list, with a priority order on it. The collision rule and the
gap inside the set are configured rather than remembered. You have set a review interval, and
every flow has a retirement condition.

## Sequence

**1. Take the inventory.** One list: flow, firing event, entries per period, length, channels,
contribution. The first inventory almost always turns up flows nobody remembered and two flows
built on the same event by different people a year apart.

**2. Order the set by proximity to a decision, not by revenue.** Started checkout, abandoned cart,
saved item, viewed item, browsed category, then catalog and date occasions. Ranking by revenue
hands priority to the flow with the most volume rather than to the one that fits the moment. A
notification the person asked for (back in stock, a price drop they subscribed to) sits outside
this order: it is the one message they requested, so a behavioral flow that collides with it
yields, and the notification is never the one left to expire in a deferral.

**3. Write the collision rule.** When two flows fire for one person at the same moment: the senior
one goes, the junior one is suppressed or deferred. Say which of the two, and for how long. A
deferred flow needs its own expiry, or it comes back when the occasion has gone cold.

**4. Set the gap inside the set.** A minimum distance between two triggered messages from different
flows to one person, and a ceiling per period. This is not the same as the overall contact cap,
which belongs to `contact-orchestration`. This one exists so that automated flows do not interrupt
each other. Steps of one flow keep their own intervals, and a cascade escalation keeps the wait its
channel sets: hold them to the gap and a cascade read in minutes waits hours. The ceiling counts
every automated message, steps and escalations included.

**5. Deduplicate by object, not by flow.** One item sits in the cart and in the saved list, its
price drops, and its stock runs low. Write the rule on the object: one event on one object
produces one message, from the flow that is senior in the order of step 2, and the other flows stay
quiet about that object. The rule holds only as a claim written before the send, keyed on the
person and the object, because a message in flight shows up in no history yet
(`contact-orchestration` claims a pitch across programs the same way).

**6. Separate flows from campaigns.** The seniority rule is already set in `email-program`, which
uses `contact-orchestration`'s five classes: a flow goes before a campaign and yields to a service
message or a mandatory notice. Add the other half here. You exclude someone inside a
flow from the campaign on the same subject, otherwise they get the same offer twice in two
different wordings, and the two wordings will not match. A held-out entry counts as inside the flow
for this rule and for steps 3 and 5; otherwise the control receives the same pitch by another path.

**7. Do not clone flows.** A variant is a branch inside the flow, not a new flow. Cloning one per
promotion, per tier or per segment produces duplicate sends and makes analysis impossible: the
same flow exists in ten near-identical copies that differ by a banner.

**8. Set a review.** Once per cycle, walk the inventory: entries, conversion per entry,
contribution to load. A flow with no entries is broken or unwanted. A flow with load and no
conversion comes out. This review decides what the trigger set contains, and it answers one
question: does this flow work. `scenario-map` asks the other one of the whole program's roster:
does the decision this flow serves deserve a mechanic at all. A flow can pass this review and
still come off the roster, because another mechanic serves the same decision better.
Watching whether live flows still work belongs to `program-audit-and-ops`.

## Thresholds and timings

- **The gap inside the set:** the minimum time between two triggered messages from different flows
  to one person. Derive it from your own data, by finding the spacing at which unsubscribes start
  to rise.
- **A ceiling on automated messages per person per period**, kept separately from the overall
  contact cap. Flows fire without a schedule, so they fill a cap invisibly and the campaign that
  hits the ceiling gets blamed.
- **The deferral window** for a junior flow in a collision: the deferred message leaves only while
  its event is younger than the event's expiry, counted from the event rather than from the
  collision.
- **The review interval**, tied to the program cycle rather than to the calendar. A set that has
  never been reviewed grows in one direction only, because adding a flow has an owner and removing
  one does not.
- **A liveness floor:** the minimum entries per period below which a flow counts as dormant and
  gets checked by hand.
- **A peak-season pause.** During the peak the calendar is already full. Decide in advance which
  flows pause, and pause them from the list rather than in reaction to complaints.

## Edge cases

- **Two flows on one event, built at different times.** The classic legacy case: overlapping
  conditions, messages going out simultaneously in different channels, and no single owner. Only
  the inventory finds it.
- **A service message in a collision.** Order confirmations and delivery status always go. The
  priority rule does not apply to them.
- **Two dates on one day.** A birthday and a purchase anniversary land together. The senior one is
  whichever is closer to money today; the other is skipped rather than moved, because a date moved
  by a week has lost its occasion.
- **One person, two profiles.** The gap is enforced per profile and the person receives double.
  Until stitching is done, set the ceiling tighter than the data suggests.
- **A flow required by law or by contract.** A marketing flow holding higher priority does not
  suppress a notice that a service is about to expire.
- **A full-base promotion.** The order between layers does not change: on the same day a flow still
  goes before the campaign (`email-program`). What changes is inside the flow: its money step is
  suspended or replaced for the duration (`flow-shape-and-cascade.md`), because the person sees the
  public offer anyway and a weaker personal code beside it reads as an insult.

## Failure modes

- **Several automated messages a day from different flows.** Unsubscribes and complaints rise, and
  people blame the channel as a whole, because per-flow reporting never adds up to per-person
  reporting. Tell it apart from a single bad step (`flow-shape-and-cascade.md`) by reading the
  unsubscribes against how many automated messages each person received that day: rising with the
  count points here, concentrated on one step whatever the count points there.
- **Priority lives in one person's head.** Test it by asking what goes out when both flows fire,
  then check whether that answer exists in the configuration.
- **The set grows and nothing is retired.** Where nobody owns switching flows off, flow count only
  rises.
- **Promotion clones.** One flow exists in ten near-copies. Duplicate sends become a matter of time,
  and comparing variants is impossible because they were never the same flow.
- **Total automated load is invisible.** Each flow reports on itself, nobody counts touches per
  person, and the first signal is a rise in unsubscribes, read by the separating question above.
- **The review happens after an incident.** The tell: someone reassembles the list of live flows
  from scratch every time something breaks, and nobody keeps it in between.
