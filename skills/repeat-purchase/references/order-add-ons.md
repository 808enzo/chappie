---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-10
---

# Add ons to an order: what may be offered alongside a purchase

The unit here is **the order**. Not the person and not the session: the selection is assembled
against the contents of one order and lives as long as that order is current. One person with two
open orders gets two different selections.

Three kinds of add on live in this file, and they are not interchangeable. A dearer alternative
replaces what is being bought. A companion item adds to it. A cheaper alternative rescues a
purchase that is being abandoned on price, and its entry condition is a refusal rather than a sale.
Its unit is the order being refused, and it has no row among the moments in step 1, because those
attach to a purchase that is going ahead.

## Entry conditions

The contents of the order are known, and so are the links between products, either from a history
of items bought together or from a rule in the catalog. The catalog carries the repeat purchase
flag, meaning whether an item is bought again or bought once (`personalization`).

## Exit conditions

Named: the moment, the source of the pairing, the exclusion lists, whether the offer is monetary,
and the rule for the refusal on price. The selection is reproducible: the same order contents
produce the same set.

## Steps

**1. Pick the moment, and pick it by one question: does the add on have to travel with the
order.** There are three moments and they do different work.

| Moment | What belongs there | The constraint |
|---|---|---|
| Before checkout, on the item | a dearer alternative | it replaces the main item rather than adding to it, so after checkout it is pointless |
| In the cart, before payment | a companion item on this same order | the last moment at which the add on ships in one delivery |
| After the order closes | a companion item as a separate order | it has its own delivery and its own free delivery threshold, and the offer has to account for that |

**2. Take the source of the pairing from what data you have, not from what is elegant.** Items
bought together yield pairs nobody thought of, but they need volume and they know nothing about a
new product. A catalog rule covers a new product from its first day and repeats what the
merchandiser already believes. Both are legitimate: the rule as the baseline and as the cold start,
the history as a refinement where the observations are there.

**3. Subtract before you show, using three lists.** Selection here is mostly subtraction. The
lists below are what keeps a selection from contradicting the order it is attached to.

- **Already owned and not consumable.** The flag comes from the catalog rather than from the
  algorithm: bought again against bought once. Without it the selection offers a second mattress to
  somebody who bought the first one yesterday.
- **Out of stock.** Checked when the selection is assembled, not when the rule was configured. How
  fresh the availability data has to be is `martech-stack`, and it is the same freshness class as
  the storefront rather than a reporting one.
- **Outside this person's constraints.** Size, age, compatibility. This is not a refinement of the
  selection but a condition on it: an add on that cannot fit reads as not knowing them.

**4. Address the dearer alternative and the companion item differently.** A dearer alternative goes
to people whose own order value already sits above the base, which is a cut you compute from your
own data. A companion item is addressed by the contents of the order and needs no audience cut at
all.

**5. Hang the cheaper alternative on a refusal over price, never on a purchase.** Its entry
condition is different in kind: somebody declined because of the price, or because they were paying
for more than they needed. Hung on a purchase it offers something cheaper to a person who has
already agreed to pay more, and it costs you the difference. The entry needs a sign that price was
the reason: the item removed after the total was shown, a direct answer, a renewal canceled with
price given as the cause. An abandoned cart on its own is not that sign, since people leave carts
for reasons that have nothing to do with price, and it belongs to the abandoned cart flow in
`triggered-messages`. A canceled renewal is the subscription case and lives in
`subscription-retention`. Without a sign, the mechanic does not run.

**6. Say whether the offer is monetary, and hold two limits on the ones that are.** A discounted bundle and free
delivery are monetary: they raise the order value and cut the margin at the same time. A selection
of companion items and a service attached to a product are not. What it costs and how deep it may
go is `offer-design`. What stays here is the flag and two limits, each binding a different case:
one monetary add on per order, and none at all on an order that already carries an offer from
another mechanic, whether that offer came from this skill's second purchase series or from anywhere
else.

## Thresholds and timings

| Quantity | Class | What sits beside it |
|---|---|---|
| Delay before the touch that follows a closed order | 4 | time to first use from your own data; for a consumable it is shorter than the interval in `references/interval-model.md` |
| The cut that receives a dearer alternative | 4 | own order value above the median of the base; recipe: take the median order value across the base for a period, then the people above it |
| Items in a selection | 5 | start with three or four; it applies to an email or a product page where the selection is not the only block, and a page built entirely around a selection is a different problem; revise it when clicks on the last position fall to noise |
| Observation threshold for a pair drawn from history | 5 | start with pairs seen together no fewer than thirty times; it applies to a catalog where items are not one of a kind; revise it by whether the pair holds between periods |

## Edge cases

- **The order already contains the add on.** Check the whole order rather than its main item. A
  case offered alongside a phone that was bought with a case is a failure the recipient sees at
  once, and one check on the full contents prevents it.
- **The selection is empty after the subtraction.** The three exclusion lists can leave nothing. The
  block is then removed whole, together with its heading and its button, rather than shown empty or
  padded with arbitrary items. The template has to hold both states (`email-design`).
- **The order was placed through a salesperson or in a store.** The add on was already offered out
  loud. Which channel the order came through is a condition: repeating the offer in writing is fine,
  pretending it never happened is not.
- **The add on is a service.** Assembly, installation, setup. Its availability is its own, by
  location and by schedule, and it is not checked against stock.
- **The add on costs more than the main item.** Formally a pair, in substance a different purchase.
  Set the ceiling on the price ratio in advance rather than discovering it in a selection.

## Failure modes

**There are no pairs.** The catalog is small or the items are one of a kind, so no history of
co purchase accumulates and there is nothing to write a rule about. The mechanic does not get
built, and filling the space with an arbitrary selection is worse than leaving it out: it teaches
people not to look at that block.

**The selection assembles but the availability data is older than the cycle.** The sign is clicks
on items you cannot sell. The mechanic stops until the freshness is fixed rather than being softened
with a disclaimer.

**The rise in order value is eaten by the discount that produced it.** The sign is order value
rising while margin per order falls. This is not the selection failing but the monetary form
failing, and it is not settled here: the economics are `offer-design`. What stays here is the
two limits in step 6.
