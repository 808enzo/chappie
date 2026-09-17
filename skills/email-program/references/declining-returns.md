---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-04
---

# Declining returns: diagnosis and recovery

A falling channel has a short list of causes. The order below is not a ranking by what a check
costs: it runs by dependency, because each step can invalidate the reading of every step after it.
A broken attribution makes the load number meaningless, mail that does not arrive makes every
response number a shadow, and a base that stopped growing changes the mix the later steps read.
Work it out of order and you rewrite copy for a problem that turns out to be an attribution change.
Where two steps do not depend on each other, take the cheaper one first.

## Entry conditions

- The control metric, revenue per recipient per cycle, has fallen for two consecutive cycles
  **while total channel revenue did not rise**; **or** the channel's share of revenue is falling
  while send volume stays flat. A metric falling because the program reached more people while the
  channel earned more is arithmetic, not decline, and it does not open the mechanic.
- One cycle is noise and does not open the mechanic. Act on one cycle and you change rhythm every
  cycle, which leaves you with a program you can never read.
- Your comparison is like for like: same season, same definition, same attribution. Establish
  that before you enter, or step 1 will establish it for you.

## Exit conditions

The metric holds across two consecutive cycles, and you have either walked volume back up to
plan in steps or left it below plan on purpose. Leaving it below plan is a legitimate exit: a
smaller program that earns beats a large one that does not.

## Sequence, and the order is the mechanic

**1. Rule out a measurement artifact.** Did attribution change? Did link tagging break? Did the
report window or the denominator change? Did the way you count opens change? Opens are the softest
number here. A mailbox provider that prefetches records opens no human made, and when your sending
platform changes what it filters out of those, the reported figure moves in either direction with
nothing happening in the program. Image blocking works the other way and removes opens that did
happen. Read a move in opens as a reason to check the counting method, not as a reading of the
program.
Restore comparability first. When the drop lives here, stop: there is nothing to fix in
the program.

**2. Rule out delivery.** Inbox placement, bounces, complaint volume. When mail does not arrive,
every downstream number is a shadow of that, and no program change moves it. This is
`deliverability`'s work. Come back here when it is resolved. Read it by provider rather than
averaged: a fall that sits in one provider is placement, and it also means the tier demotions of
that cycle are reading silence the program caused.

**3. Rule out list composition.** Is the active share shrinking? Has the inflow of new
subscribers dropped? A channel fed by a capture surface that stopped converting decays for
months while the program itself stays unchanged. That belongs to `onsite-capture` and
`list-building`, not here.

**4. Check load.** Have touches per person risen, counting automated flows and counting the other
channels the same person is on? When load has risen, **reduce before you add**. Teams skip this
step, because the intuitive answer to a falling channel is more sends, and more sends is what
deepens the decline when fatigue is the cause.

**5. Check program composition.** The share of selling slots against the rest, how often the same
subject repeats, how much volume goes to the dormant tier. A program drifts to promotion-only one
urgent request at a time, and you see the drift only when you list the slots side by side.

**6. Only now, offer and content.** When steps 1 to 5 come back clean, the problem is what you
say or what you offer, which puts it in `email-copy` and `offer-design`. Reaching this step with
the earlier ones ruled out is a useful result: it tells the copy team the problem is theirs.

## Recovery

Run these in order once you have the cause:

1. **Freeze volume.** No new slots until the metric holds for a cycle. The freeze is what makes
   every later change readable.
2. **Narrow mass sends to the active tier.** The dormant tier gets anchors only, or one
   deliberate return attempt run as its own campaign. That campaign belongs to
   `lapse-and-winback`, not to the standing program.
3. **Restore suppression rules** switched off during the push that preceded the decline. Check
   each rule against the plan rather than asking whether anyone changed one.
4. **Move rhythm one step per cycle**, in the direction the diagnosis pointed.
5. **Walk volume back up in steps** once the metric is stable. A step is one widening of the
   audience by recency of response, and it is authorized by signal rather than by the calendar:
   refusals, complaints, the provider's reputation reading and response itself, all of them read
   per provider (`deliverability`, which owns the ladder and whose ceiling outranks the plan while
   it runs). Stop at the step where any of them moves the wrong way, and treat the step below it as
   this audience's ceiling.

## Thresholds and timings

- **Entry:** two consecutive cycles of decline.
- **Measurement after any change:** not before the end of the cycle in which you made it.
- **Variables changed at once:** one.
- **Comparison basis:** the same period of the previous seasonal cycle, not the previous month.
- **Stability, for exit:** two consecutive cycles.
- **Ceiling:** the volume step at which complaints move. One step below it is your working
  ceiling.

## Edge cases

- **The decline coincides with a season.** Compare year over year. Month-over-month comparison in
  a seasonal category gives you a false diagnosis every time the season turns.
- **The decline follows a list cleanup.** Absolute totals fall while rates rise, which is the
  cleanup working. Read revenue per recipient and total channel revenue separately, or the
  cleanup looks like the cause.
- **One large segment explains the whole drop.** Fix the segment. Do not restructure the program
  around one cohort's behavior.
- **A platform migration or a change of measurement method sits inside the window.** The series
  does not compare across it. Build a new baseline and start the clock again. There is no honest
  diagnosis across that seam.
- **A promotional peak masks the decline.** Peak weeks flatter everything. Exclude them from the
  comparison, then check whether the program outside the peak has been decaying for cycles.
- **The channel falls because another channel took the same demand.** Total customer revenue
  stays flat while email's share drops. Read it on the person across channels, as
  `contact-orchestration` reads revenue per reachable person, not as a program failure, and it is the case where fixing email hardest does the most damage.
- **Sends were paused for a period.** Response after a gap does not compare to response during a
  steady rhythm. Treat the restart as a ramp, per `program-plan-and-cadence.md`.

## Failure modes

- **You ran the full sequence, two cycles passed, delivery and list are clean, and the metric has
  not recovered.** The cause sits outside the channel: the offer, the assortment, the price. You
  cannot repair the channel from inside it. Escalate, and say which of steps 1 to 5 you cleared,
  so the next owner does not repeat them.
- **Every step returns "not confirmed" and you have no holdout.** Your conclusions are not
  trustworthy. Without a control group, a flat metric during a market-wide decline looks
  identical to a program doing nothing. The one that answers this is a control drawn from the base
  and rotated, reading revenue per person assigned rather than attributed revenue, since there is
  nothing to attribute in a group that received nothing. Put it in place before you continue
  (`experiments-and-holdouts`).
- **The metric recovers only through cuts, and total channel revenue keeps falling.** You are
  holding rates at the cost of reach. Record the volume floor below which the channel stops
  contributing, and take the trade-off to whoever owns the channel's target instead of settling
  it alone.
- **You run this diagnosis every cycle.** You are managing the program by rescue. Stop
  diagnosing and rebuild the plan.
