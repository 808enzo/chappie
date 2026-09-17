---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Build order: what gets built first when you cannot build everything

Admission decides which mechanics deserve to exist. It says nothing about when any of them gets
built, and the gap between the two is where a year goes: nine rows are admitted,
three can be built this quarter, and the three that get built are the three somebody found
interesting in the meeting.

Interest is a bad sort key, and the reason is specific rather than moral. A mechanic that fires
rarely produces nothing to read for months. It cannot be validated, it cannot be repaired, and for
all of that time it looks like a failure while there is nothing in it to fix yet.

This mechanic covers the order the roster is built in, the dependencies that override the order,
how the queue is cut into waves, and what a blocked row looks like so that it stays blocked out
loud.

## Entry conditions

More rows have been admitted than can be built in one cycle. That is the same test
`crm-program-design` uses to hand its first queue over, stated in the same unit on both sides: a
cycle of building, not a count of what fits into the team's hands at one moment.

## Exit conditions

A queue cut into waves, with every wave's prerequisites closed before it starts, and a written
reason beside any row moved out of its computed position.

## Steps

**1. Order by firing volume before anything else.** The first row built is the one that will start
working immediately after launch. This is not a preference for easy work: a row that fires rarely
gives no reading, and a row with no reading cannot be confirmed, tuned or defended.

**2. Then by dependency, which overrides volume.** Three kinds, and confusing them is expensive:

- **Data.** The row needs an attribute or an event that does not exist yet, or that arrives in a
  slower freshness class than the row needs (`martech-stack`).
- **Mechanic.** The row needs the output of another row. Winning back lapsed customers rests on a
  definition of lapsed, and that definition is computed from history you have to accumulate first.
- **Promise.** The row needs a construction that has not been signed off. A loyalty mechanic
  cannot run before the loyalty program exists (`loyalty-program-design`).

A data dependency is closed by somebody else's work and is planned as a date against that owner.
A promise dependency does not close at all until the construction is agreed, which makes it the
one worth surfacing earliest, because no amount of effort inside the program moves it.

**3. Build the mechanics of the beginning of a relationship before those of its continuation.** The
reason is population, not difficulty. Early on, the people who have been with you long enough to
qualify for a late-relationship mechanic are few, and the people arriving now are many. This is
step 1 applied to the age of a relationship, and it is why the familiar instinct loses. Start
with the loyalty mechanic and leave the simple ones for later, and the elaborate mechanic fires
for almost nobody in the months when you most need something to read.

**4. Cut the queue into waves sized by what one person can verify**, not by what the platform can
switch on. A wave is a quantity of the reader, not a constant of the tool: as many rows as the
owner can walk end to end before the next wave starts.

**5. Run the overlap check against what is already live before a wave goes out.** It is the same
search as at admission (`roster-and-admission.md`, step 6), but now against the running set. Six
months can pass between admitting a row and building it, and the set has moved in the meantime.

**6. Verify a wave by walking the path, not by counting settings.** The walk is done on a real
address, end to end, with the delays and the substitutions in place. How the walk itself is done
belongs to the mechanic being built: `triggered-messages` for a flow, `onsite-capture` for a
capture point. What belongs here is the requirement: a wave is not built until every row in it has
been walked from the occasion to the last message.

**7. A waiting row does not idle.** A row blocked on data carries its prerequisite as an obligation
with an owner and a date, and it stands on the roster as waiting on X rather than planned. The
distinction is not cosmetic. Planned obliges nobody and survives any number of quarters; waiting
on X names a person who can close it.

## Thresholds and timings

- **Wave size is computed from the person verifying it rather than assigned.** The recipe: however
  many rows the owner can walk end to end inside the slot they have, that is the wave.
- **The next wave does not start until the previous one has finished its ramp-up.** Start with two
  of the row's own firing cycles or one month, whichever is longer. That applies to rows with a
  regular occasion; where the occasion is seasonal, ramp-up is measured in seasons and a month is
  not enough under any circumstances. Replace the figure once your own history shows how long your
  rows take to reach volume.
- **A row moved forward out of its computed position is recorded with the reason.** Without the
  record, a quarter later the queue has stopped being an order: nobody remembers why the top rows
  are on top, so nobody can argue with them either.

## Edge cases

- **The owner of the business insists on starting with loyalty.** Answer with an estimate: how
  many people will meet the condition in the first month on the data you hold now.
  Where the answer is few, the mechanic is admitted and built later, and that decision goes into
  the row so it does not have to be won twice.
- **The high-volume row is blocked on data and a low-volume row is ready.** Build the ready one and
  open a dated prerequisite against the blocked one. Ordering by volume governs comparable rows;
  it is not a license to stand idle.
- **The order was set and then the business changed.** Rebuild the queue rather than moving one
  row. What changed is the sort key, not a position.
- **Two rows can only be verified together.** This happens with mechanics that share an occasion
  and split into branches. The unit of the wave becomes the pair, and that is written down;
  otherwise half the pair ships in the next wave and the verification proves nothing.
- **A wave stalled halfway.** Some rows live, some not. The safe move is to finish the current wave
  and not start the next. It means the wave was cut larger than the verification could cover.

## Failure modes

- **Everything was switched on at once.** Errors arrive faster than anybody can work through them
  and keep surfacing long after launch. The signal is that there was no queue, only a list.
- **The first three rows fire for nobody.** The queue was ordered by interest. It is caught by
  comparing the actual firing volume against the number stated at admission, not by how the launch
  felt.
- **A wave was verified with one test send.** A test send checks a template. A path is checked by
  walking it. The signal is that the defects turn up in a delay or a substitution, which is
  exactly where a test send does not go.
- **A row has read planned for over a year.** No prerequisite, no owner, no date. That is not a
  queue, it is storage.
- **A promise dependency was treated as a data dependency.** Somebody scheduled a date for a
  construction that nobody has agreed to build, and the date passes without anyone being wrong,
  because no owner was ever on the hook for it.
