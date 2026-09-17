---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-04
---

# Program plan and cadence

A program is a repeating cycle in which every send has a slot, a tier of recipients, and an
owner. Without those three, the channel is a queue someone fills on Monday morning, and its
volume drifts upward until the audience pushes back.

## Entry conditions

- You have a legal basis to send and a list of addresses that confirmed it.
- Event history covers at least two purchase cycles, or you are starting from zero (step 9
  handles that case).
- One person owns the channel end to end. With no owner, you get a calendar nobody keeps.

## Exit conditions

The program is written down: send inventory, tiers, rhythm per tier, slot list, calendar for one
cycle, suppression rules. You do not finish the mechanic, you re-run it once per cycle, and that
review is itself a slot in the calendar.

## Sequence

**1. Inventory what already goes out.** List everything that leaves the channel in one cycle:
manual campaigns, automated flows, service messages. Count touches per person per tier, not
sends per month. Start with the automated flows: they are the ones nobody adds up, and they are
where the gap between the planned program and the real one hides.

**2. Set the planning unit.** One program cycle is the median interval between purchases in the
category, the billing period for a subscription, the deal cycle for B2B. Plan in cycles, not in
calendar months. A month means nothing in a category people buy from twice a year, and it
over-plans a category they buy from weekly.

**3. Sort the list into engagement tiers.** Use recency of response: active, occasional, dormant,
suppressed. Derive the engagement window that separates them, do not pick it. Take the period
within which most responses to a send arrive, and never let it fall below one purchase cycle. A
window shorter than the purchase cycle files healthy customers as dormant. Anyone whose history is
shorter than one window has no tier yet and carries the base rhythm until they do: a person who has
never had the chance to respond is not dormant, and filing them there is what makes them dormant.
Set the sunset in the same step, in windows rather than months: how many engagement windows without
a response end the standing program for a person, after which they get one return attempt
(`lapse-and-winback`) and the record's fate is `list-building`'s.

**4. Assign a rhythm per tier.** The base rhythm belongs to the active tier. The occasional tier
gets a fraction of it. The dormant tier gets anchor sends only. The suppressed tier gets nothing
but service messages and mandatory notices, which are not marketing and do not turn into marketing
because the program has no slot for them.

**The rhythm yields to a delivery ceiling.** While `deliverability` runs a warmup or a placement
recovery, the volume ceiling it sets outranks the planned rhythm, and the rhythm holds still for
the length of each of its steps instead of moving one step per cycle. Change both at once and you
can read neither the provider's reaction nor the program's. One rhythm for the whole list is a starting state: it is what a program
looks like before you have enough data to tell the tiers apart, and you leave it behind as soon
as you do.

**5. Define the slots.** Every recurring send gets one: purpose, recipient tier, frequency,
owner, and what happens when there is no material for it. Keep a reserve of subjects that are
not tied to an occasion. A slot you cannot fill is what breaks the rhythm, and once the rhythm
breaks, people stop expecting the mail.

**6. Write the suppression rules.** You execute them in `send-selection-and-suppression.md`, but
you decide them here. They belong to the program, not to whoever assembles a given send.

**7. Lay out the calendar for one cycle.** Anchors first: the rows of `promo-calendar`'s register
that fall inside the cycle, product events, anything that cannot move. The register is built before
the channel calendar and the anchors are read off it, because where demand peaks is a fact about
the category rather than something a channel can work out; a calendar laid out first will fit the
year around its own rhythm and meet the peak late. Slots fill what remains. Leave one slot unassigned as
reserve. Split the calendar into two groups, sends that go on a fixed date and sends that can
float to a better day. Only the first group blocks anything.

**8. Change rhythm only by test.** One step per tier per cycle, one variable at a time. Change
rhythm and content in the same cycle and you get a result nobody can read. Test design belongs
to `experiments-and-holdouts`.

**9. Starting from zero and restarting are two cases.** With no sending history at all, open with a
single slot to recent subscribers and recent buyers. Recency of the relationship is the only signal
you have; it stands in for response rather than measuring it, so say that, and replace it as soon
as your first sends produce a response history. Restarting a program that has sent before is the
other case, and there you pick the audience by recency of response to mail and widen it one notch
at a time. An audience picked on purchases contains people who never open anything, and opens and
clicks are what the provider reads, so a ladder built that way advances on signals from people who
were never going to respond. In both cases volume follows the audience rather than the calendar,
and the ramp itself belongs to `deliverability`. Tell people at signup how often to expect mail,
then match it: the first cycle sets the expectation the rest of the program lives with.

## Thresholds and timings

None of them is a market norm. The windows you compute from the program's own data; the counts are
starting points this skill chose, and they are marked as such.

- **Engagement window:** at least one purchase cycle, otherwise the period containing most
  responses to a typical send. Computed.
- **Sunset:** a stated number of engagement windows with no response. Computed from the window,
  and the number of windows is yours to set and to defend.
- **Rhythm change step:** one send per tier per cycle, in either direction. A starting point.
- **Reading a change:** no conclusion before two full cycles have run under the new rhythm. A
  starting point, and the one to revisit first in a category with long cycles, where two cycles can
  be a year.
- **Subject reserve:** at least one slot's worth, held at all times. A starting point.
- **Tier recalculation:** once per cycle, before you lay out the calendar.
- **Ramp step when starting from zero:** set by delivery state, not by a volume target.

## Edge cases

- **The list is too small to tell tiers apart.** Do not split it. Run one rhythm and compare the
  program against its own periods. Splitting a small list gives you four groups of noise.
- **No purchase history**, because the business is new or the product is bought once. Derive the
  cycle from product events instead: signup, activation, usage milestones.
- **Seasonal category with no interval between purchases.** Replace rhythm with season windows:
  dense inside the window, anchors only outside it.
- **The list is growing fast.** Recalculate tiers every cycle, and keep the newest arrivals out of
  the calculation until they have seen one engagement window. Recalculating alone does not save
  them: at every recalculation somebody who has never been mailed still has no response to show,
  so they file as dormant, receive anchors only, and stay there by construction.
- **Low-frequency, high-consideration category**, bought once in several years. Content carries
  the program, the selling slots hang off anchors, and you read the control metric per cycle
  rather than per send, because single sends will show nothing.
- **B2B.** The cycle is the deal cycle, the mix leans to content over offers, and the calendar
  respects the buying organization's dead periods: end of quarter, end of financial year,
  holiday shutdowns. Those periods move response itself, not only how much you send.
  Lifecycle work before the deal belongs to `b2b-lifecycle`. After the deal, `b2b-retention` gives
  each stage of the contract term an ownership class, and the class decides whether this program
  may send at all: under an account manager's class it sends only from the allowed set that skill
  names, and a stage with no class has no right to send. Read the class before the tier. The rhythm
  changes here, the reasoning does not.
- **Two brands or two markets on one platform.** They are two programs with two calendars, even
  when they share a template. Merge them and you lose track of which one carries the number.

## Failure modes

How you see that the mechanic is not working, and what you do about it.

- **Revenue per recipient falls for two consecutive cycles while volume rises.** Separate the two
  kinds of volume before you act, because the metric answers them differently. More touches to the
  same people leave the denominator where it was, so a fall means the extra sends earned nothing:
  the program is buying revenue with load. Wider reach adds people to the denominator, and a fall
  there is arithmetic rather than fatigue, which is why total channel revenue is read next to it: if
  the channel earns more in total, reach is working. Freeze volume and switch to
  `declining-returns.md` in the first case; in the second, decide whether the reach is worth its
  cost and record the decision.
- **Unsubscribes and complaints rise in a tier right after its rhythm went up.** Roll that tier
  back one step. This is the only change you revert without waiting for the cycle to finish,
  because you pay for the wait in list damage.
- **Slots sit empty and sends get assembled at the last minute.** The slot count exceeds what the
  team can carry. Cut slots until the calendar is executable. Trying harder does not fix it: the
  rhythm is the asset, and the rhythm fails first.
- **Tiers do not differ in response after two cycles.** Recency of response carries no
  information for this audience. Return to one rhythm and look for a different signal.
  `segmentation` owns that search.
- **Nobody can say who owns a slot.** You have a habit, not a plan. Restart at step 1.
