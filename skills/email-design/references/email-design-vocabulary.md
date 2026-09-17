---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# Vocabulary for email design

The terms the three mechanics assume. The last section lists eleven words this skill shares with its
neighbors. Provider and window keep the neighbor's meaning, version keeps it and adds the release
gate, and the other eight do not.

## The template

**Template.** The frame and the block library, released together as a version.

**Frame.** The locked part of a template: identification of the sender, the required elements, a
visible unsubscribe link, a link to the preference center, and a link to the web version. No send
edits it.

**Required elements.** What your regime and the mailbox providers require in every message. Which
elements those are belongs to neighbors; where they sit is the frame.

**Block.** A unit of the template's library that has a contract.

**Block contract.** What a block carries, where its content comes from, its declared size, its
minimum, its states, and what leaves with it when it is removed.

**Minimum.** The smallest number of items at which no layout of the block leaves an empty cell.

**Block state.** One of four: full, short, stand-in, removed. The message itself has a fifth
outcome: held.

**Stand-in.** A block with a contract and a job of its own, declared for the place of a block that
fell below its minimum. A selection recomputed against a lower anchor is not one: that is
`personalization`'s anchor ladder at work inside the original block.

**Template version.** A record of a change to a template (what, when, who, why) together with the
released state whose identifier is stamped on every send.

**Release.** The decision that a version goes into sends, taken after the check in real environments.

## Base and layers

**Base layer.** Everything every environment shows: live text, background colors, a simple layout. It
carries the job.

**Layer.** Anything some environments do not show: dark scheme tuning, a web font, a background image,
animation, an interactive part, video. Each one has a fallback.

**Deletion test.** Remove the layer; the message still does its job. If it does not, the element was
never a layer.

**Live text.** Text the client renders as text, not as pixels inside an image.

## Environments

**Environment.** A mail client family and device class inside one provider, as your platform reports
them.

**Condition.** A state of an environment in which you check a version: images off, dark scheme,
narrowest width, clipped, animation off, fallback part shown.

**Environment matrix.** The environments from your own base, in order of accepted share, with their
conditions.

**Unchecked share.** The share of accepted recipients in environments below the last one you checked.
Written down.

**Seed mailbox.** A real mailbox in one environment, used for a live check.

**Emulated preview.** A tool's drawing of a client from its own model. A prediction, not an
observation.

**Clip point.** Where a client cuts a long message. Found with a seed send.

**Size budget.** The assembled size at which the job, the action and the required elements all sit
above the earliest clip point in your environments.

**First screen.** The area visible before scrolling in a given environment, measured at its narrowest
width.

**Fallback part.** The part of a message a client shows when it does not show the richer one: the text
part under HTML, or the HTML or text part under an interactive one.

## Assembly

**Assembly log.** The count of states per block, and of held messages, per send.

**Window stand-in.** A stand-in block declared before a peak window opens and switched on by the
owner of the window's sends before a position of the window's message ladder.

## The metric

**Environment click index.** The control metric: the click rate among accepted recipients in one
environment inside one provider, divided by the same rate across all of that provider's accepted
recipients with a known environment, in the same send. Required links, the frame's web version link
among them, are outside the numerator. The environment is set from clicks before the send and never
cleared.

**Row.** One pair of provider and environment, as the control metric reads it.

## Eleven words this skill shares with neighbors

| Word | Here | At the neighbor |
|---|---|---|
| first screen | the area before scrolling in an environment | `email-copy`: a requirement about the order of meaning |
| fallback | always qualified: the fallback part of a message, or the fallback of a layer | `personalization`: the fallback ladder for an empty value; `email-copy`: fallback wording |
| block | a template unit with a contract and states | `personalization`: the same object as a place a value is substituted into; `email-copy`: one block, one thought, a unit of argument |
| version | a template version with a release gate | `program-audit-and-ops`: the record of a change to an object; the release gate is added here |
| template | the frame and the block library | `personalization`: a template token is an unresolved substitution; `messaging-channels`: a message format a platform has approved |
| preview | an emulated drawing of a client | `personalization`: the platform preview with demo values |
| seed | a seed mailbox in an environment | `personalization`: four named profiles that test values; `deliverability`: the seed lists behind published placement figures, measured on a population that is not yours |
| index | the environment click index, inside a provider | `deliverability`: the provider response index, against the whole send; `email-copy`: an index message is a digest |
| window | always qualified: a peak window, in `promo-calendar`'s sense, or the click collection window, in `metric-definitions`' sense | `promo-calendar`: a dated span with an offer in it |
| provider | not redefined | `deliverability`: the receiving side, read from the MX record |
| layer | a layer above the base | `triggered-messages`: the automated layer of a program |
