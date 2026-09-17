---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# The inbox line: sender name, subject, preheader

The unit here is **the inbox line**: three fields read as one. They are decided differently. The
sender name belongs to the program and changes rarely. The subject and the preheader belong to the
message and are written last.

This file does not decide whether the mail arrives in the inbox at all. Authentication, reputation
and the sender name as a provider requirement are `deliverability`.

## Entry conditions

A draft of the body exists. This is a condition rather than a preference: a subject written first
starts pulling the text toward itself, and the job of the message quietly rearranges itself around
a phrase somebody liked.

## Exit conditions

A sender name, a subject and a preheader that pass three checks: the subject matches what the
message delivers, the subject survives being cut, and no meaning rests on an emoji or on capital
letters.

## Steps

**1. The sender name is a program decision, not a message decision.** It has to be recognized by
the person receiving it, which is the requirement `deliverability` leaves here, and recognition
rests on staying the same. A changed name reads as a new sender: the mail stops being findable by
search in the mailbox, and earlier messages stop accumulating into a sender somebody trusted.

The threshold: change it no more than once per program cycle, and never during a placement
incident. Changing identity in the middle of a delivery problem adds a fresh warmup to an unsolved
one, and that belongs to `deliverability`.

**2. Write the subject as the shortest true statement of the job.** From the brief, not from the
text. The text is how the job gets done; the subject is its name.

**3. Put the deciding words first.** Display width differs by client and by device, and this skill
ships no character count: the numbers in circulation come from other people's audiences. Use a
check instead. **The subject has to survive being cut at the point where your own readers stop
seeing it.** Find that point the way step 8 of `body-and-action.md` finds the clipping point: send
yourself the message in the two or three clients most common in your base and look at where the
subject is cut, on a phone and on a desktop. Until you have looked, **take the first third of the
subject as the starting point**: it is a placeholder rather than a measurement, it holds while your
subjects stay about the same length as each other, and you replace it with your own cut-off the
first time you check. Read whatever survives the cut on its own. If it does not say what the message is
about, the subject gets rewritten rather than shortened.

**4. Check the subject against what the message delivers.** The subject states something the
message hands over, and the first block confirms it. The same requirement appears in law and in
mailbox provider rules, and that side, with its sources, is in `deliverability`. The operational
half is here, and it is an order of work: decide what the message delivers, then name it.

One defect this step catches: a subject that names the secondary thing. A message invites people to
a conference and also lists three blog posts; the subject names the posts. The invitation will not
read as the point of the message even when it takes up the whole first screen.

**5. The preheader completes the subject and never repeats it.** An unwritten preheader is not
empty: the client pulls the first words out of the body, which can be a utility line or the start of
a heading. You have two choices, write the preheader or make the first line of the body worth
showing, and no third one, because something gets shown either way.

**6. Emoji, capitals and punctuation are an audience question, with one hard rule.** What works on a
given base is shown by a test on that base, and `experiments-and-holdouts` owns the test. No general
claim is shipped here. The hard rule: **meaning may not rest on an emoji or on capital letters.**
Check it by removal: delete the emoji and read what is left. If a word went missing with it, the
subject is broken. The receiving client draws that character, not you, and a reader on a screen
reader hears whatever their software calls it.

**7. No list of words exists, banned or magic.** Say so plainly, because the question arrives
constantly. Step 4 answers the worry the list is reached for: a subject that matches the message and
promises nothing extra is not the kind of subject filters and readers are reacting to.

**8. A triggered subject has to be true at the latest moment the message can arrive.** The event
ages. "Your cart" is true after an hour and doubtful after a week. Choose the wording for the
latest arrival, not the average one, because the average case is not the one that generates the
complaint.

The latest arrival is later than the latest send, and two neighbors hold its halves.
`triggered-messages` holds the longest delay the flow permits before it fires. `deliverability`
holds your platform's retry ceiling, which is what a receiver that defers your message spends
before handing it over. Add the two and write the subject for that moment rather than for the
moment the flow fires.

## Thresholds and timings

- **The subject is written after the body, always.** One exception: a message whose entire job is to
  state a fact, such as a confirmation or a status. There the subject is the job and it comes first.
- **Whatever survives the cut carries the point**, which is the check that replaces a length. The
  first third is the starting point you use until you have measured your own cut-off.
- **A triggered subject is written for the latest arrival**, meaning the flow's longest delay plus
  the retry ceiling, not for the moment the flow fires.
- **The sender name changes no more than once per program cycle**, and never during a placement
  incident.
- **A resend's subject may not contradict the first one.** Whether to resend at all is
  `email-program`. The rule here is that somebody who sees both must not be handed two different
  promises about one message.

## Edge cases

- **A message with no freedom in the subject**, such as an order or delivery notice: the subject
  names the event and the reference number, and subject-line technique is out of place.
  `transactional-messaging` owns that class.
- **A base in several languages.** A subject is rewritten rather than translated. Word order decides
  which half survives truncation, and word order is not the same across languages.
- **A long company name, or a brand nobody knows yet.** The sender name carries recognition, not
  completeness. The explanation goes in the preheader, not in the name.
- **A message the person is waiting for**, because they just subscribed or just ordered. Name the
  expected thing directly. Intrigue works against recognition here, and recognition is the whole
  job.

## Failure mode

**The signal:** opens rise while the on-job click share falls. The inbox line is selling something
the message does not contain.

**The second signal, which behaves the opposite way:** opens do not move at all, in either
direction, however much the subject changes. Check two things before touching the subject again:
whether the mail is reaching the inbox at all, which is `deliverability`, and whether the opens in
this base are largely machine generated, which leaves the human share invisible. The second is in
`SKILL.md` under the control metric.

**What to do:** in the first case, stop the whole family of subject lines rather than editing them
one at a time, because the defect is in the technique and not in the phrasing, then go back to step
4 and write the subject from what the message hands over. In the second, leave the subject alone
until delivery has been checked, and read subject decisions on clicks rather than on opens.
