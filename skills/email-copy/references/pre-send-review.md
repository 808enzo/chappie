---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# The review before the send: what stops a message going out

The unit here is **a send standing at the door**. This file is not editing and not taste. It is the
separation between a defect that stops the message and a remark that stops nothing, and the order
in which the two get looked for.

Monitoring a flow that is already live is `program-audit-and-ops`. Comparing two versions to see
which performs better is `experiments-and-holdouts`. What happens here happens once, before
anything leaves.

## Entry conditions

The draft is final, the audience is assembled (`email-program`), the send is scheduled, and there
is time left to fix things. A review that cannot physically stop the send is not a review, it is
reading afterwards.

## Exit conditions

The send is released or held, and the reason is written down. Both get written: without the record
you cannot count either the share of sends held or the defects found after the fact, and the
failure mode of this mechanic is read off exactly those two counts.

## Steps: the order is the mechanic

The order does not change. Cheapest to detect and most expensive to miss goes first.

**1. Reconcile the promise.** Does the message promise what the program will honor? Two
reconciliations, both left here by neighbors. The wording of a benefit against the order in which
benefits apply, because two benefits applied in sequence do not add up while a person reads a sum
(`offer-design`). The wording of a promise against the wording of the capture point, because a
promise reads as kept when the person recognizes the words they saw
(`welcome-and-activation`). **Blocks the send.**

**2. Check the claims.** Every claim traces to a fact (`body-and-action.md`, step 4). Start with the
sentences that appeared after the brief was written: claims added during the edit are the ones
least likely to have a fact underneath, because nobody went looking for one. **Blocks the send.**

**3. Read for the legal line.** Is the urgency real; is the testimonial genuine and not conditioned
on being positive; can the reader tell this is advertising; does free mean free. The regimes and
their sources are in `SKILL.md`. **Blocks the send.**

**4. Test the substitution on edge values.** Send tests to addresses where the field is empty, very
long, in a different grammatical form, and a list with one item. A sentence that breaks **blocks the
send**. A sentence that reads awkwardly while staying true is a remark.

**5. Check survival.** Images off, message clipped, message read in a preview pane. Are the job and
the action still there? A disappearing action **blocks the send**.

**6. Check the links.** Every link opens, leads where the message said, and carries its role
(`message-brief.md`, step 6). Two destinations block. One **contradicts** the message. The other
does not **carry** what the message promised, and that is the quiet one: `body-and-action.md`
reports it later as clicks landing exactly on the work links while people leave the page at once.
Read the destination as somebody who has just read the message, and require the promise to be
visible there rather than merely unopposed. Both **block the send**, and you fix the second in the
message rather than on the page, because the message is what goes out today. A destination that
carries the promise and is merely thin is a remark addressed to the page.

**7. Read it aloud, last and whole.** This catches what no itemized check catches: somebody else's
voice, an argument that does not join up, a sentence nobody can say out loud.

**Remarks are everything else:** a different phrasing, a better order of paragraphs, an idea for
next time. They do not stop a send and they are not discussed at the moment of sending, because a
review that turns into editing stops arriving on time.

## Thresholds and timings

- **An author does not review their own work.** Somebody else reviews it. Where there is nobody
  else, time reviews it: text written today is read tomorrow. This is the only substitute and it is
  worse, because it catches language and misses inheritance.
- **The review starts early enough for a blocking defect to be fixed.** What has to be named is not
  a duration but a person: who holds the send. A review with no such name is a meeting.
- **A triggered message is reviewed when it changes, plus on a rereading rhythm.** The rhythm is set
  by how fast the world around the message moves rather than by the calendar: the more often terms,
  offers and prices change, the more often the mail that sends itself gets reread.
- **A rereading has no door to hold, so name what blocking means there before you start.** The
  message is already going out and the classes do not change: a broken promise, a claim with no
  fact, a legal breach, a broken substitution, a disappeared action, a destination that contradicts
  or does not carry the promise. The action changes. A blocking defect in a live flow is an
  incident, and the route is `program-audit-and-ops`: pause the object, then fix the words, and
  write the pause into the counts below as a hold. File such a defect as a remark because nothing
  could be stopped and you are already in the first failure mode.
- **Every campaign message is reviewed.** The argument that the template is unchanged does not hold:
  blocking defects live in the inheritance and the claims, and both change from message to message.

## Edge cases

- **There is no time.** Run the short review, meaning steps 1 to 3, and say out loud that the rest
  was not checked. Shortening does not remove the requirement to name who can hold the send.
- **Fifty product cards.** Review the frame in full and a sample of cards: the first, the last, and
  every card where a value is substituted. Checking every card is catalog work rather than message
  work.
- **A message that has gone out many times already.** Check the inheritance and the claims; do not
  reread the language. Rereading language on a repeat send spends the review on the part that did
  not change while the inheritance did.
- **The reviewer disagrees with the text.** Disagreement is a remark unless it lands in steps 1 to
  6. The separation has to be written down in advance, or the blocking class quietly expands to
  include taste and sends start standing still.
- **The message was assembled by a model.** Same review, with step 2 run harder
  (`body-and-action.md`, edge cases).

## Failure mode

**The signal:** nothing is ever stopped. The review happens, boxes are ticked, and across a quarter
not one send was held, while defects keep being found afterwards through complaints and questions to
support.

**The second signal, which behaves the opposite way:** almost everything is stopped, sends get
postponed, and when the held defects are examined they turn out to be remarks: a different phrasing,
a different order of paragraphs. The review has become editing and is now costing the program its
slots.

**What to do:** in the first case, put the two counts side by side, sends held against defects found
after the send. If the second is not zero while the first is, the review is missing the blocking
classes, and the place to start is step 1, which is the step that needs a neighbor's file open and
therefore the easiest one to skip. In the second case,
return remarks to their class and forbid discussing them at the moment of sending; if that does not
help, you have two reviewers with different ideas of what blocks, which means the class was never
written down.
