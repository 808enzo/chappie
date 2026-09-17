---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# The check in real environments

The unit here is **a template version in an environment**, and the decision belongs to whoever
releases the version. This file answers where people read your messages and whether the
version holds there.

`template-system.md` covers what the template is made of, and `block-states.md` what a block shows
when it is empty. The fifth step of the review in `email-copy` checks whether the meaning survived.

## Entry conditions

Any one of four: a template version is ready to ship; a send carries an assembly that no check has
seen; the order of environments in your base has changed; or a client in your matrix has announced a
change to how it renders mail.

## Exit conditions

A result recorded for every environment and condition, a recorded release decision, an owner for
every known defect, and **the share you ship unchecked, written down as a number**.

## Steps

**1. Build the environment list from your own base before opening any tool.** From the messages
providers accepted in the last period: the provider, read from the MX record the way `deliverability`
reads it; inside each provider, the environment, meaning the client family and device class your
platform reports, taken from people's clicks before the period; and the unknown share as a row of its
own.

**Weight the list by accepted messages.** Not by opens: Apple states that Mail downloads remote
content in the background regardless of engagement, so opens overstate environments that load content
that way, and Microsoft states that classic Outlook does not download pictures automatically by default
for senders outside the reader's safe senders list, so a tracking image understates those environments. Not by
clicks on the current send either: an environment where the template is broken stops clicking and
drops out of the count, so the failure hides itself.

**2. Build the matrix.** Take environments in order of share until what remains equals the share you
are willing to ship unchecked, and write that share down. For each environment, check under these
conditions:

- **as the client shows mail by default**;
- **images off.** Gmail offers a setting to ask before displaying external images, and it holds back
  images on its own in a message it considers suspicious. Classic Outlook does not download pictures
  automatically by default, except from senders on the safe senders list;
- **a dark scheme**, where the environment offers one. Microsoft states that dark mode in new, classic
  and web Outlook gives the reading pane a dark background, with a button for the reader to switch it.
  WebKit describes Mail on macOS displaying simple messages with a dark mode interpretation;
- **the narrowest width**, including a narrow preview pane in a desktop client;
- **clipped.** One seed send of a deliberately long message per environment, with a subject line
  nobody else has used;
- **animation off.** Microsoft states that Outlook plays animated graphics by default, and that in
  Outlook for Microsoft 365 from version 2008 playback follows the Windows animation setting; with
  animation off, only the first frame appears;
- **the fallback part in place of the interactive one** (the layers section below).

**3. Emulated preview first, live mailboxes second.** A preview tool draws its own model of a client,
and the client changes without telling the tool. A live seed mailbox in the environment catches the
difference. One mailbox per environment, opened on a device of that class, with the conditions
switched on it. The platform's own preview substitutes demo values (`personalization`), so check
assembled blocks with the state profiles in `block-states.md`, step 8.

**4. Read in order: cheapest to see and most expensive to miss comes first.**

- **(a) The required elements are present and readable:** the route out is visible and the sender is
  identifiable. **Holds the release.**
- **(b) The job and the action are live text, the tap target is reachable, and nothing is covered or
  pushed off the edge.** **Holds the release.**
- **(c) No broken state:** a leaked substitution token, an empty cell, overlapping blocks, sideways
  scrolling. **Holds the release.**
- **(d) Text carrying the job and the action reads in the dark scheme.** **Holds the release.**
- **(e) The brand looks right:** the logo, image edges, a replaced font. **A remark**, unless it hides
  anything in (a) to (d).

**5. Decide the release.** A defect in classes (a) to (d), in any environment above your unchecked
line, holds the release. In an environment below the line it becomes a known defect with an owner and
a date, except in class (a): a required element unreadable in any environment you know about holds
the release on either side of the line, because the line is a share of readers you have not looked
at, not a share you may leave without the route out. Remarks do not hold a release.

**6. On each send, run the lighter check.** The assembled message in your top environment with the
state profiles; the size against the budget (`template-system.md`, step 8); the text part; the fallback
parts of any layers. This meets the fifth step of the review in `email-copy`: they read whether the
meaning survived, this reads whether the template held. One person can do both, and neither side
counts the other's check as done until it is recorded.

**7. After the send, read the environment click index** (`SKILL.md`), no earlier than the end of the
click window and after the retry queue has emptied. For an environment below its band, or whose share
of web version clicks rose, open the seed mailbox in that environment. In spam: `deliverability`. One
seed in spam shows where the provider filed that message for that one mailbox. It diagnoses the case
in front of you; it is not a placement rate for your base, and `deliverability` explains why no seed
list gives you one. In the inbox and broken: a template defect, the first failure mode in
`template-system.md`. In the inbox and intact: the row's population changed, so compare who landed
in that environment on this send with the previous one.

**8. Run the matrix again** when a new version ships; when the order of environments changes and a new
one rises above the unchecked line; when a client in the matrix announces a rendering change; and, for
templates behind live flows, on a rhythm set by how fast your environment list changes, which you find
by comparing the lists from your last two periods.

## The layers above the base: interactive parts, animation, countdowns, video

- **Deciding on a layer** starts with the deletion test (`template-system.md`, step 5), and you
  write the fallback before the layer.
- **An interactive part in Gmail.** Google requires the sender to register, messages to be
  authenticated with SPF, DKIM and DMARC, and **a similar HTML or text part**, which Google says is
  shown in its place in many instances. The reasons Google lists include: dynamic email is disabled;
  the setting to always display external images is off; the message was automatically forwarded from a
  different account; it was sent over 30 days ago; the interactive part is too long; translation is
  enabled; the platform does not support it. **The consequence:** even in a supporting environment some
  readers see the fallback, so the job has to survive in it whole. The 30 days are Gmail's rule;
  another client that shows interactive parts has conditions of its own, and you read them from its
  documentation, with the date.
- **Content that changes after the send** is a claim tied to time, which `email-copy` handles: it
  must be true at every moment it is shown. The fallback part freezes at the send, and the two parts
  drift apart as time passes.
- **A countdown.** An image drawn at the moment it is requested shows the moment of the request, not
  the moment of reading, and Apple states that Mail downloads remote content in the background
  regardless of engagement, so what the client shows later is invisible to the sender. The deadline
  therefore stands **beside it in live text**, with the date, the time and the time zone, and after the
  deadline the image shows an ended state. **An animation that restarts its count on every load states
  a false time remaining and does not ship.** The legal side of false urgency is in `email-copy`.
- **Animation.** The first frame carries what the whole animation carries, because where animation is
  off, the first frame is all that shows.
- **Video** ships as a still frame linking to a page where it plays, unless your check showed it
  playing inside the message in your environments. A claim made aloud in the video is repeated in
  text (the FTC disclosure guidance in `SKILL.md`).
- **Forms, carousels and choices inside the message.** The action is also reachable by a link to a
  page. A form that collects personal data carries the wording of its basis, which is
  `consent-and-preferences`.
- **One interactive scenario per message.** Every layer multiplies the number of checks by its number
  of states, and when a message with two layers renders broken, nothing tells you which one broke.
- **A separate index series.** A message with a layer that only some environments show is its own
  baseline series, or the index measures the layer rather than a defect.

## Thresholds and timings

| Value | What sets it |
|---|---|
| The share shipped unchecked | your decision, written beside the matrix |
| Clip point | a seed send of a long message in each environment |
| Rhythm for re-running the matrix behind live flows | how fast your own environment list changes |
| 30 days before Gmail shows the fallback part | Google's documentation; a rule of one client |

## Edge cases

- **An environment you have no device for.** Get a mailbox there through a live rendering service or
  a colleague who reads mail in it. If neither exists, the environment stays below the unchecked line,
  and the record says so.
- **A base concentrated in one environment.** The matrix has one or two rows and the unchecked share
  is close to nothing. The risk left is a rendering change in that one client, so re-run the
  matrix whenever it announces one. The index of that environment sits at 1 by construction and
  moves by no more than the other rows' share (`SKILL.md`); the seed mailbox and the absolute rate
  are what you have.
- **Test sends with the same subject line get grouped into one conversation** and shown as one long
  message, so take the clip point from a message with a subject nobody else used.
- **A platform preview with demo values** hides exactly the class of defect this check exists for
  (`personalization`).
- **A corporate gateway between the provider and the client** that rewrites links or strips styles.
  That environment behaves differently from personal mailboxes at the same provider, so it gets its own
  row if your platform can tell them apart.

## Failure mode

**The signal:** the check has turned into a preview stamp. Every environment passed in the emulator
and no live mailbox was opened. The index falls in an environment marked as checked, and the count of
defects found after release in checked environments is above zero while the count of held releases is
zero.

**What to do:** put a live mailbox back into every environment above the line, and record both counts.

**The second signal, which behaves the opposite way:** the matrix has grown to the tool's list of
clients. Releases wait for weeks and people build messages around the template. The sign is rare
releases and a growing share of sends with no released version (`template-system.md`, second failure
mode).

**What to do:** set the unchecked line by the share of your own base again, not by the list of clients
a tool can draw.
