---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# Entry points and the shape of the series

The work does not start with a message. It starts with a list of entry points, and until that list
exists any series you build serves one of them and silently fails to serve the rest.

This mechanic takes you from "we should welcome people" to a specification you can build, price and
read afterwards: one specification per entry point.

## Entry conditions

A neighbor has produced a contact with a basis recorded and a marketing state attached: a capture
point on the site (`onsite-capture`), an enrollment (`loyalty-program-launch`), an offline channel
or an import (`list-building`). The arrival event is on the profile in a source field.

## Exit conditions

A specification per entry point: the promise, the target action, the window, the number of touches
and the spacing between them, the channel, a send condition and a skip condition on every touch, and
the mark that says the series has finished.

## Steps

**1. List the entry points and do not merge them.** An entry point is not a traffic source and not a
form. It is a **promise**: what the person believes they got in exchange for the contact. A
newsletter signup, an account registration, a lead magnet, a purchase without registration, a
loyalty enrollment, an inquiry or a callback request are six different promises.

Two entry points share one series only when **the promise and the target action both match**. One of
the two matching is not enough, and the failure is visible from outside: the first message thanks
somebody for subscribing who placed an order and never subscribed to anything.

**2. Write the promise down verbatim, before the first touch is written.** What exactly was offered:
a discount, a guide, a notification when something is back in stock, access to a trial. **Whatever
was promised is delivered by the first touch and before anything else.** Until the promise is kept,
the program has no standing to ask for anything, not data, not a second channel, not a purchase.

The content of the first touch is set by the capture point rather than by the program. The wording
is `email-copy`, but copy cannot restate the promise in different terms: a promise reads as kept
when the person recognizes the words they saw.

**3. Name one target action.** The thing the series exists for and breaks on: a first purchase, an
activation event (see `activation-and-first-value.md`), an enrollment, a completed profile. Two
target actions mean the series ends on neither, because breaking on the first leaves the second
unreached and breaking on the second leaves the first unreached.

The target action has to be an event your systems see when it happens rather than in an overnight
export (`martech-stack`). An event visible a day late breaks the series a day late, and that is
exactly the day somebody is asked to do what they have already done.

**4. Compute the window.** The length of the series is **your own median time to first purchase,
computed on the people who did buy**. It is not thirty days. Thirty is a name for the problem, not a
parameter of it. A long purchase cycle gets a long window, a short one gets a short window, and both
get it from their own data.

`rfm-segments` computes the same figure to decide who is not in the grid yet, and the agreement is
not a coincidence. Below that median, an absent purchase is not yet a fact about the person, which
is why they belong to this mechanic; above it, it is, which is why they leave.

Compute it on arrival cohorts old enough to have finished buying. A cohort younger than the window
you are estimating cannot show you its own late buyers, so the median comes back short, the series
comes out shorter still, and the error runs in the direction that hides itself. Where you have too
few purchases for a median at all, take the longest run you hold, mark the window as provisional in
the specification, and recompute once you have two full purchase cycles.

**5. Derive the touch count and the spacing from the window, in that order.** A series is not "three
emails". It is as many touches as fit in the window at a spacing you can defend, and the spacing is
set by **the regular program that starts afterwards**: no tighter inside the series than what the
person will receive once it ends.

The reason is expectation, not volume. A daily series in front of a weekly program teaches somebody
to expect a message a day; when the series ends the frequency drops fourfold and reads as having
been dropped. The same effect runs the other way: a series spaced wider than the regular program
fits fewer touches than you sized the window for, and the regular program reaches the person before
the series has finished.

**6. Put a send condition and a skip condition on every touch.** The send condition says which state
lets the touch go. The skip condition says which state makes it not go while the series continues.
Skipping and breaking are different things: a skip removes one touch, a break closes the series (see
`exit-break-and-second-entry.md`).

Skip conditions are named **before launch**. Added afterwards they are not free: everybody already
inside the series needs their state rewritten by hand, and for anybody who received the skippable
touch yesterday there is nothing to do at all.

**7. Check that the series does not double the regular program inside the same window.** Somebody
inside the series is still in the base, and the regular campaign knows nothing about them. How many
messages one person gets in total, and what yields to what, is `contact-orchestration`. Naming the
collision is this skill's obligation, because inside the window a second program is running on every
person in the cohort by construction rather than by chance.

**8. Walk every branch by hand before launch.** Five checks carry over from ordinary flow work: the
trigger fires on a real action; every behavioral branch goes where it should; the message renders;
links and substitutions resolve; the timings are what the specification says. Add one that belongs
to this mechanic: **walk the series as somebody who completed the target action right after the
first touch**, and confirm that nothing else arrived.

## Thresholds and timings

- **The first touch fires on the basis being recorded, not on the form being submitted.** Where the
  capture point confirms the address, it fires on the confirmation; where it does not, on the basis.
  No figure is needed here, because it is an ordering rule, and it is what keeps a series off an
  address that does not belong to the person who typed it.
- **Spacing is no tighter than the frequency of the regular program** (step 5), computed from your
  own sending plan and not chosen by hand.
- **The length of the series is the window** (step 4), computed from your own median time to first
  purchase.
- **The touch count is derived**: the window divided by the spacing. If that gives one touch, the
  window is shorter than the spacing, which says the regular program is too infrequent for this
  category, not that the series should hold one message.

## Edge cases

- **An entry point exists and has no series.** Those people are still in the arrival cohort and
  still in the denominator of the control metric. Two ways out: build a series, or map the entry
  point explicitly onto an existing series whose promise matches. Silence is not a third way out, it
  is the silent loss.
- **The promise cannot be kept when the first touch is due**, because the promo code ran out or the
  guide was withdrawn. The fate of an issued promise is `offer-design`; the rule here is narrower.
  The first touch does not go out carrying a dead promise, and the series waits for a replacement. A
  touch that keeps a promise with an excuse is worse than a late one.
- **The contact arrives in a requested message state.** Somebody asked to be told when one item is
  back in stock and nothing more. That is not an entry into a series: the capture point handed over
  one fact and not permission for a program. A series starts on the marketing state only.
- **One person arrives twice in quick succession through two entry points**, subscribing and
  registering the same day. One series runs, the one whose promise was made first; the second point
  is recorded as a source and starts nothing. Otherwise the person gets two first touches and both
  of them say hello.
- **The target action happens before the first touch**, when somebody subscribes and buys in the
  same session. The series does not start; the person goes to the post-purchase mechanic. These
  people sit in the arrival cohort with a target action the series did not produce, so watch the
  size of that group in the control metric. Once it is large enough to move the number, the capture
  point stands after the purchase instead of before it, which is a question for `onsite-capture`.

## Failure modes

- **The series is healthy and the cohort is not growing.** The sign is a share of the arrival cohort
  that entered no series at all, larger than zero and unexplained. The cause sits at a seam and not
  inside the series: an entry point with no mapping, a basis that was never recorded, a pending
  state that never resolved, an address undeliverable from day one. Find it by comparing two
  numbers, how many arrived and how many entered, and put that comparison in the cohort report.
- **One series for every entry point.** The sign is unsubscribes and complaints concentrated on the
  first touch rather than spread across the series. The first touch is talking to the wrong person:
  they did not subscribe, they placed an order.
- **The series outlives its basis.** This one is not visible in a metric, it is visible in the
  specification: the window was computed from a purchase cycle while the entry point gives the basis
  a shorter life. The series has to be shorter than the basis, and the legal section of `SKILL.md`
  says which entry point gives which.
