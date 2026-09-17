---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-11
---

# Vocabulary for promo-calendar

The terms all three mechanics assume. Words other skills also use, and words this skill declines
or claims, are marked at the end.

## Cycle

The planning cycle: the span one register covers, whether a calendar year or, in B2B, the
customer's budget year. It is not the purchase cycle, which is the interpurchase interval of the
category (`repeat-purchase`) and measures shoulders and gaps. "Once per cycle" and "the previous
cycle" always mean the planning cycle.

## Occasion

A reason for a dated commercial push: a period where demand rises on its own, an event outside
your business the audience already acts on, or an event of your own. An occasion exists whether
or not you act on it. Admitting one to the calendar is a decision, and it has a test.

## Window

A dated span with an offer inside it, addressed to a named audience. This is the unit of the
skill. It is larger than a send, larger than a flow entry and larger than an offer: one window
contains several of each.

## Fixed and movable window

A fixed window is tied to a date that is not yours to move. A movable one can be placed anywhere
the calendar has room. Fixed windows are laid down first, because every movable one has to fit
around them.

## Shoulder

One purchase cycle on each side of a window. The shoulder before it is where sales are lost when
the announcement teaches people to wait; the shoulder after it is the hole left by whatever the
window pulled forward. Reading a window without both counts borrowed purchases as gains. Two
windows one purchase cycle apart share a shoulder, and in those weeks the two losses cannot be
told apart.

## Extended window

The window plus both shoulders. The only span on which a window gets a verdict.

## Index of a period

Revenue or orders of one period, with the trend taken out, divided by the average period of the
same year. Computed within a year and never against last year, which would put the trend into
every figure; and on detrended figures, because a business that grows through every year
otherwise shows its late periods as a season. The indexes of one year sum to the number of periods
in it.

## Season, trend and your own calendar

Three things that look alike on a chart. A season is a stable rank of periods repeating across
years. A trend is a movement in level across the whole history; left in, it tilts every year the
same way and passes for a season. Your own calendar is an unstable rank
that happens to sit where your promotions sat: the index is then measuring what you did rather
than what the market wants.

## Amplitude band

How far the peak sits from an average period, cut on your own distribution rather than on a
published typology. The band is not a label. It says whether the year has a shape to build on;
which mechanic has work to do is decided by what constrains the peak.

## Promotional share of the year

The share of periods, and the share of revenue, allowed to go at a promotional price. Set in
advance as a budget. Left as a residual it climbs every cycle, because each window is justified
on its own and nobody owns the total.

## Issuance cutoff

The date after which you stop issuing one kind of promise, because every copy issued later would
still be live in a coming public window. Set per kind: the window's start minus that promise's
redemption window. It is the calendar's lever over promises, because `offer-design` does not
allow a promise already issued to be shortened.

## Outstanding promise

An issued promise, in `offer-design`'s term, that has not expired or been redeemed. It is a wall
in the year
with a known expiry date: the calendar has to see it before placing a window, not after.

## Window register

The list of admitted windows, one row each: occasion, start, end, audience scope, depth class,
fixed or movable. It is the output of this skill and the input of several others.

## Occasion tag

The mark put on a customer whose first order closes inside a window, naming the occasion. It is
what lets anybody reading cohorts later tell a cohort recruited in a sale from an ordinary one.

## Lead time

The median time, in your own data, from the first recorded interaction with the promoted category
to the purchase in it. The warm-up starts that far ahead of the window, which is why a considered
purchase is warmed for weeks and an impulse one for days.

## Message ladder

The four positions a window's messages occupy: announce, open, mid-window reminder, close.
Somebody who buys inside the window leaves it.

## Channel ladder

The order channels are used as the date approaches, from broad and patient far out to immediate
and intrusive at the end. An interrupting channel spends money, the person's tolerance of it, or
both, and that spend earns its price at the end of a window, where there is no time left to reach
the person any other way.

## Freeze window

The span in which nothing in the sending stack, the loyalty processing or the catalog integration
is changed. It opens before the warm-up and closes after the shoulder.

## Cap exception

Permission to exceed the standing frequency cap for a named term, with the cap returning
automatically. Requested before the window, never during it, and granted by the owner of the cap.
It runs from the first warm-up message to the close.

## Shift

A quantity of demand deliberately moved from one period to another, with a direction, an
instrument and a price. Three directions: forward, backward, and extension.

## Redemption window

`offer-design`'s term for how long an issued promise can be used, placed on the calendar with a
start later than issuance: the span in which an instrument issued during a peak may be used. It
opens after the peak's shoulder, which is the whole point. Opened inside the window, the
instrument is redeemed during the peak; opened inside the shoulder, it lands in the peak's own
verdict. Either way it was only ever a discount.

## Borrowed demand

Purchases the window took from its own shoulders. Revenue arrives earlier and at a lower price,
the window's report looks good, and the year is smaller.

## Habituation

What a base learns from a calendar it can predict. People who can predict it and are in no hurry
stop buying at full price and wait, which shows up as shoulders eroding cycle over cycle while the
windows grow.

---

## Words this skill shares with its neighbors

**Window.** Here it is a dated span with an offer in it. Elsewhere in the library the word carries
a qualifier, and the qualifier names a different object: the cohort window of `repeat-purchase` is
the span in which a cohort's second purchase counts; the attempt window of `lapse-and-winback` is
the span of a return attempt; the engagement window of `email-program` is the recency period that
classifies a subscriber; the window of the control metric in `triggered-messages` is the span in
which an entry's target action counts; `experiments-and-holdouts` defines four windows of a test. They are told
apart by what they are about rather than by how long they last. A bare "window" in this skill is
always this one.

**Redemption window.** Shared with `offer-design`, which owns it: how long an issued promise can be
used. This skill places it on the calendar and may start it later than issuance; the length is
still the neighbor's.

**Anchor.** Not used here. `email-program` calls a send tied to something immovable an anchor,
and the peak season is one of its examples. What that skill anchors on is a row of this skill's
register: the register is built first, the channel calendar is laid out around it.

**Campaign.** Here, a window in the register. `scenario-map` uses the word to mean a row on the
roster that is tied to a date and an offer and therefore is not a mechanic, and sends those rows
here. `contact-orchestration` uses it as a message class, addressed to many and repeating.

**Shoulder.** Not used by any other skill in the library, and stated here so it stays that way.
