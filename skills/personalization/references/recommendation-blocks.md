---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# What fills a block: the anchor before the algorithm

The unit here is a **placement**: one block on one page or in one message that returns a list. A
list fails in three ways where a single value fails in one. It comes back empty, it comes back
shorter than the block, and it comes back identical for everybody.

## Entry conditions

The placement exists and the rule for showing it has been settled by a neighbor:
`onsite-capture` for a page, `email-program` and `triggered-messages` for a message. The catalog is
reachable and the item fields the selection runs on are populated.

## Exit conditions

Written down per placement: the job of the placement, the anchor, the algorithm class, the
constraint list, the block size, the short fill rule, and the recompute cadence.

## Steps

**1. Name the job of the placement.** Three jobs, and they do not mix. **Choose among**: the
person has an anchor item and is deciding between options. **Add to**: the person has committed and
can extend the purchase. **Discover**: no anchor exists at all. The job comes from the page or the
message, not from the list of algorithms the platform offers.

**2. Name the anchor, the object the block is computed against.** Five levels, top to bottom: the
person, their last action or session, the item on the page, the category, the storefront.

**Choosing a block is choosing an anchor before it is choosing an algorithm.** That is what makes
cold start an ordinary case instead of an exception. An empty profile is an anchor that does not
resolve, and somebody with no history starts lower on the ladder. Declare the descent in advance
and apply it the same way for everybody: where the anchor does not resolve, take the next one down.

**The descent has a floor, and the job from step 1 sets it.** "Choose among" and "add to" both need
an item to work from, so their floor is the item: below it the block still fills, but it has
stopped doing the job you put it there for. "Discover" has no floor, and the storefront is a
legitimate place for it to land. Below the floor the block does not descend quietly. It goes to the
short fill rule in step 5, which shows a shorter block or suppresses it, and where it sits below
the floor for most people you rename the placement for what it has become
(`live-rules-and-switch-off.md`, step 4). Without a floor the ladder ends at the storefront every
time, the storefront means popularity, and popularity shows the same thing to everybody: the ladder
itself would produce the failure the last section of this file warns about.

**3. Take the algorithm class the anchor supports.** Four classes, separated by what they are
computed on:

| Class | Computed on | Needs | Where it breaks |
|---|---|---|---|
| Co-occurrence | all orders, item pairs | order history across the catalog | a new item has nothing to co-occur with |
| Attribute similarity | item fields | populated fields | a thin catalog or empty fields |
| Behavioral | this person's actions and those of similar people | history on the person | an empty profile and a new item |
| Popularity in a scope | everybody's actions over a period | nothing about the person | shows the same thing to everybody |

The anchor picks the class, not preference: behavioral needs a person, co-occurrence needs an item,
popularity needs only a scope.

**4. Write the constraint list before you look at any output.** Availability. A price band relative
to the anchor. Exclusions: what the person already bought where the item is not bought again, what
is already in the cart, restricted categories, and cheap consumables that win on co-occurrence and
crowd out everything else. Strict attributes, where a match is mandatory and a mismatch keeps the
item out even when every other field agrees.

**Whether an item is bought again is a catalog field, not a guess the algorithm makes.** Until that
field exists, the block will recommend a second mattress to somebody who bought the first one
yesterday.

**5. Set the block size and the short fill rule.** How many slots, and what happens when fewer
items qualify than there are slots. Three options, one of them declared in advance: top up from the
next anchor down, show a shorter block, suppress the block. A shorter block goes down to the
layout's minimum, which `email-design` sets; below it the rule falls to the next option. Nothing else
qualifies: filling the remaining slots with whatever passes turns the block into a storefront and
empties the control metric of meaning.

**6. Decide where a hand written rule beats a computed one.** An expert mapping between categories,
where a snowboard brings gloves, a helmet and goggles, wins where the pairing is stable and the
categories are few. Its price is maintenance: the mapping has to be redone at every catalog change,
and an abandoned mapping degrades output more quietly than a broken algorithm does.

**7. Declare the recompute cadence per block.** Popularity is computed over a window, and the window
is a parameter: keep it short where the assortment turns over fast. A personal selection recomputes
on a cycle. A block anchored on an event splits in two: the anchor is an event property and is
frozen at the event, while the selection computed from it runs live. Resolve the anchor live as
well and a cart block reads the cart as it stands now, which for an abandoned cart is empty
(`substitution-and-empty-values.md`, step 2).

The rule from the first mechanic, restated in block terms: **a block cannot answer an action that
is fresher than its own recompute.** A selection rebuilt overnight, placed in a message triggered by
a browse five minutes ago, shows what the person cared about yesterday.

**8. Read the block against a fixed alternative.** A personal block is compared with a
non-personalized one in the same placement. The design of that comparison belongs to
`experiments-and-holdouts`, along with the trap it names: the block and the algorithm are two
changes, and separating them takes a third arm with a random selection.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Block size | the placement: how many cards are read without scrolling |
| Popularity window | how fast the assortment turns over |
| Recompute cadence | no slower than the anchor changes, no faster than the transport delivers |
| Price band around the anchor | your own price distribution in the category |

## Edge cases

- **A category holding one item.** Nothing similar exists, so a "choose among" block never builds
  there. That is a property of the catalog rather than a fault: either the placement changes its
  job to "add to", or it comes out.
- **The item sells out between the recompute and the render.** Check availability at render, not at
  computation. A block built overnight holds items nobody can buy by morning.
- **The anchor came from somebody else's session.** A shared device, a gift, a one off purchase for
  another person. No algorithm fixes this. What fixes it is giving the person a way to see what the
  selection is based on and to drop the anchor, and that belongs to the product rather than to the
  campaign.
- **Recommending what the person already bought.** Settled by the catalog field from step 4 rather
  than by a time threshold.
- **Age restricted and sensitive categories.** They enter no anchor and no output. The list is
  maintained by hand and checked separately from the algorithm (see the legal section of
  `SKILL.md`).

## Failure mode

**The block came back shorter than the placement.** Step 5 fixed that behavior, so nobody decides
it in the moment.

**Everybody sees the same block.** This has two causes, they are caught by different numbers, and
which number moves depends on what step 5 declared.

Where the anchor stopped resolving and everybody dropped down the ladder, the resolved share falls,
because those evaluations were not closed by the source the placement was designed on.

Where the anchor still resolves and the algorithm hands everybody near enough the same list, the
resolved share may not move at all. Two things produce that and they behave differently. A model
collapsed onto the catalog's bestsellers fills every slot from the assigned source, so the resolved
share holds and shows nothing. A constraint list that leaves few items standing produces short fill
instead, and there step 5 decides the answer: where you declared top up from the anchor below,
those evaluations leave the numerator and the resolved share does fall, and where you declared a
shorter block, the resolved share holds and hides the same problem. Read the short fill rule before
you read the number.

What catches the collapse is a count of distinct items the block emitted over a period, **read at
the level the anchor resolves to**. Counted across the whole audience it works only for a block
anchored on the person. Count a block anchored on an item or a category per anchor value, alongside
the overlap between two different anchors: fifty categories each returning the same eight
bestsellers look healthy in a whole audience count and are not personal at all.

**The catalog is unreachable or the fields are empty.** The block drops to the next anchor down,
and no further than its floor. Where nothing builds at or above the floor, suppress it together
with its heading.
