---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Cutting the axes: where a band boundary comes from

Every published account of this method spends its length on the twenty seven cells and one
sentence on the thing the cells depend on: "the boundaries depend on your business." That
sentence is correct and it is the whole job. Six months ago is recent for a car and old for a
face cream. Four purchases a year is frequent for furniture and rare for groceries. A boundary
copied out of an article is a boundary computed on a base you have never seen.

This mechanic covers what the axes are cut with: the direction of the scale, the two ways to
place a boundary and what each one buys you, where the recency boundary comes from, how many
bands your own distribution can carry, what money measures, and when an axis should be dropped
rather than cut.

## Entry conditions

A purchase history stitched to a person: a date, an amount, and an identifier that survives
across orders. Stitching belongs to `list-building`; where the events live and how late they
arrive belongs to `martech-stack`.

## Exit conditions

Three axes, each with a declared direction of scale, a declared number of bands and a declared
cutting method. Boundaries computed from your own distribution and written down with the date
they were computed. Any axis left out of the grid, named together with the reason. The people
with no purchase history routed out of the grid rather than sitting in its worst cell.

## Steps

**1. Confirm the history is stitched before computing anything.** An unstitched history inflates
the no purchase group and understates frequency for everybody who bought under two records. The
signal is a no purchase share larger than your acquisition numbers can account for. Fixing it is
`list-building`; noticing it is cheapest here, because this is the first mechanic that reads
every person's whole order history at once.

**2. Fix the direction of the scale and write it into the definition.** Two conventions are in
circulation and they are mirror images: in one the first value of the scale is the best, in the
other it is the worst. Pick one, put it in the group definition, and **never print a code without
its legend**. The rule costs a line and its absence costs a send: the same code in two documents
in one company can name opposite groups, and nothing in the code itself will tell you which
document you are holding.

**3. Choose a cutting method per axis: quantile, or business fact.** They answer different
questions and they are not mixed inside one axis.

- **Quantile cut.** Bands of equal size. It tells you where a person stands relative to everybody
  else, and it holds band sizes steady while the base grows. What moves is the meaning: the same
  band means something different once the distribution shifts.
- **Business fact cut.** Boundaries at named values: one purchase cycle, the free shipping
  threshold, the length of a subscription term. It holds the meaning steady and lets the band
  sizes move.

Use the business fact cut where a fact exists to stand on, and the quantile cut where there is
nothing to stand on. Write which one you used next to the boundary. A report that does not say
cannot be compared with the next report, because a change in a band could be either kind of
movement.

**4. Compute the recency boundary from your own interpurchase interval rather than from a
calendar month.** The recipe: take people with at least two purchases, take the gap between
consecutive purchases, take the median, and place the recency boundaries at multiples of it. Draw
the sample over a period long enough to contain several typical intervals, or the median
describes the last campaign rather than the base.

**5. Let your own distribution decide how many bands frequency can carry.** The number of bands
is bounded by the number of distinct values you have. A base where the largest share of
people bought exactly once cannot support three frequency bands: two of them come back empty and
the third contains everybody. Look at the distribution before choosing the number of bands, which
is the opposite of the order the published tables imply.

**6. Say what money measures and over which window.** Total spend over all time, or spend over
the same window as recency and frequency. All time money rewards tenure: somebody who spent a lot
three years ago outranks somebody spending steadily now. A shared window removes that and gives
up the tenure information. Either is defensible and an unnamed window is not, because it is the
reason two exports of one base return different groups.

**7. Drop an axis that does not separate instead of carrying it.** The test is `segmentation`'s
separation: the difference in the target metric between a band and the rest of the base, read
under the same treatment. A fixed
price catalog or a single tier subscription gives money nothing to separate, and the grid is then
recency by frequency. Carrying a dead axis multiplies the cells by the number of its bands, and
none of the extra cells behave differently from the ones they came from.

**8. Route the people with no purchase history out of the grid before you cut it, not after.**
They hold no value on any axis. A grid that admits them anyway files them in its worst cell,
where they collect that cell's route, and the route for somebody who never bought is not the
route for somebody who stopped. Their group and their two routes are in `groups-and-routes.md`,
step 5.

## Thresholds and timings

- **Number of bands per axis: start with three.** A starting point, not a property of the method.
  It applies where each axis has three distinct values worth telling apart and the resulting cells
  clear the readable floor (`segmentation`). Replace it by reading your own distribution per axis
  and counting the cells that result: three bands on three axes is twenty seven cells, and on a
  base of any size the larger part of them sits under the floor.
- **The recency boundary:** multiples of your own median interpurchase interval, computed on
  people with two or more purchases. This is a parameter of your data rather than a starting
  figure: every input to it is yours.
- **The sample period for the interval:** long enough to hold several typical intervals. Start
  with no fewer than three median intervals. That holds in a category with steady demand; in a
  seasonal one, compute the interval within a season instead, because a year long sample averages
  the season away. Replace the starting figure once you can see how stable your own interval is
  across periods.
- **Re-cutting the boundaries themselves:** on the program revision cycle
  (`crm-program-design`), not on the recompute cadence of the groups. Moving the boundary and the
  people in the same cycle leaves neither readable.

## Edge cases

- **The largest part of the base bought exactly once.** This is the ordinary shape of a base
  rather than a defect. Cut frequency at one and more than one, and put the work into recency,
  which is the axis that still moves for those people.
- **A seasonal category.** A median interval computed across a whole year labels everybody lapsed
  in the off season. Compute the interval within the season, or cut recency against the season
  instead of against days.
- **The purchase cycle is longer than the recompute cadence.** Groups barely move, and the grid
  reports what you already knew. Either the cadence stretches (`recompute-and-transitions.md`) or
  the axis is replaced by one that moves at the speed you can read.
- **One very large purchase.** Money puts the person in the top band and frequency in the bottom.
  The grid is right and the action is not obvious. Name that cell and decide once, rather than
  rediscovering it every cycle.
- **Refunds and cancellations.** Whether a refunded order counts toward frequency and money is
  decided here and written into the definition. The formula for the metric itself belongs to
  `metric-definitions`; what belongs here is that the choice gets made rather than inherited from
  whatever the export happened to do.
- **The company pays and a person reads.** Cut the grid on the account and choose the recipient
  separately (`b2b-lifecycle`). A grid cut on individuals in a business base scores the person who
  happens to submit the orders.
- **Two brands or two catalogs in one base.** Interpurchase intervals differ, so the boundaries
  differ. Cut each one on its own distribution and say which grid a report came from.

## Failure modes

- **The bands came out of an article.** The signal is round numbers, identical across categories
  that have nothing else in common. It is caught by comparing the boundary against your own
  distribution rather than by arguing about it.
- **A code was printed without its legend.** The signal is two documents in one company using one
  code for opposite groups. It surfaces after somebody has sent on it, which is why the legend
  travels with the code rather than living in a separate glossary.
- **The grid was cut on an unstitched history.** The signal is a no purchase group larger than
  acquisition explains. Everything downstream is then computed on people who did buy, filed as
  people who did not.
- **A dead axis is carried anyway.** The signal is cells that differ only in that axis and
  respond identically. The cost is not the axis, it is the cells: they get named, they get owners,
  and they produce work.
- **The window on money was never named.** The signal is two exports of the same base returning
  different groups and both being defended.
