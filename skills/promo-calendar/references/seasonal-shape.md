---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# The shape of the year, and what earns a place on the calendar

The unit here is **the window**: a dated span with an offer inside it, addressed to a named
audience. It is a larger object than anything the neighboring skills count. `email-program`
counts a send, `triggered-messages` counts an entry into a flow, `offer-design` counts one offer;
a window holds several of each and is decided a year at a time.

This file produces a register of windows. It does not build the sends inside them and it does not
price them.

## Entry conditions

Revenue or order history by period for at least two full cycles, stitched across every sales
channel (`list-building`, `martech-stack`). The interpurchase interval of the category is known
or computable (`repeat-purchase`); the shoulder and the minimum gap both come from it. And you
know which periods of the past carried promotions: without that the index can be computed but not
read.

## Exit conditions

Named: the period unit, the index of every period across two or three cycles, the separation of
season from trend, the amplitude band, the admitted occasions with the reason each was admitted,
the register with dates and audience scope, the promotional share of the year, and an issuance
cutoff for each kind of promise in front of every window in the register. The register is
reproducible: two people working
independently arrive at the same one.

## Steps

**1. Choose the period unit before computing anything.** Two limits set it. It can be no coarser
than the shortest window you intend to place, or step 5 cannot tell whether an occasion moved
anything. And each period has to hold enough orders that an unpromoted period keeps its rank from
one year to the next: start at the finest unit your data allows, and coarsen while unpromoted
periods jump rank between years. The purchase cycle does not set the unit. It sets the shoulder
and the gap between windows, which is where this file uses it.

**2. Compute the index of each period against the average period of the same year, after taking
the trend out.** Revenue, or orders, of the period divided by the average period of that year.
Not against last year, which puts the trend into every figure. And not on raw revenue unless the
business is flat: in one that grows steadily, the late periods of every year sit above that year's
average, the rank repeats year after year, and growth passes the season test in step 3. Fit a
straight line through the whole history, divide each period by the line's value at that period,
and index what is left. In a flat business the line is level and changes nothing. Do it separately
for each of the last two or three cycles.

The indexes of one year sum to the number of periods in it, which is arithmetic and is worth
checking, because a set that does not sum means the periods do not tile the year.

Three cycles where the history allows, two as the floor. That is a starting point rather than a
property of any market: it holds where the assortment is comparable across those years, and it
stops holding the moment a category with a different rhythm is added (see the edge cases). Revise
it every cycle, and use the test in step 3 to tell whether what you have is worth keeping.

**3. Separate the season, the trend and your own calendar.** Three things look alike on a chart
and want three different responses.

| What you have | How it shows | What to do |
|---|---|---|
| A season | the same periods sit above average, cycle after cycle: the rank is stable | build the calendar on it |
| A trend | the level moves across the whole history, and within each year it tilts toward one end | it is not a calendar question; the line in step 2 takes it out, and a tilt left in the index is a trend posing as a season |
| Your own calendar | the rank is unstable and its highs sit where your promotions sat | the index is measuring you |

**This is the sharpest point in the mechanic.** If those periods were promoted, the index proves
peaks you created. The test is to recompute the index on the part of the assortment that was not
promoted in the periods you are testing. If the peaks survive there, the season is real. If they
flatten, you had no season, you had a habit.

Run it on the unpromoted assortment rather than on full-price revenue across everything. A
promotion moves the promoted items' sales off full price, so full-price revenue in a promoted
period falls by construction, and a real season flattens under that version of the test as surely
as a habit does. Where every item was promoted in the same period every year, nothing is left to
recompute on: the season cannot be told apart from your calendar, the register marks that peak as
unverified, and the next cycle leaves part of the assortment at full price in it so the test can
run.

**4. Name the amplitude band.** Three bands, cut on your own distribution: the peak comes to a
multiple of an average period, the peak differs by a fraction of one, or the peak barely stands
out. The band is not a label to file the business under. It says whether the year has a shape to
build on at all: where the peak barely stands out, the windows are occasions of your own set
against a flat year, and each is read against that. Which of the next two mechanics has work to
do is decided by what constrains the peak, in step 1 of `demand-shifting.md`, and not by the band.

I do not have a citable benchmark for what counts as a deep season, and one would not help, since
the amplitude is a fact about your assortment and your prices. Cut the bands on your own index.

**5. List the candidate occasions and admit them one at a time.** Candidates come from three
places: every local maximum of the index, which is an occasion whether you act on it or not; a
dated event outside the business that the audience already acts on; and an event of your own.

Admission is a test of three questions, and an occasion is admitted only if every question that
applies to it answers yes.

1. **Does it move this assortment?** Not whether it is popular.
2. **Does the audience act on it without you?** If purchases do not rise in that period even when
   you are silent, the lift you saw was your own promotion and not the occasion; read it on the
   unpromoted assortment from step 3. An event of your own fails this question by construction,
   since nobody acts on it before you announce it. It skips question 2 and is admitted on
   questions 1 and 3 and on the budget in step 6, as a window whose demand you create.
3. **Can you tell it apart in the data?** An occasion whose window is buried under a larger one
   may still be run, but it will never get a verdict, and that has to be said before the launch
   rather than discovered in the report.

**This skill ships no list of dates.** A calendar of holidays is a fact about one market in one
year: it goes stale, it does not travel, and it quietly tells a reader on another continent to
run somebody else's year. What travels is the test above. Apply it to your own market and your
own assortment, and the list you get is yours.

**6. Place the admitted windows and resolve the collisions.** Fixed windows first, since nothing
about them is negotiable, then the movable ones into what is left. Two placement rules.

- **The minimum gap between two windows addressed to the same people is one purchase cycle.**
  Closer than that and the second window is selling to somebody who bought in the first, at a
  discount, having already paid for them once. Where the two audiences only partly overlap, the
  gap binds the people in both: keep it, or take the overlap out of the later window. The gap is
  a floor for placement and not enough for reading. A shoulder is also one purchase cycle, so two
  windows at the minimum gap share a shoulder, and the register marks such a pair to be read as
  one span (the control metric in `SKILL.md`).
- **The promotional share of the year is a budget, not a residual.** Decide in advance what share
  of periods, and what share of revenue, may go at a promotional price, and refuse the window
  that breaks it. Left as a residual the register fills on its own: every window is justified on
  its own merits and the year ends up as one long sale. The share of periods is known when a
  window is admitted, the share of revenue only after it runs: admit on the period share and a
  forecast of the revenue share, and carry the actual revenue share into the next cycle's budget.

**7. Check outstanding promises before fixing a date.** A promise already in somebody's hands
cannot be shortened, and that is `offer-design`'s rule, not a matter of taste. It does not leave
the calendar powerless, because **the calendar's unit of control is issuance rather than
redemption**. Promises in circulation are a wall in the year with a known expiry, and the job is
to see the wall before placing the window.

Set an **issuance cutoff** for each kind of promise you issue: the window's start minus that
promise's redemption window (`offer-design`'s term for how long it can be used). After its cutoff
you stop issuing that kind, because every copy issued later is still live when the window opens.
A shorter-lived promise keeps its later cutoff. Stopping all issuance at the earliest cutoff is
safe and wider than it needs to be; where some promise lives longer than the gap between two
windows, it would stop that promise for good.

Three legal moves when a promise and a window do overlap, and one that is not available:

1. Move the window out of the overlap, if the window is movable.
2. Keep the window and honor the promise inside it, deciding **before launch** whether the two
   may stack. The collision rule is `offer-design`'s; what belongs here is not discovering the
   question in the middle of a peak.
3. Stop issuing at the cutoff, which is the move the calendar owns outright.

Not available: shortening or withdrawing a promise in circulation, and equally the quieter
version, letting it stand while a deeper public price makes it worthless. The second breaks no
rule and lands worse, because the person is looking at proof that their personal promise was the
weaker offer.

**8. Publish the register.** One row per window: occasion, start, end, audience scope, depth
class, fixed or movable. The register is the output of this file and the input of several
neighbors. `email-program` lays its anchors on it. `contact-orchestration` reads it to grant cap
exceptions with terms. `repeat-purchase`, `rfm-segments` and `crm-reporting` use it to tell which
cohorts were recruited inside a window, which is why every first order closed inside a window
carries the occasion tag.

The register also answers the overlap `repeat-purchase` leaves here. A cohort recruited inside a
window has its own cohort window for the second purchase, and any later window addressed to those
people that opens before that cohort window closes is an overlap. Name it on the cohort: a second
purchase made inside the overlap was bought on an offer, and the reader counts it and flags it
rather than pooling it with the rest.

## Thresholds and timings

| Quantity | Value |
|---|---|
| History behind the index | three cycles where available, two as the floor |
| Sum of one year's indexes | the number of periods in the year |
| Gap between windows at the same people | one purchase cycle to place them; two to read them apart |
| Register rebuilt | once per cycle, before the channel calendars are laid out |
| Promotional share of the year | set by you, reviewed once per cycle |

The order in that last-but-one row matters. The register is upstream of the channel calendar: a
channel that has already laid out its slots will fit the year around its own rhythm and discover
the peak late.

## Edge cases

- **Less than two cycles of history.** You have no index, and you cannot borrow one. A public
  series of search interest for the category will give you the **shape** of a year, but not your
  amplitude, and amplitude is what the next two mechanics act on. Mark the first register
  provisional and rebuild it from your own data at the first full cycle.
- **Demand driven by weather.** The date moves from year to year, so fix the window to an
  **opening condition** rather than to a date: name the threshold in the observable that drives
  it, and build the window in advance so it can open on short notice. A calendar pinned to last
  year's dates is wrong in every year the weather moves, and it is wrong in both directions.
- **More than one peak.** Then the trough is not a period but the space between peaks, each peak
  has its own shoulders, and the peaks are not read pooled. Two peaks of different amplitude
  pooled produce an average year that does not exist.
- **B2B.** The cycle is the customer's budget cycle rather than the retail year: fiscal year end,
  quarter ends, and the holiday troughs of the buying organization. The occasion is a budget
  moment and the audience is a role. The construction of that is `b2b-lifecycle`; what belongs
  here is that the period unit is theirs and not yours.
- **A new assortment with a different rhythm.** The blended index stops meaning anything as soon
  as two categories with different shapes both carry material revenue. Compute per category from
  that point, and keep the blended figure only for reporting.
- **An occasion that cannot be separated in the data.** Admitted under question 3 above with its
  verdict waived. Run it if the reason is good; do not later present its numbers as a result.

## Failure modes

**The calendar measures itself.** The index is built on promoted periods and proves the peaks you
made. It gets stronger every cycle, the trough gets deeper, and full-price revenue per period
falls while the chart looks more seasonal than ever. Diagnosis is the recomputation on the
unpromoted assortment in step 3. This one is comfortable to have, which is why it survives.

**The register fills up.** Every window is justified on its own, the promotional share climbs
cycle over cycle, and nobody owns the total. The symptoms are the promotional share of revenue
rising while margin per order falls, and the shoulders of each window flattening until there are
no full-price weeks between them. No single campaign report shows it, because in each report the
window did well.

**An occasion admitted for the wrong audience.** Demand for the occasion exists, but not in your
assortment: engagement in the channel is high, and revenue over the extended window is no
different from an ordinary period. It survives because the channel metrics look like success.
Question 1 of the admission test is the one that was skipped.

**Two of these failures and two in `peak-run.md` share symptoms, so read them in order.**
Full-price revenue thins between windows while the windows grow in the calendar measuring itself,
in the register filling up, and in the audience learning the calendar; margin per order falls in
the register filling up and in the discount reaching people who were buying anyway. First run the
recomputation in step 3: if the peaks vanish on the unpromoted assortment, the index is false, and
every other reading built on it goes with it. Then read the promotional share of the year: rising
means the register is filling, and the fix is the budget. Share flat and the shoulders still
eroding means the audience has learned the calendar, and the budget as it stands is too high to
stop it.
