---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# The body and the action: what is claimed and what is asked

The unit here is **a claim and an action**: the thing that can be checked for truth, and the thing
that can be clicked. This file is where most of the writing happens, and it holds the claim discipline
that replaces every list of words in circulation.

The template, the blocks and the rendering are `email-design`. Where a personal value comes from is
`personalization`. The economics of the offer are `offer-design`.

## Entry conditions

The brief is written, the facts are collected, and the inheritance is on paper
(`message-brief.md`).

## Exit conditions

A draft where the first block carries the whole job, every claim has a fact under it, there is one
action, and both the job and the action survive with images off and the message clipped.

## Steps

**1. The first block carries the whole job.** Somebody who reads only that block knows what is
offered and what to do. Everything below it is argument for the people who needed more.

**2. The order of the argument is offer, then reason, then action.** A reader who has not yet seen
why skips a call to action they meet first. The exception is named and narrow: an audience that
already knows the offer, such as a reminder, a last day, or the continuation of something started.
There the action comes first, because the argument was made by the earlier messages.

**3. One block, one thought.** The check is deletion. Take the block out. If the job of the message
is unharmed, the block was filler rather than argument.

**4. Every claim carries a fact, or the claim is cut.** The practical test is substitution: replace
the evaluation with what stands behind it. Fast delivery becomes the number of days. High quality
becomes a specification or a guarantee. Best offer becomes what it is being compared with. Where no
substitution exists, the sentence comes out. It does not get softened, and it does not get
rewritten more carefully.

This is the rule that replaces both lists people ask for, the banned words and the magic ones. A
word does no damage on its own. A sentence that asserts something nobody can point at does damage
whichever words it uses.

**5. The sentence stays true for any value a substitution can take.** Where the value comes from,
and what the level of fallback is, belong to `personalization`: a neutral value, a second version
of the block, or dropping the block with everything that referred to it. The words are written
here, and they are written **next to the original sentence rather than during the incident**.
Acceptance has two parts: the sentence is still true, and the message still does its job. Check
what the value can be: a plural, a different grammatical form, a list with one item in it, something
very long.

**6. One action. Many exits are allowed when they are the same exit.** An index message, meaning a
digest, a product roundup or a list of articles, carries a dozen links and all of them are one
action: choose and go. A second button becomes a second job not by being second but by being
different. Buy and follow us on social media in one message is two messages glued together.

**7. The words of the action name a verb and an outcome**, meaning what happens after the click
rather than what the reader is supposed to feel. Read the action on its own: somebody who sees only
the button should know where it leads.

**8. The message survives images being off and being clipped.** Meaning and action live in text. A
job named only on a banner disappears for a share of readers along with the images. Mail clients
also clip long messages; no provider publishes the threshold at which they do, so no number is
shipped here. The check replaces it: send yourself the message in the two or three clients most
common in your base and look at where it stops. Everything carrying the job and the action sits
above that point.

**9. A claim tied to time carries its own basis.** A price, a remaining quantity and a deadline are
read when the person opens the message, not when you sent it. Either the claim carries its
condition, such as the price being the one in force on the day of the send, or the figure does not
appear in the message at all and is replaced by a link to the page where it is live. A gap between
message and page reads as dishonesty even when it was caused by honest aging.

One figure takes neither route. A value quoted to one person as their final figure is the promise
itself, so `offer-design` has you compute it at the send and hold it at checkout. A condition
attached to that figure contradicts it, and the claim rules in `SKILL.md` say a disclaimer that
contradicts the main claim rescues nothing. Where you cannot hold the figure, do not quote it.

**10. The footer offers another way out and does not compete with the action.** Its links are
navigation and required roles (`message-brief.md`, step 6). Keeping the two apart is not tidiness:
the control metric counts the navigation links in the footer and leaves the required ones out, so a
footer whose roles are merged cannot be read at all.

## Thresholds and timings

- **The first block is the whole job.** Everything below it has to be argument rather than addition.
- **A claim without a fact is cut**, not softened and not rewritten.
- **One action**, with the index message as the single exception.
- **Fallback words are written with the original**, never during the incident.
- **The images-off check runs before the send**, every time the template changes. `email-design`
  owns the template; what is checked here is whether the meaning survives it.

## Edge cases

- **A two-sentence message.** The rules collapse to two: the subject matches the content, and the
  action is named. Short messages do not need argument, they need a reason to exist.
- **A message that is almost entirely product cards.** The copy is the frame, meaning why this
  selection and why now, plus the labels on the cards. The frame has to be true of the whole
  selection: calling it new arrivals with two items from last year breaks the frame, not the cards.
- **The action is not a click**, such as replying, coming in, or saving a date. Name the way to do
  it, and move the measurement to a substitute or record that it is unmeasured
  (`message-brief.md`, step 4).
- **A draft written by a model.** Fluent text hides missing facts better than a human draft does,
  because nothing about it reads as unfinished. Run step 4 sentence by sentence rather than
  sampling.
- **A tone unlike your earlier messages.** An unfamiliar voice reads as somebody else's mail, and
  people report it rather than delete it. Changing tone is a program decision, not a technique for
  one message.

## Failure mode

**The signal:** there are clicks, but they collect on navigation and on the menu in the footer. The
job did not land: somebody opened, found no reason, and went to browse instead.

`inbox-line.md` describes a failure with the same signal, and opens separate the two. A falling
on-job click share with opens flat is this file's failure: the body lost the job. A falling share
with opens rising is the inbox line selling what the message does not contain. Opens carry a
machine component and decide nothing on their own, so read them as a direction and no further
(`SKILL.md`, control metric). Where they are flat in both cases, run step 4 of `inbox-line.md` and
check the subject against what the message hands over.

**The second signal, which behaves the opposite way:** clicks collect exactly on the work links and
then people leave the destination immediately. Here the copy did not underdeliver, it overdelivered:
the message promised more than the page hands over. The fix is in the message rather than on the
page, and the two cases must not be confused, because they look identical in a click report and
opposite in a page report.

**What to do:** in the first case, move the job back into the first block and delete everything that
is not argument (steps 1 and 3). In the second, remove the claim the destination does not support,
and check the promise against what the person sees after the click.
