---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Reviewing the roster and retiring from it

Sets of mechanics grow monotonically unless something removes from them, and almost nothing does.
Every skill in this library, including this one, is written to help somebody add. Retiring is the
part nobody has an instinct for: the mechanic still runs, it costs no money this month, and
switching it off is a decision somebody has to sign.

Retiring is also the part with a real hazard in it, which is why the order of the steps matters
more here than anywhere else in the skill. A mechanic switched off in the platform strands
everyone currently inside it, holding a promise the next message was supposed to close.

This mechanic covers what is read on a review, the four verdicts, the route a neighbor's finding
takes to become a verdict, and the order a row is retired in.

## Entry conditions

Rows have finished their ramp-up window, so there is something to read.

## Exit conditions

Every row carries a verdict with a date. Every retired row carries a retirement record.

## Steps

**1. Read rows, not messages.** Three readings, all of them about the row as a whole:

- did it reach the firing volume stated at admission;
- does the decision it serves happen more often for the people it touched, which
  `experiments-and-holdouts` owns the measurement of;
- is it still the only row on its occasion.

**2. Give each row one of four verdicts: keep, rework, merge, retire.** Rework means the decision
still matters and the construction does not work, so the row goes back to the author of that
mechanic. Merge means two occasions turned out to be one, and one row survives carrying one
promise. Retire means the program no longer needs the decision, or a neighboring row serves it
better. A verdict without a date has not been given.

**3. Take a neighbor's finding by route rather than directly.** Other skills produce findings about
rows and do not retire rows themselves.

- `program-audit-and-ops` answers whether something running still works. Its conclusion arrives on
  the row as evidence and is read at the next review. The one exception is a fault that reaches a
  person: that leaves through the incident route immediately, and the row is marked paused pending
  review, which is not a retirement.
- `triggered-messages` runs its own review of the live trigger set: entries, conversion per
  entry, contribution to load. The roster does not repeat that reading. It takes the result and
  asks its own question: does this decision deserve a mechanic at all. A flow can pass its own
  review and fail this one, because another row serves the same decision better.
- `experiments-and-holdouts` delivers a confirmed hypothesis. The roster decides whether it
  becomes a new row, an edit to an existing row, or nothing.

The rule underneath all three: **switching something off changes what the program promises, so the
holder of the roster decides it, not whoever found the defect.**

**4. Retire in this order: close the entrance, finish the people inside, switch off, record.** New
people stop entering the row first. Those already inside either reach the end or are moved
somewhere explicitly. Only then is the mechanic switched off in the platform, and only then is the
retirement written down. Reversing the first two strands people mid-path, holding a promise they
were already given and missing the message that closes it.

**5. A merge keeps one occasion and one promise.** Merging is not joining two texts into one flow.
It is choosing the occasion the surviving row will stand on and giving up the other one out loud.
Skip the choice and you get a row with two entrances, which reports as one mechanic and behaves as
two.

**6. Size the set by who reads it.** The ceiling is not a number of rows, it is a question: does
the review get through the whole roster inside its slot. Where it does not, either the slot grows
or the set shrinks, and shrinking is the answer whenever nobody will staff the larger slot: a set
nobody reads carries rows whose status nobody knows.

**7. Keep a retirement record**: what the row did, why it went, and what would have to be true to
bring it back. Without it the retired mechanic returns in a year as a fresh idea, passes the
admission test a second time, and reaches the same result by the same route.

## Thresholds and timings

- **No verdict is given before the row's ramp-up window has passed** (`build-order.md`, thresholds).
  Before that there is nothing to read, and a verdict given early retires working mechanics.
- **A paused row does not stay paused indefinitely.** Start with one review cycle: a row that has
  not come back into service within a cycle takes the retire verdict rather than hanging. That
  applies to rows paused because of a defect; a row waiting on an external event with a known date
  lives until that date. Replace the figure once your own history shows how long paused rows
  take to be repaired where you work.
- **Every row carries the date it was last read.** That date is how you see that the review keeps
  walking the same few rows: the dates on the rest do not move.

## Edge cases

- **The mechanic works and nobody needs the decision any more.** The retire verdict is given on the
  decision, not on the conversion. Conversion is an argument against retiring and a weak one: a
  well-served unnecessary decision is still unnecessary.
- **The row was retired and the occasion is still being captured.** The event stays in the event
  plan with no consumer. Hand that to `martech-stack` as part of the retirement, or the capture
  runs and is paid for indefinitely.
- **The row carries a promise made at signup.** Somebody was told they would receive a particular
  kind of message at a particular frequency. Retiring the row does not cancel that. The row is not
  retired until the promise is closed explicitly: by a message, by a change in the preference
  center (`consent-and-preferences`), or by a replacement row.
- **The row being retired is one other rows depend on.** Read the dependencies from `build-order.md`
  backwards: retire the dependents first, or give them another source.
- **Two rows both perform well and serve one decision.** Merge rather than keeping both. The set is
  paid for in attention, and two rows on one decision cost twice while producing a reading neither
  of them can explain.
- **Somebody outside asks for a row to be switched off for the duration of a campaign.** That is
  not a retirement, it is an exclusion from an audience for a period, and it lives in
  `contact-orchestration`. A row switched off and back on loses its ramp-up and comes back
  unreadable for as long as the ramp-up lasts.

## Failure modes

- **Rows are judged on revenue and the service ones look empty.** The empty-mechanic criterion does
  not apply to a service message; that belongs to `transactional-messaging`. The signal is a run of
  retire verdicts on confirmations and status messages.
- **Nothing has ever been retired.** The set grows monotonically. That is not a sign the program is
  healthy. It is what a roster looks like when the review never reaches a verdict, and counting
  retirements per year is how you see it.
- **A mechanic was switched off in the platform and the roster still shows it live.** From that
  moment the roster lies, and it lies at the worst moment, which is while somebody is planning the
  next wave against it.
- **The review reads the same rows every time**, the ones that have numbers on them. Caught by
  the last-read date, which does not move on the rows the review skips.
- **People were stranded mid-path.** The row was switched off before the people inside it were
  finished. The signal arrives as complaints from people who were promised a second message and
  never got it, which is months after the decision and from the wrong direction.
