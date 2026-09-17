---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# Activation: getting somebody to a first value

Some products are used before they are paid for. A trial, an app, a subscription, a membership. In
those the target action of the welcome series is not a purchase but a use, and picking which use
counts is the decision the rest rests on. Pick it badly and every number afterwards is measured
against the wrong thing.

## Entry conditions

The product is used before it is paid for or repeated, and the target action of the series is a use
rather than a purchase. **Where the purchase is the first action, this mechanic does not apply**,
and the skill runs on the other two. That is a normal outcome and not a gap.

## Exit conditions

A named activation event in the form "X actions in Y days from arrival", chosen by the two-sided
criterion and by reach, and tested for causation, plus the path to it broken into a setup step and
touches placed at the drops.

## Steps

**1. Start qualitatively and confirm quantitatively.** A search that starts with correlations finds
a marker rather than a cause: any action taken by engaged people correlates with their success,
because they are engaged. Start by talking to people who got there. Why they came, what your product
replaced, at which point they decided to stay. The output of this step is a list of candidates, not
an event.

**2. Split by the job somebody arrived with.** One product serves several jobs, and each has its own
moment of value and its own path to it. The job is learned three ways, in descending order of
reliability: from what you already know, meaning the landing page, the source, the plan; from a
question at registration; from the first behavior.

Two rules govern the question at registration and both are operational. **Do not ask what you
already know**: somebody who arrived from a page about one use case gets it preselected and the
option to change it. **Do not make the answer mandatory**: a mandatory answer does not produce data,
it produces a random answer, and the whole path afterwards is built on it.

**3. Write the candidates in one form.** The form is **"completed X actions in Y days from
arrival"**. Neither parameter is filled in yet. What matters at this step is that candidates are
comparable to each other, not that they are precise.

**4. Pick the event with the two-sided criterion, then check you can reach it.** Compute three
numbers for every candidate:

- **the share who reached success among those who did the event**, read against the success rate of
  all arrivals and not on its own;
- **the share who did not reach success among those who did not do the event**, read the same way,
  against the failure rate of all arrivals;
- **the reach**: the share of arrivals who do the event at all.

The first two say how well the event separates, and a level on either one misleads, because the base
rate pulls both. Where most arrivals never convert, almost every candidate scores high on the second
share. An event almost everybody does scores on the first share whatever the base rate is, and its
non-doers are too few a group to read anything from. What you look for on both shares is distance
from the base rate, in the same direction, on the same candidate.

The third number decides between candidates that separate equally well, and the other two do not
substitute for it. An event only a few people ever do can separate perfectly and still fail as a
goal, because no series leads most people to it.

Take a worked example with invented numbers rather than an observed case: 18% of all arrivals go on
to pay, candidate A is done by 8% of arrivals and 52% of those pay, and candidate B is done by 46%
and 24% of those pay. Both sit above the base rate, so both separate, and A separates harder. On the
second share the two are barely distinguishable, 85% against 87%, which is what a base failure rate
of 82% produces and why that share settles nothing on its own. A is the strong marker and the poor
goal, B is the weaker marker and the usable goal, and reach makes the difference.

**5. Find the setup step in front of the event.** Look for a piece of setup between arrival and the
event: the thing without which the event either cannot happen or happens to no effect. Where there
is none, skip this step. Work backwards to find it: take the people who did the event and look at
what they did first; take the people who started and did not finish and look at where they stopped.

The setup step is a target for touches in its own right, and it must not be folded into the event.
Somebody who finished setup without doing the event and somebody who never started setup need
different messages.

**6. Place touches at the drops, not on a calendar.** Break the path from arrival to the event into
steps, compute the share who move from each step to the next, and place a touch where the share
falls. This is what separates an activation series from a welcome series: the welcome series is
spaced by rhythm, the activation series is spaced by where people stop.

**7. Build around the single most common path first.** While there are several jobs and not enough
resource for all of them, take the most common one and add the others one at a time. An averaged
path is made of steps that each serve part of the arrivals, so it costs more than a single path and
serves every job worse than a path built for that job.

**8. Prove causation with a test.** Everything steps 3 to 5 produce is an association. It becomes a
cause when groups assigned at random to what pushes toward the event (the guidance, the nudge) differ
in outcome; comparing people who reached the event with people who did not compares different
people. The design of that test is `experiments-and-holdouts`. Until it is run, the event is a hypothesis and the specification says
so in that word.

## Thresholds and timings

- **The form of the event is "X actions in Y days"**, fit both parameters to your own data and
  record the date you fit them. An event without Y is not an event: "connected the integration" with
  no window does not separate somebody who did it on day one from somebody who did it in month
  three.
- **Y is no longer than the window of the series, and no longer than the trial period** where one
  exists. An event that lands after the trial ends cannot be the goal of a series running inside it.
- **The number of setup steps between arrival and the event.** If there are more than a person
  completes in one session, the event is too far away: the only people who reach it are those who
  came back on their own, and the series was not losing those. Check it against your own
  distribution of sessions to the event.

## Edge cases

- **There are no candidates, because the product is too simple.** Activation coincides with the
  purchase and this mechanic does not apply.
- **The base is too small for the two-sided criterion.** Keep the qualitative part, name one event
  out loud as a hypothesis, with that word in the specification, and fit the numbers later. A
  hypothesis called a hypothesis is worth more than an event found on twenty observations.
- **Almost everybody does the event.** That is not an activation event, it is a step on the way: it
  does not separate the people who got there from the people who did not. Take the next one along
  the path.
- **There is no behavioral data from inside the product.** Activation cannot be defined, and the
  first job is getting events into the systems (`martech-stack`). Until then the mechanic does not
  work even qualitatively: interviews will produce candidates and there will be nothing to test them
  against.
- **The job changed on the way.** Somebody arrived for one thing and found value in another. The
  sign is that the event for their stated job never happened and they stayed. This is a candidate
  for a different path, not a failure.

## Failure modes

- **Onboarding gets completed and activation does not move.** The sign is a rising share who finish
  the tour against a flat share who reach the event. The onboarding was built around the interface
  instead of the job, and a long product tour gets clicked through to the end, which counts as
  completion.
- **The event was chosen on reach alone.** The sign is that the thing being called activation is
  done by almost everybody who arrives. It separates nobody, its share among doers sits on the base
  rate, and counted as a total it rises whenever traffic rises.
- **Qualification at registration collects noise.** The sign is that the distribution of answers
  does not vary by source although the sources do. People are answering to get past the screen.
