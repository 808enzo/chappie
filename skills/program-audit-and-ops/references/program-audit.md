---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# The audit: inventory, five checks, a decision on every finding

An audit differs from duty in the question it asks rather than in how deep it digs. Duty asks
whether what you launched still works. The audit asks whether it should still be running.

## Entry conditions

Run one when the roster has grown past what a slot can walk, when the systems or the team changed,
when a noticeable share of mechanics has no owner, or when revenue from the program drifts and no
single object explains it.

## Exit conditions

Every mechanic that can fire is on the inventory, every finding carries one of four decisions, and
the changes are recorded as versions so the next audit reads a difference instead of deriving the
same list again.

## Steps

1. **Inventory what is running, not what was designed.** Pull it from the sending systems, the flow
   lists, the schedules, the widgets, the exports. The first finding is rarely numeric: there is
   always a gap between what the team believes is live and what can fire.
2. **Get four numbers for each mechanic:** sends in the period; people reached, which is not the
   same as sends; money, counted by the rules in `metric-definitions`; and the cost of keeping it,
   meaning how many manual steps one issue takes.
3. **Run five checks:**
   - **dead**, meaning nothing has gone out for longer than its expected silence;
   - **duplicates and overlaps**, meaning identical or intersecting send conditions, or two
     mechanics competing for the same person;
   - **empty**, meaning it sends and produces neither money nor the target action on its own control
     metric;
   - **expensive**, meaning every issue is assembled by hand, so the cost scales with frequency and
     late sends appear wherever several people have to touch one issue;
   - **holes**, meaning people and stages no mechanic covers at all. Look for these from the base
     outward, because a list of mechanics cannot show you what is missing from it.
4. **Inspect configuration for the defects numbers never reveal.** A negation lost from a condition.
   A test address among the recipients. A once-per-lifetime cap on an event that repeats. A
   frequency limit left over from an older launch. A pause set during an edit. Consent a person gave
   that the system never recorded.
5. **Take the severity gate first, then order the rest by exposure.** Take a finding that lands in
   one of the three severity classes in `incident-response.md` out of the audit report and hand it
   to the owner of that class the day you find it: consent the system never recorded is one of
   those, and so is a suppression rule that stopped holding. Everything left orders by exposure,
   meaning people
   in the period multiplied by the value of the action at risk. Not by how old the finding is, not
   by how many times it fired, and not by how easy it is to fix. Sorting by ease produces a long
   list of completed work and an untouched top line.
6. **End every finding in one of four decisions:** repair it; merge it with a neighboring mechanic;
   switch it off; leave it as it is with the reason written down. The fourth is a real decision, and
   without the recorded reason your next audit starts from zero on the same question.

   Two of the four change what the program is composed of rather than how it runs, and those two
   the audit proposes rather than executes. Merging and switching off change what the program
   promises, and that is signed by whoever holds the roster (`scenario-map`), with the finding
   attached as the evidence. This blocks nothing urgent: you pause a fault that reaches a person
   on the spot through the incident route below, and a paused mechanic is not a retired one. Say
   which of the two you mean, because a pause filed as a retirement stays paused forever and falls
   out of both registers at once.
7. **Record versions:** what changed, when, who did it, why. Versions are what turn the next audit
   into a diff.

## Thresholds and timings

- **Timing comes from the state of duty, not from the calendar.** An audit is due when the roster
  outgrew the slot, when a system or the team changed, or when the share of ownerless mechanics
  became visible. A date on its own is not a reason.
- **Switching off a dead mechanic takes two conditions together:** silence longer than its expected
  silence, and no seasonal explanation. Silence alone is not enough.
- **After a migration, start with the base rather than the mechanics.** Part of the base may not
  have made it across, and then "the mechanic does not cover these people" means "these
  people are not in the system". Check in that order: people, then coverage, then configuration.
- **Read messages per person together with unsubscribes,** never on its own. Cutting the number of
  mechanics and cutting the load on a person are different decisions, and the second one belongs to
  `contact-orchestration`.

## Edge cases

- **A mechanic with no money and a duty to exist.** Service and order status messages are not judged
  on revenue. Their criterion lives in `transactional-messaging`.
- **A mechanic with money and no causality.** Last-click revenue flatters whatever sits closest to
  the purchase. The audit names candidates, it does not establish effect, and the proof belongs to
  `experiments-and-holdouts`.
- **A mechanic you may not switch off.** Subscription and consent confirmations are decided with
  `consent-and-preferences`, not on operational grounds.
- **Duplicates that are not duplicates:** the same send condition against different audiences,
  separated by an attribute you did not look at. Test it by intersecting the audiences rather than
  by comparing the conditions.
- **The audit finds what duty already knows.** That is a good sign: overlapping findings mean the
  roster covers the territory. The divergence matters more, and it looks like a mechanic that sends
  and appears in no roster at all.

## Failure modes

- **The audit ends in a list of recommendations.** Tell: the report has findings and no decisions
  from step six. The next audit will find the same list, and the one after that will too.
- **Mechanics get judged on conversion detached from volume.** The rare and valuable one gets
  switched off while the frequent and empty one survives.
- **Things get switched off with no reason recorded.** Six months later the mechanic comes back,
  carrying the defect it had before.
- **The audit happens once.** Without versions, each new one re-derives the same conclusions, and
  the cost never falls.
