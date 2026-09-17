---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Changing platform: the decision, the order, and the reconciliation

Moving records is the cheap part of a migration. What costs is rebuilding the logic, proving it
works, and earning back a sending reputation that starts at nothing. The steps below are ordered,
and what this mechanic exists to prevent is what happens when one of them is skipped: the base
moved without being cleaned, forms left pointing at the old system, a first send to everybody.

This mechanic covers deciding whether to move at all, the order the move goes in, and the
reconciliation that outlives it.

## Entry conditions

Somebody suspects the program is limited by the tool rather than by the setup, or the decision to
move has already been taken elsewhere.

## Exit conditions

A decision with the limitation named. A migration plan whose steps are in order and each verified.
A reconciliation that continues after the move is declared finished.

## Steps

**1. Establish that the constraint is the tool.** Five signs that a tool has been outgrown: a
ceiling on volume or send rate high enough that a campaign lands after its own occasion; every
setup change needs a developer; reporting stops at opens and clicks and never reaches revenue;
technical failures have become part of the working week; the price rises while the capability set
stands still.

**The threshold for the decision: at least one sign has to block a capability a mechanic on your
agreed plan needs.** Otherwise you are moving for comfort and paying the full price of a
migration.

**2. Write the requirements as the mechanics that have to run, not as a list of features.**
A feature is easy to demonstrate; a mechanic gets tested on a trial with your own data. **Compare
at least three options as a starting floor**, and make one of the three staying where you are,
priced by what the missing capability would cost to build on the current platform. Two options
turn the exercise into a preference between two vendors; raise the floor where the switching cost
is high enough to pay for the extra evaluation time.

**3. Freeze the current state on paper before anything is touched.** What transfers between
platforms is the description, not the setup. Write down the live flows with the trigger condition,
the branches, the delays and the exit conditions for each; the segment definitions; the templates;
the suppression list; the field register and the formats. Templates and flows do not carry across,
because the editors differ. This map does, and it can only be assembled while the old platform is
still running.

**4. Load the suppression list before the first send, not alongside the base.** People who
unsubscribed, people who complained, and addresses that are technically unreachable get onto the
new platform **before** there is a live send on it. The order is the substance here, not
housekeeping: reversed, it sends mail to somebody who asked you to stop, and the obligation to act
on that request does not pause while you are migrating.

**5. Repoint intake on the day you start sending from the new platform.** Forms, integrations and
capture points still pointing at the old system keep filling it, and the split widens every day
until somebody notices. Where the two cannot be switched on the same day, switch intake first and
send from the old platform a little longer, rather than the other way around.

**6. Rebuild flows in waves, starting with the ones carrying money and service.** Turning
everything on at once produces errors faster than anybody can work through them, and they surface
for months afterward. Each rebuilt flow is verified by walking the whole path on a real address,
with the delays and the substitutions, rather than by sending one test message. Running two
platforms in parallel is safe only where a duplicate send is impossible by construction; where it
is possible, cut a flow over whole rather than half of it.

**7. Reconcile daily while the move is running, and stretch the interval on evidence.** Compare a
few counts per flow: the number of records, the number with a live basis, and the fill rate of the
fields the mechanics use. Add the cheap check the counts do not replace: open a handful of
random profiles and look at them.

**8. Hand the sending reputation to `deliverability`.** Warmup, authentication records, and inbox
placement belong there. What stays here is the requirement not to open with a full-volume send and
to hold time for warmup inside the migration plan.

**9. Read the first period against an expectation, and treat a rise as a signal too.** Take the
expectation from the volumes the old platform was producing; where you have no history, from the
count of records that meet the condition. Treat a number that has moved by an order of magnitude
as a broken transfer until you have checked the unit of measurement on both sides.

## Thresholds and timings

- **The duration is set by what has to be rebuilt, not by the size of the base.** Size it by
  counting: live flows, integrations, and fields in non-standard formats. Moving the records is
  the cheapest part. In order of magnitude, a first send is reachable quickly, a full move of the
  mechanics is the expensive part, and moving loyalty processing extends it again. Those are
  statements about order, and you put your own dates against them.
- **Reconcile daily while flows are being cut over.** Stretch the interval after two consecutive
  reconciliations come back clean rather than on a date, and keep a periodic one for as long as
  the integration lives. Start with that pattern on a platform change or any large change to a
  source system, and replace it once your own history shows how long discrepancies keep appearing
  in your stack.
- **The suppression list moves first and is verified before the first send.** Two steps of the
  move have no acceptable reordering, and this is the one that reaches a person when it is
  reordered. The other is the freeze of step 3, which is not a matter of discipline: once the old
  platform is off, the description of what ran on it cannot be written at all.
- **The old platform stays on until at least one full reconciliation has passed after the last
  flow was cut over.** Until then it is the only thing you have to compare against.

## Edge cases

- **Running two platforms in parallel is not possible**, on cost or on contract terms. Then cut
  over flow by flow rather than all at once, and order the flows by which is cheapest to roll back
  rather than by which is most convenient.
- **History that will not export.** Check opens, clicks and impression history first: a new
  platform starts empty on all three. Decide before you cancel, not after: list the segments that
  stand on that history, and either rebuild them on something that does move or agree out loud to
  lose them.
- **A trigger condition was copied across and behaves differently.** Identically named settings
  mean different things on different platforms. Check it by comparing how many people entered the
  flow over a comparable period, not by comparing the settings.
- **Loyalty processing is moving too.** This extends the move again and adds a risk the other
  flows do not carry. While the balance is being computed in two places, any message quoting a
  balance risks quoting the wrong one. The rules of the program belong to
  `loyalty-program-design`; what stays here is the requirement not to send balance messages until
  the balance has one owner again.
- **The old contract expires before the move finishes.** A real constraint, and it is planned as a
  date: export everything that becomes unreachable at switch-off first, then move the flows.
- **The vendor changes a sub-processor mid-move.** It is an event for your stack rather than
  paperwork for theirs, and the contract terms on sub-processors decide what notice
  you get and whether you may object (the legal section of `SKILL.md`). Ask about those terms
  while choosing the platform, not when the notice arrives.
- **The migration stalls halfway.** Some flows on the new platform, some on the old, the dates
  gone. It is a sign the waves were cut too large. The safe move is to finish the current wave and
  not start the next, rather than to roll back what is done.

## Failure modes

- **Somebody who unsubscribed is receiving mail again.** The failure of a migration that reaches a
  person rather than a report. Check the order first: the suppression list arrived after the base.
- **The base has split.** New contacts land in the old system, reports disagree, and the gap grows.
  It is caught by comparing intake over a period on both platforms.
- **The first send went to everybody.** What happens next is `deliverability` territory, but the
  cause is here: the migration plan had no warmup step in it.
- **The reconciliation was done once and the move declared finished.** The symptom is discrepancies
  arriving months later, one at a time, through complaints.
- **A number rose by an order of magnitude and the room celebrated.** One cheap check settles it:
  the unit of measurement on each side of the transfer.
- **Nobody can say which flows are already on the new platform.** Halfway through a wave-based
  move, the list of what is where is the only thing keeping two platforms from sending the same
  message, so its absence is itself the failure.
