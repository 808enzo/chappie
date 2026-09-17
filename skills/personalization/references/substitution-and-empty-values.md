---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-08
---

# Substitution: the source, the moment, and the empty value

The unit here is a **place**: one spot in one message or on one page whose content differs from
one person to the next. A message holds several of them, and they fail one at a time. This
mechanic takes a place from "we substitute the name here" to a specification you can build, check
and read afterwards.

## Entry conditions

A neighbor has decided what the message is for and what it promises: `email-copy` for the wording,
`triggered-messages` for the flow, `welcome-and-activation` for the series, `offer-design` for the
promise, `onsite-capture` for the spot on the page. Profile fields and events exist, each with a
named owner and a freshness class (`martech-stack`). The fill rate of the attribute across the base
has been measured (`segmentation`).

## Exit conditions

Five things written down per place: the source, the moment of resolution, the format, the fallback,
and a check case. One thing written down for the message as a whole: what happens when the personal
part cannot be built at all.

## Steps

**1. List the places and name a source class for each.** Four classes, and the class sets both the
moment of resolution and the failure mode:

- **profile field**, stored on the person: name, city, size, preferred category;
- **event property**, fixed at the moment the event happened: cart contents, the item viewed, the
  order total;
- **catalog lookup**, resolved from an item id: price, availability, image;
- **computed value**, which the program works out itself: a points balance, an expiry date, a
  discount depth handed over by `offer-design`.

The class is not decoration. An empty profile field looks like a blank string; a missing event
looks like nothing to send about; a catalog lookup fails as an item that no longer exists; a
computed value fails as a zero or a negative you must not show.

**2. Declare the moment of resolution.** Four moments: **assembly**, when the campaign is built;
**trigger**, when the event fired; **send**, when the message is handed to the channel; **render**,
when the person opens the message or the page paints.

The rule runs in two directions, and each direction breaks in its own way.

- **A place resolves as late as its transport allows, and no later than the freshness class its
  source delivers** (`martech-stack` writes both classes down: the one the decision needs
  and the one the transport delivers). A place that claims to resolve at render while feeding on a
  nightly export shows yesterday's state and reports success.
- **A value that describes an event is frozen at the event and never re-read later.** The cart
  contents in an abandoned cart message are the subject of the message, not the current state of
  the cart. Re-read at send, they produce a message about an empty cart, because by then the person
  has either paid or cleared it.

What separates the two is the question "what is the subject here": a current state, or a fixed
fact. Answer it once per place and write the answer next to the source.

**3. Measure fill rate on the population that will receive this message.** Fill rate is
`segmentation`'s quantity and the floor it sets carries over unchanged. The population does not:
a field can be well populated across the base and close to empty among the people who arrived
yesterday through a form that never asked for it.

That decides the order of work. **Where the fill rate sits below your floor, design the place from
the fallback.** Write the version that covers the larger part of the receiving population first,
and attach the personal version to it. The other order builds the message around the case that
fails, and it reads as broken for everybody the fallback has to carry.

The people who arrived most recently are the emptiest: no history, and nothing yet in the fields
that fill up over time. The welcome series is where you test empty value behavior first
(`welcome-and-activation`).

**4. Write a format contract for every source field.** Capitalization, number form, length, date
format, unit. One rule holds all of it: **normalization belongs to the source, not to the
template.** One field, one canonical form, applied where the field is written (`list-building`
owns the record). A template that fixes capitalization at render hides a data defect and repairs it
in that message and nowhere else.

**5. Give every place a fallback, chosen from three levels in order.**

1. **A neutral value** that keeps the sentence true: the sentence loses the city and names the
   general address instead.
2. **A rewritten sentence without the place**, which is a second version of the block with no
   personal value in it at all.
3. **The block comes out whole**, together with the heading, the image and the button that
   referred to it.

Three outcomes are never acceptable: an empty string inside a finished sentence, a template token
that leaked into the body, and a substitution that states something untrue, such as naming a
favorite category that was never computed.

**The level is chosen here and the words are written by whoever writes the message**
(`email-copy`). The acceptance test for a fallback has two parts: the sentence is still true, and
the message still does its job. Where dropping the place costs the message its job, the level is
wrong and the decision moves to step 6.

**6. Decide, for the message as a whole, what happens when the personal part cannot be built.**
Two classes, declared before launch:

- **core, where the personal value is what the message is about**: an abandoned cart, an order
  status, a points balance, an expiring code. No value, no message. It is not replaced by a generic
  one, because a generic message in that slot answers a question the person did not ask. Count the
  messages you hold: they are the only trace this class leaves, and without them the resolved share
  for the place reads 100% forever (see the control metric in `SKILL.md`);
- **addition, where personalization supplements the message**: a campaign carrying a recommendation
  block, a letter that greets by name. No value, and the message goes with the fallback.

Decide it in advance, because at send time there is nobody there to decide it.

**7. Check on named profiles before launch.** Four at minimum: a full profile, an empty one, an
awkward one (a long name, an apostrophe, a script the template was not built for, a value at the
edge of the format), and one live person from the real audience. Look at what the person will see
rather than at the platform preview: previews substitute demo values and hide exactly the class of
defect the check exists for.

**8. After launch, read the resolved share per place** (see the control metric in `SKILL.md`).
Set the alarm on movement against that place's own baseline rather than on an absolute value. Until
that baseline exists, the fill rate you measured in step 3 is what the share should come out at.

## Thresholds and timings

This mechanic introduces no absolute value of its own. Everything that looks like a threshold is a
parameter you compute:

| Value | What sets it |
|---|---|
| Fill rate floor for a source | the floor `segmentation` already sets, applied to the receiving population |
| Moment of resolution | no later than the freshness class the source's transport delivers |
| Alarm on resolved share | movement against that place's own baseline |

**The seed set of four profiles is a starting point, not a property of anything.** It works where a
field holds one or two shapes of value. It does not work for open text such as an address or a
company name, where the number of shapes grows with the number of ways people write them. Replace
it with your own list the first time a defect arrives from a shape the set did not hold.

## Edge cases

- **The value was true at resolution and false by the time it is read.** Price, availability, a
  points balance. A place resolved before render and read afterwards either carries the moment it
  was true, or is not used: a promise the person cannot act on when they follow the link costs more
  than an empty spot.
- **Grammar.** The sentence has to work for every value the field can hold: gender, number, case,
  and a list of one where the copy says "these items". Check on the most awkward value the field
  can produce rather than on a typical one.
- **An inferred value against a supplied one.** Name a value the person gave you in the copy. Use a
  value derived from behavior to **choose** the content, and keep it out of the sentence: an
  inference can be wrong, and being told something wrong about yourself reads as a mistake about
  you rather than about the data.
- **The value came from a session and nobody is identified yet.** An attribute belongs to a person,
  a session belongs to a browser. A value taken from an anonymous session lives until that session
  ends and does not enter the profile until identity is stitched (`list-building`). A message sent
  later uses the event property instead of the session.
- **Consent withdrawn or the attribute deleted between resolution and send.** The place loses its
  source, so treat it as empty. Where the value was what the message is about, hold the message.
- **A place in the subject line.** The subject resolves at send and gets no second chance, so write
  its fallback and check it separately from the body.

## Failure mode

**The personalization service or the catalog is unavailable at render.** Declared behavior: the
place ships its fallback, an addition class message goes, a core class message waits. Declare
that before launch, so nobody on duty has to decide it that night.

**A template ships with an unresolved token.** The mandatory run across the four seed profiles
catches it before release. No run, no release.

**Quiet success is the main failure mode of this mechanic.** Every place ships its fallback,
nothing crashes, delivery is green and the campaign report looks ordinary. The resolved share shows
it, and only when you read it place by place.
