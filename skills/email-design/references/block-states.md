---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Block states at assembly

The unit here is **one block for one recipient in one send**. The decision belongs to a rule declared
before launch, and at the level of a whole send, to the send's owner. This file answers what a block
shows when there is nothing, or too little, to put in it.

`personalization` decides where the content comes from and which fallback level applies, `email-copy`
writes the words of a fallback, and `template-system.md` holds the block's layout and contract.

## Entry conditions

The template has at least one block whose content is decided at assembly: a substitution, a selection,
a catalog, stock levels, a feed.

## Exit conditions

Every such block has a minimum, four states with their layouts, and a do-not-send outcome where the
block carries the message's job. An assembly log is kept. The send's owner has written a send-level
line. A peak window has a declared stand-in.

## Steps

**1. List the blocks decided at assembly**, per template: the source, the moment of resolution (which
`personalization` sets), the declared size and the minimum (`template-system.md`, step 3).

**2. Lay out four states.**

- **Full:** the declared number of items.
- **Short:** between the minimum and the declared number, in a layout with no empty cells. Three to a
  row becomes two or one, and the see-all link stays.
- **Stand-in:** below the minimum, where a stand-in block is declared: a block with a contract and
  a job of its own, such as an editorial block or the window's offer block in the place of a personal
  selection, not the empty frame of the original. A selection recomputed against a lower anchor is
  not a stand-in; that is `personalization`'s anchor ladder at work inside the same block, and it
  comes out here as full or short.
- **Removed:** below the minimum with no stand-in. The heading, the image, the button and any links to
  the block from other blocks leave with it, the spacing collapses, and no divider is left hanging.

**3. Map the states onto `personalization`'s two rules.** For a substituted value, the fallback
ladder: a neutral value is the full state carrying fallback words, which `email-copy` writes; a
rewritten version of the block is the stand-in; removal is the removed state. For a selection, the
anchor ladder and the short fill rule: a descent to a lower anchor, topped up or whole, comes out full
or short; the neighbor's "show a shorter block" is the short state, and **the minimum is the number
that option was missing**, because below it no layout of the block holds and the block goes to
stand-in or removed; "suppress" is the removed state. Which option the neighbor declared is the
neighbor's. The layout of each outcome, and the minimum, are here.

**4. A message without its job does not go.** Where a block carries the job of the message, the class
`personalization` calls core, such as an abandoned cart or an order status, its removal turns the
message into a do-not-send outcome rather than into an empty message, and the template has to be able to return
that outcome. Count the held messages: without them the share of full states reads 100% by
construction. A message left with no block that carries a job does not go either, even when every
block in it was optional on its own.

**5. Drop an item that is missing a required field before counting.** An item in a selection without
the price, the image or the name, where those are part of what the block promises, is not shown and
does not count toward the minimum.

**6. Keep an assembly log.** For every send and every block: how many recipients got each state, and
how many messages were held. A preview shows one message; the log records the state every recipient
got.

**7. Write the send-level line before launch.** The send's owner, `email-program` for a campaign or the
flow's owner for a triggered message, writes down the share of full states below which the send comes
back to them before release. Compute the line from the log of that block's past sends, measured
against its own history. The template counts; the owner decides. Deciding it before launch means
nobody has to decide it in the middle of the night.

A triggered flow has no send and no release. Read the line on the assembly log of a period, the same
period the index uses, and treat a breach as a decision going forward rather than a send returned:
fix the source, switch to the stand-in, or leave it. Messages whose missing block carried the job
were already held by step 4. A block with no history has no line yet: the owner reads its first sends
by hand and writes the line from them.

**8. Test the states before launch** with profiles that force each one: full, short at the minimum,
stand-in, removed, and held. The four named profiles in `personalization` test values; these test the
layout.

**9. In a peak window, decide the stand-in in advance.** Inside a window, stock sells through faster
than usual, and a selection shrinks between sends and inside a single send that takes hours to go out.

- Resolve availability at the latest moment your platform allows; the moment of resolution is
  `personalization`'s.
- **Declare the window's stand-in block before the window opens.** It lives in the template as a
  state.
- **For each recipient, the decision is always the declared minimum**, never a person.
- **Switching to the window's stand-in is the decision of the owner of the window's sends** (step
  7), taken before a position of the window's message ladder in `promo-calendar`, the opening, the
  reminder or the close, and read from the assembly log of the previous position, never on the fly.
  The stand-in holds until the window closes, on its date or early, or until the owner switches back
  before a later position.
- **The switch is a state of the template**, so every send and every flow assembling on that template
  switches together; a flow that has to keep its own block runs on its own template. You declare the
  stand-in before the window's freeze opens, so switching it on is not one of the changes the freeze
  forbids.
- A window nobody can serve closes early and says so. That decision is `promo-calendar`'s, and swapping
  a block does not replace it.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Minimum of a block | the block's layout (`template-system.md`, step 3) |
| Send-level line | the assembly log of the same block's past sends |
| Moments to switch the window's stand-in | the positions of the window's message ladder in `promo-calendar` |

## Edge cases

- **Stock changes during a long send.** Early and late recipients get different states. The log shows
  it and the preview does not.
- **Items with images of different proportions** break the alignment of a short block, so the image
  proportion is part of the block's contract.
- **A price or availability that was true at assembly and false at reading.** The item links to a live
  page, and a price claim follows the rule for claims tied to time in `email-copy`.
- **An interactive part that fetches content at open.** Its state at reading can differ from the state
  of the fallback part at the send, so declare both.
- **The text part** gets the same state as the HTML, because both come out of one assembly.
- **Two blocks removed at once.** See step 4: check the message as a whole, not the blocks one at a
  time.

## Failure mode

**The signal:** quiet removal. Sends go out, the report looks ordinary, and the block was removed for
recipients nobody counted. The share of full states in the log falls below its own history, and the
click rate falls equally in every environment while the environment click index stays flat, because
removal does not depend on the environment.

**What to do:** read the log before the index. The send-level line in step 7 should have returned the
send to its owner; if it did not, the line was never written or sits too low. The same signal has
three other causes, one of them this skill's; the order to read them in is in `SKILL.md`.

**The second signal, which behaves the opposite way:** the personal block almost never shows. The
minimum is set too high, or the stand-in fires too early. The share of stand-in and removed states
grows while the resolved share in `personalization` stays healthy. **The question that separates the
two:** does the source hold values for these recipients? If it does, the minimum or the layout is
wrong, and the fix is here. If it does not, the source is the problem, and that is `personalization`.
