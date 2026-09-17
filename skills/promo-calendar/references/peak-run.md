---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Running one window: preparation, the run, and the verdict

The unit here is **one window**, from the decision to run it to the moment it gets a verdict. The
window is already in the register with its dates and its audience scope (`seasonal-shape.md`);
this file is what happens between that and the reading.

The offer inside the window is `offer-design`'s: what it is, how deep it goes, what happens when
two of them meet on one order. What belongs here is everything the date decides.

## Entry conditions

The window sits in the register with dates, audience scope and depth class. The offer is settled.
Stock or capacity is confirmed: a window nobody can serve does not open. The purchase cycle is
known, because both the shoulder and the minimum gap are measured in it.

## Exit conditions

Named: the lead time, the three stages and what separates them, the message ladder and its
ceiling, the channel ladder, the exclusion lists, the term of the cap exception, the freeze
window, and the extended window the verdict will be read on.

## Steps

**1. Derive the lead time from your own decision cycle, not from convention.** Measure it on past
purchases in the promoted category: the time from the first recorded interaction with that
category, whatever your data holds (a visit, a view, a search), to the purchase. First touch with
the business will not do, because for anybody already in the base it dates their first purchase
and says nothing about this one. The warm-up starts that far ahead of the window opening. A
considered purchase is warmed for weeks; an impulse one for days. Anybody who needs a decision
cycle to choose has started choosing before the window opens, which is what the lead time
measures; a warm-up that starts with the window reaches them after the decision. The median
reaches half of them in time. A later point of the distribution reaches more at the price of a
longer warm-up; which one you take is your call, and the plan states it.

**2. Three stages, and what separates them.** Warm-up: no offer, the argument is the assortment.
The window: the offer is live and the price claim is made. Reminders: the window is closing.

What separates the warm-up from the window is **what the recipient can do**, rather than tone or
content. During the warm-up there is nothing to buy at the promotional price, so a call to buy now
is a false statement about the window. What separates the window from its reminders is the time
left: the recipient can do the same thing in both, and the reminder says how long they have. It is
held to the same rule from the other side, since a close that claims less time than there is makes
the false limited-time claim described under the legal regime in `SKILL.md`. Both rules are easy
to break, because the warm-up and the reminders are written by the same people at the same time
as the window's own messages.

**3. The message ladder inside the window has four positions**: the announcement before the
start, the opening on day one, a reminder in the middle, and the close on the last day. Each
answers a different question, which is why four positions rather than four sends of the same
thing. Somebody who has bought inside the window leaves the ladder: the reminder and the close go
only to people who have not, because the question those two answer is one a buyer no longer has.

Cap it at four messages to one person for the window. That is a starting point rather than a
property of any market: it covers one brand and one window, service messages are not counted in
it, and you revise it against your own unsubscribe and complaint rate per window rather than
against anybody's published figure. A base that tolerates more will tell you; so will one that
tolerates less, and it will tell you by leaving.

**4. Run the channel ladder from broad and patient to immediate and intrusive.** The further from
the date, the broader the channel and the longer it can wait to be read; the closer, the more it
interrupts. This is a rule rather than a schedule, and the reason is worth stating: an
interrupting channel spends something on every send, money in some channels and the person's
tolerance of the channel in all of them, and that spend earns its price at the end of a window,
where there is no time left to reach the person any other way. A channel can be cheap per message
and still belong near the end, because what it spends is tolerance. Which channels sit where on
that ladder is yours, and it is a question of both kinds of cost rather than of a list.

**5. Ask for the cap exception before the window, not inside it.** The standing frequency cap
belongs to `contact-orchestration`, and so does the shape of the exception: raised in advance,
for a named term, falling back automatically, with its price named up front. Your request names
the window, the extra messages per person, the date the cap returns, and the number read
afterward: the window's unsubscribe and complaint rate, the same figure step 3 revises the ceiling
against. The term runs from the first warm-up message to the close, since those are the sends the
exception is for; the weeks after the close carry no window messages and need no raised cap.
Suspending the cap for a season removes the policy rather than making an exception to it, and its
owner can refuse on those grounds.

**6. Name the exclusions before the send list is built.** Three lists, and the third is not an
exclusion at all.

- **People who bought the promoted item at full price in the shoulder before the window.** They
  paid full price for what the window now sells for less, and the announcement is how they would
  find out. Whether you owe them the difference is decided elsewhere; the send list should not
  decide it by accident.
- **Holders of an outstanding promise the public window devalues.** This is the other end of the
  issuance cutoff in `seasonal-shape.md`. If the cutoff was set, this list is short; if it was
  not, this list is the reason it exists.
- **The holdout**, which is a measurement obligation rather than an exclusion. Without it the
  window has a number and no way to tell whether the messages caused any of it. Name what the
  holdout did not get: withheld from a public window's messages, it still sees the price, so it
  measures the messages and not the window; only a targeted window can hold out the offer itself.
  That is `experiments-and-holdouts`.

**7. Freeze the machinery.** Nothing in the sending stack, the loyalty processing or the catalog
integration changes inside the freeze window. It opens before the warm-up and closes after the
shoulder, and one named person can lift it.

The reason is not superstition about change. At a peak, volume, exception traffic and manual
intervention rise together, which makes it the worst moment to be telling a new failure from an
old one. Migrations and reworks go in the trough, which is what the trough is for
(`demand-shifting.md`). Duty rosters and incident handling during the window are
`program-audit-and-ops`; what belongs here is the dates and the authority to lift them.

**8. Read the verdict on the extended window.** Not on the days of the sale. The extended window
is the window plus one shoulder on each side, and the shoulder is one purchase cycle. Compare it
with the same window of the previous cycle, never with the period before it: the period before a
peak is a trough, and any peak beats it. Where the register marked this window as sharing a
shoulder with its neighbor, read the two as one span.

## Thresholds and timings

| Quantity | Value |
|---|---|
| Lead time | the median of your own decision cycle |
| Messages to one person per window | up to four, as a starting point |
| Term of the cap exception | from the first warm-up message to the close, with automatic fallback |
| Freeze window | from the start of the warm-up to the end of the shoulder |
| Shoulder | one purchase cycle |
| Comparison basis | the same window of the previous cycle |

## Edge cases

- **A fixed window lands on a competitor's dominating event.** Two legal moves: move it, if it is
  movable, or stay and accept that the verdict will be unreadable because your window and theirs
  cannot be told apart in your data. Shouting louder is a channel decision and it changes nothing
  about the calendar.
- **Stock or capacity runs out mid-window.** The window closes early and says so. Continuing to
  advertise a price you cannot serve, without saying so, is not a judgment call in the UK, where it
  is a named banned practice with no consumer-detriment test to pass.
- **The window has to be extended.** An extension can make the announced end date false after the
  fact, and that is the limited-time claim the UK bans outright and the US guides warn against,
  both under the legal regime in `SKILL.md`. If the extension also deepens the price, the EU
  prior-price rule applies to the new reduction, and whether the prior price is the one before the
  first cut depends on the Member State. Decide before launch whether the window may extend, and
  if it may, say so in the announcement from the start rather than adding days at the end.
- **A triggered flow collides with the window.** Somebody is inside a welcome series or a
  replenishment reminder when the mass send lands. Precedence is `contact-orchestration`'s. What
  belongs here is that a window is known weeks in advance, so this is a collision to be resolved
  on the calendar rather than an incident to be handled live.
- **Two brands on one base.** Two registers, one person. The cap exception is granted per person,
  so two peaks in the same week spend one person's allowance twice, and the owner of the cap sees
  one person and decides once for both brands. Resolve it in the register, a cycle earlier,
  while one of the two windows is still movable.
- **A window with no verdict by design.** Admitted under question 3 of the admission test with
  its verdict waived. Run it, and do not build the next cycle's amplitude estimate on it.

## Failure modes

**Demand was borrowed, not created.** The window sold what a shoulder would have sold at full
price. The symptom is a window that is up while the extended window is flat or down in margin, and
at least one shoulder deeper than the same shoulder last cycle. Which shoulder tells you which
mechanism: a thin shoulder before the window means the announcement taught people to wait, and a
thin one after it means the offer pulled purchases forward. Reading only the days of the sale sees
neither, and the days of the sale are what gets reported.

**The discount reached the people who were buying anyway.** Redemption concentrates in the most
recently active segment, margin falls, order count barely moves. The fix is the audience of the
window, not the depth of the offer: a public reduction reaches everybody, including everybody who
had already decided.

**The audience learned the calendar.** Slower than the other two and visible only across cycles:
full-price revenue in the shoulders falls cycle over cycle while the window itself grows, so the
year looks increasingly seasonal and earns less. Somebody who can predict your calendar and is
not in a hurry has no reason to buy off it. The countermeasure is the promotional share budget in
`seasonal-shape.md` rather than secrecy about your dates: the fewer promotional weeks a year
holds, the more waiting costs the person doing it. This failure shares its symptom with two in
`seasonal-shape.md`, and the order in which to tell them apart is written there.
