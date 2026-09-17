---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-08
---

# Vocabulary for personalization

The terms all three mechanics assume. Four of them are shared with neighboring skills under
different meanings, and those are marked at the end.

## Place

One spot in one message or on one page whose content differs from one person to the next. The unit
of `substitution-and-empty-values.md`. A message holds several, and they fail one at a time.

## Placement

A spot that returns a list rather than a single value. The unit of `recommendation-blocks.md`. It
fails in three ways where a place fails in one: empty, short, or identical for everybody.

## Source class

Where a value comes from: a profile field, an event property, a catalog lookup, or a computed
value. The class sets both the moment of resolution and the failure mode.

## Moment of resolution

When a place gets its content: assembly, trigger, send, or render. A property of the place,
declared in advance.

## Frozen value

A value that describes an event and is taken at the event. It is not re-read later, because the
subject of the message is the fact rather than the current state. The cart in an abandoned cart
message is frozen; the price in a price drop message is not.

## Fill rate on the receiving population

The share of the people who will receive this message for whom the source holds a value. The
quantity is `segmentation`'s and is not redefined here. What changes is the population: the base
and the people who arrived yesterday give different answers, and the second is the one that decides
whether the personal version or the fallback is the main version.

## Fallback ladder

Three levels, taken in order: a neutral value that keeps the sentence true, a rewritten version of
the block without the place, and removal of the block together with everything that referred to it.
The level is chosen in this skill; the words belong to whoever writes the message.

## Message class

**Core**: the personal value is what the message is about, and without it the message does not go.
**Addition**: personalization supplements the message, and without it the message goes with the
fallback. Declared before launch, because at send time nobody is there to decide. Call it core
rather than subject: the subject line is a place like any other, and the two words would collide.

## Resolved share

Evaluations of a place closed by the source assigned to it, divided by every evaluation of that
place. An evaluation is every time your system asks the place for content, including the times it
returned a fallback, a short block or nothing at all, and the times you held the message back. The
control metric of this skill. Counted on evaluations rather than on people, which separates it from
fill rate, and rather than on impressions, because a suppressed block and a held message leave
none.

## Anchor

The object a selection is computed against: the person, their last action or session, an item, a
category, or the storefront.

## Anchor ladder

The declared order of descent between anchors. Where the anchor does not resolve, the block takes
the next one down. The ladder is what makes cold start an ordinary case: an empty profile is an
unavailable anchor, not a failed algorithm. The descent stops at a floor set by the job of the
placement: below it you shorten or suppress the block rather than fill it, because a block that
descends far enough always builds and stops doing the job you put it there for.

## Algorithm class

What a selection is computed on: co-occurrence across orders, similarity by item attributes,
behavior of this person and similar people, or popularity within a scope. The anchor decides which
classes are available.

## Constraint list

What is barred from output regardless of the algorithm: items out of stock, items already bought
that are not bought again, sensitive categories, items outside the price band, and anything failing
a strict attribute match.

## Short fill

The state where fewer items qualify than the block has slots. Handled by a rule declared in
advance: top up from the anchor below, show a shorter block, or suppress it. Which of the three you
declared decides whether a tightening constraint list shows up in the resolved share or hides from
it, so read the rule before you read the number.

## Output spread

The count of distinct items a block emitted over a period, counted at the level its anchor resolves
to: across the audience for a block anchored on the person, per anchor value for one anchored on an
item or a category. The signal that a personal block is still personal. It catches the case the
resolved share can miss, where the anchor still resolves for everybody and the algorithm hands them
all the same short list. Where the anchor stopped resolving instead, the number that moves is the
resolved share.

## Register of live rules

The list of personalization rules currently running, with the source or anchor, the moment of
resolution, the format contract, the fallback, the check case, an owner, a launch date and a date
of last check. The unit of `live-rules-and-switch-off.md`.

## Inferred attribute

A value derived from behavior rather than supplied by the person. Use it to choose content and keep
it out of the copy as a statement about the person, because an inference can be wrong and a wrong
statement about somebody reads as a mistake about them rather than about the data.

## Terms shared with neighbors

**Fill rate** is `segmentation`'s: the share of the base holding a value for an attribute, measured
independently of any segment built on it. This skill takes that quantity and applies it to the
receiving population of a specific message. The number that belongs to this skill is the **resolved
share**, which counts evaluations of a place rather than people and fails for different reasons.
Both sides carry this split in their vocabularies.

**Freshness class** is `martech-stack`'s: a property of a source and its transport, written down
twice, as the class the decision needs and the class the transport delivers. The **moment of
resolution** is a decision about a place, capped from above by that class. They are not synonyms
and one does not imply the other.

**Display rule** is `onsite-capture`'s on the site and `in-product-messaging`'s inside an app or a
signed-in account area: whether a block shows, in what order, and how many windows one page or one
screen may open. This skill supplies what the block holds and never decides when it appears.

**Personal offer** in `offer-design` is the construction of a promise: depth, threshold, expiry.
Here it is a value with a source and a moment of resolution. The economics belong to the neighbor,
the place belongs here.
