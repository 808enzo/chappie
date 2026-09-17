---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# The roster and what gets onto it

A program accumulates mechanics the way a house accumulates keys. Something was launched for a
campaign three years ago and never switched off; something else was configured by a person who has
left; a third thing exists twice under two names. Ask three people what is currently running and
you get three lists, none of them complete, and the shortest one belongs to whoever configures the
platform.

The roster is one list of what the program does, kept outside the sending platform. It has to be
outside, because the platform can only hold what is configured: not the candidate you rejected,
not the row waiting on data that does not exist yet, and not the reason any of it is there.

This mechanic covers writing down what already runs, telling a mechanic from a campaign, the test
a candidate passes before it is built, and the collisions checked before it is admitted.

## Entry conditions

More than one mechanic is running or planned, and no single list of them exists.

## Exit conditions

A roster: one row per mechanic carrying its occasion, its audience, the decision it serves, its
owner, its stated firing volume, its admission date, its last-read date and its status. Separately,
a list of rejected candidates with the reason each was rejected.

## Steps

**1. Write down what already runs before deciding what to add.** Every live flow, series and
recurring send becomes a row, including the ones nobody claims. Three sources, and none of them is
complete alone: the flow list in the sending platform, the capture points on the site, and the
data flow diagram from `martech-stack`. A mechanic that exists and is not on the roster is the
expensive kind, because it sends and nobody reads what it did.

**2. Agree that a row is a mechanic, not a campaign.** A mechanic fires on an occasion and can run
for a year without editing. A campaign is tied to a date and an offer. One test settles it: change
the date and change the offer. A campaign stops making sense; a mechanic does not. Campaigns live
in `promo-calendar`.

Four signs a candidate is a mechanic: it fires in response to something a person did or did not
do; its content is assembled mostly from that person's own data rather than from one text written
for everybody; it is not tied to a dated promotion or a single promo code; and the audience of one
firing is small enough that assembling it by hand each time costs more than automating it.

**3. Give every row the decision it serves**, in one sentence naming what the person should do and
inside what window. A row without that sentence cannot be ordered, cannot be read, and cannot be
retired, because there is nothing to say it failed at. Two decisions in one sentence means two
rows, even where one flow will implement both.

**4. Run the admission test on a candidate before it is built.** Five questions:

- **Is there an occasion**, meaning an action by a person or a change in their state that the
  mechanic answers? No occasion means this is a campaign.
- **Does the data exist**, and in the freshness class this mechanic needs? The class belongs to
  `martech-stack`; what belongs here is checking that the answer arrived before the build did.
- **Will it fire often enough to earn a slot?** Estimate from your own data: how many people met
  the condition over the last comparable period. Not from the ambition.
- **Is a basis available** for the audience the row names, and where the data was collected for
  something else, is the reuse compatible with the original purpose? See the legal section of
  `SKILL.md`.
- **Is there a named person who owns the row after launch?**

A "no" to any of these is a prerequisite rather than a rejection: it gets an owner and a date, and
the row sits on the roster with the status waiting on that prerequisite, not planned. The difference between those two
words is the whole point, and step 7 of `build-order.md` is where it bites.

**5. Take occasions from an industry set and compute the constants yourself.** A ready-made list
is a good source of candidates and a bad configuration. The same mechanic waits one purchase cycle
in one business and three in another, and the number in somebody's article came from neither.
Where you have no constant of your own yet, the row is admitted with a starting value that is
named as a starting value, plus a date to revisit it. Not with a borrowed number presented as a
setting.

**6. Check the candidate against the roster before admitting it, not after.** Two rows can each be
sensible and be wrong together. Three collisions, all of them found by reading the roster rather
than by reading reports:

- **One occasion.** Two rows start on the same event. In reports both look healthy, because each
  counts the same firings as its own.
- **One person inside one window.** This is load. How much of it is acceptable is decided by
  `contact-orchestration`; what the roster contributes is the list of who creates it.
- **One promise.** Two rows tell one person different things about the same object.

**7. Record rejections with the reason.** A candidate rejected in conversation comes back every
quarter, the discussion starts from the beginning each time, and by the third round the person
arguing it is somebody new.

## Thresholds and timings

- **The roster is reread on a cycle, not on an event.** Start with monthly while the set is still
  growing and quarterly once it has stopped. Those are starting points: they apply to a set one
  person can walk row by row inside one slot, and where there are more rows than fit the slot, the
  answer is to shrink the set rather than lengthen the cycle (`roster-review.md`, step 6). Replace
  the cadence once your own history shows how often verdicts change.
- **The stated firing volume is computed from the last comparable period and written into the row
  at admission**, so that there is something to compare the actual against. Count the people who
  met the condition, not the sends.
- **The volume estimate is recomputed whenever the entry condition changes or the source under it
  changes.** A row whose condition was rewritten goes through admission again rather than
  inheriting the old number.

## Edge cases

- **A mechanic exists in the platform and has no owner.** The row goes on the roster anyway, and
  either an owner is named or the row goes to the front of the next review. An ownerless send is
  not a trifle: nobody will switch it off on the day that matters.
- **A candidate is demanded from outside and the demand has a date attached.** The date is the
  signal that this is a campaign. What turns it into a mechanic is not a refusal but a question:
  what is left of the request once the date has passed.
- **The occasion exists but almost nobody triggers it.** The row is admitted with the status
  waiting on volume and does not take a place in the build queue until the volume appears. Building
  it now produces a mechanic there is nothing to read on for as long as the occasion stays rare.
- **One mechanic serves two decisions.** Split it into two rows even where the implementation will
  stay one flow. The verdicts arrive per decision, and a merged row cannot tell them apart.
- **A mechanic needs a segment that does not exist yet.** The prerequisite belongs to
  `segmentation` and the date belongs in the row. Until the segment exists, the row does not move
  into the build queue.
- **The set arrived with a platform migration.** Every row goes through admission again, and this
  is not a formality: some of those rows were shaped around what the old platform could do, and
  some around a person who no longer works there.

## Failure modes

- **The platform's flow list is being used as the roster.** It lists what is configured rather
  than what is intended: no rejected candidate, no row waiting on a prerequisite, and no reason
  any row exists. The signal is that the roster cannot be opened without access to the platform.
- **Everything is admitted and the set only grows.** Zero rejections in a year means there is no
  admission test, only a queue of requests.
- **Rows describe messages instead of mechanics.** The September email, the one about new arrivals.
  Such a row cannot be ordered or retired, because the decision it serves is not written anywhere.
- **The constants in the set belong to somebody else.** The signal is round numbers, identical
  across mechanics that have different cycles. It is caught by comparing a constant against your
  own distribution, not by arguing about it.
- **Two rows start on the same occasion and both report success.** Each counts the same firings.
  Reading reports will not find it, because both look healthy; comparing occasions across the
  roster will.
