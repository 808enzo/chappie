---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# How the series ends, and what a second arrival does

A welcome series is built as a sequence and fails as an ending. The touches keep arriving for
somebody who already bought. The window closes and nobody picks the person up. Somebody who left and
came back gets introduced to a brand they have been buying from for years.

The sequence below is the same whichever way the series ends, which is why it is a file of its own
and not the last steps of the previous one.

## Entry conditions

The series is running and a person is inside it.

## Exit conditions

The person is out, the outcome is written to the profile as a state, and the mechanic they now
belong to is named.

## Steps

**1. Name the outcomes before launch.** They come from crossing two facts: whether the target action
happened, and whether the person is still reachable. That gives four, and each has an address.

| Outcome | What happened | Who owns the person next |
|---|---|---|
| Break | the target action happened inside the window | the post-purchase mechanic: `repeat-purchase`, the regular program |
| Exhaustion | the window closed with no target action | the reachable-and-never-bought group (`rfm-segments`) |
| Departure | an unsubscribe, a complaint, a hard bounce | suppression (`consent-and-preferences`, `list-building`) |
| Basis expiry | the basis ran out before the window did | nothing goes until a new basis exists |

Cause separates the fourth outcome from the third, not consequence. Departure follows something the
person did; expiry happens on a clock, and only somebody watching the clock notices it. If your
construction produces a fifth outcome, name it and give it an address the same way. An outcome
without an address is the thing this step exists to prevent.

**2. Break on the target action, by default.** The action happens, the remaining touches do not go
out.

The reason is what an unbroken series says. A message asking somebody to do what they have already
done reads as not having been noticed, and it is trust lost for nothing: it happens in the first
week of a relationship, with the machinery working perfectly.

One exception exists, and it does not mean leaving the touch in place. **A touch that is still
useful after the action, covering delivery and returns, how the loyalty program works, how to use
what was bought, is not a welcome touch.** It belongs in a neighbor's post-purchase series and that
is where it moves. The test that separates them: strip out everything that pushes toward the target
action, and if what remains still makes sense, the touch was never a welcome touch and was sitting
in the series by accident. The test starts at the second touch. The first one keeps the promise the
entry point made (`entry-and-series-design.md`, step 2), you owe it whether or not anybody acts, and
it survives the strip by construction.

**3. Check the break as late as possible, not at assembly.** A queue sits between assembling a send
and sending it, and the target action happens inside that gap. A skip condition evaluated at
assembly sees only what happened before assembly: it stops the touch for everybody who acted
earlier, and sends it to everybody who acted in the gap.

The rule: the state is re-read before the send, and where it disagrees with the snapshot the send
was assembled from, the touch does not go. `lapse-and-winback` holds the same rule from the other
side, re-checking recency at selection instead of trusting the group. It is one rule seen twice:
**the snapshot a send was assembled from is not a basis for sending it.**

**4. Hand over by address at the end of the window.** The window closes with no target action, and
the person moves to whoever owns the state they are now in. The three addresses are in the table
above and none of them is "stays in the base". An unaddressed handover loses somebody without a
trace: they stop being anybody's responsibility while remaining on every list.

Separately: **somebody who stopped opening inside the window has not lapsed.** They are a few weeks
old, they have no response history for an engagement tier to be computed from (`email-program`), and
the absence horizon that `lapse-and-winback` works on has not started. They stay in the series until
the window closes.

**5. Let the record's state decide a second entry, not the flow.** Somebody unsubscribed and
subscribed again; came back from silence and registered again; arrived a second time through a
different entry point. Does the series replay?

**One fact decides it: whether this person has ever completed the target action of this series.**
Not whether they received the series, and not how much time has passed.

- **Never completed it.** The series replays. It never did its job, and the occasion that brought
  them back is no worse than the first one. It replays knowing what they already received: touches
  that landed last time are a fact on the record, and repeating them word for word is not required.
- **Completed it.** The series does not replay. This is not a new person, and introducing a customer
  to your brand as a stranger is a visible failure, and the person seeing it has already been buying
  from you. They go to the mechanic that owns their state: silent goes to `lapse-and-winback`,
  recently buying goes to the regular program.

**Why a flow cannot decide this.** A flow sees the entry event, and the entry event is identical in
both cases: the same subscription confirmation, the same source, the same hour. The fact that
separates them, whether the target action ever happened, lives on the record and is not in the
event. A flow handed this decision makes it on the only thing it has, the arrival, and therefore
replays the series for everybody.

**6. Put two limits on replaying.** First, **a replay does not start while the previous run is still
going**; the floor is the length of your own series, because two copies of one series should not run
on one person. Second, **a replay is worth running while people on a second or third run reach the
target action more often than the group they would otherwise join reaches it.** Both shares count
the same thing over the same length of time: the target action inside one window, over everybody who
entered the run or the group in that period. The comparison flatters the replay, because somebody
arriving a second time selected themselves and the group did not, so read a small gap as no gap.
When the two meet, replaying has stopped being a welcome problem and become that group's problem.

**7. Write the outcome to the profile as a state, not as a send.** A send report answers what you
mailed. It does not answer where this person is now, and that second question is what this mechanic
is about.

## Thresholds and timings

- **The window** is your own median time to first purchase (`entry-and-series-design.md`, step 4).
- **The floor on a replay** is the length of your own series (step 6).
- **The replay limit** comes from comparing two of your own shares (step 6). Do not set it as a
  count. A number of replays that is reasonable in one category means a year of correspondence in
  another.
- **The break delay** is the time between assembly and send. The larger it is, the more people
  receive a touch they should not have. Take it from your own stack; no norm supplies it.

## Edge cases

- **The target action happened in a channel your systems do not see**, offline or through a partner.
  The break will not fire, and that is a defect in how systems connect (`martech-stack`) rather than
  in the series. Until it is fixed, the series has to at least ask: a touch pushing toward a first
  purchase is written so that somebody who already bought offline does not read it as an error.
- **The basis expired before the window closed.** The basis cuts the series, not the window, and the
  remaining touches are not deferred and not sent later.
- **An unsubscribe inside the series** is an outcome, not a fault. The share of unsubscribes inside
  the window is a ballast measure, and it moves with spacing before it moves with content.
- **A second arrival while the first series is still running.** It starts nothing and is recorded as
  a source; the series continues from where it was.
- **Somebody else completed the target action**, an order placed on the same address by another
  member of the household, a registration on a shared work address. The break fires anyway: the
  series works on a record rather than on a person, and separating records is `list-building`.

## Failure modes

- **The series does not break.** The sign is people in the cohort who received a touch pushing
  toward a first purchase after their first purchase. One query finds them and the answer has to be
  zero.
- **The handover is empty.** The sign is a share of the cohort that completed nothing inside the
  window and landed in no group.
- **The series plays to customers.** The sign is purchase history among the recipients of a first
  touch. It means a flow is deciding second entry (step 5).
- **The outcome is not recorded.** The sign is that "how many people are inside the series right
  now" gets answered with an export of sends. No state exists, so none of the three checks above can
  be run.
