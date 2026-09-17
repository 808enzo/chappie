---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# The template: frame, block library, base layer and layers

The unit here is **a template version**, and the decisions belong to the template's owner. A
template is what every message is assembled from and what does not change from one send to the next.

`rendering-check.md` checks a version in real environments, `block-states.md` covers what a block
shows when there is nothing to put in it, and `email-copy` writes the words inside the blocks.

## Entry conditions

The program sends more than one kind of message, or at least one message is assembled from
substituted content, or a template is about to change. A single message laid out by hand once a
quarter is not a template, and this file does not apply to it; `rendering-check.md` does.

## Exit conditions

A registry of templates, each with its version in use and an owner. Every version has a frame, a
block library with contracts, declared layers, a text part, a size budget and a release record, and
its identifier is stamped on every send.

## Steps

**1. Keep a registry of templates.** Every template any send goes out on, whether campaigns, flows or
service messages, with the version in use, its owner, and the flows that use it. Nobody releases a
template that has no owner. A flow running on a version the registry does not hold is a send outside
the template, which is the second failure mode below.

**2. Separate the frame from the blocks.** The frame is what every message of the template carries
and what no send may edit: identification of the sender; the elements your regime requires, with
that regime, `consent-and-preferences` and `deliverability` deciding which ones apply; a visible
unsubscribe link and a link to the preference center; and a link to the web version. All three links
carry the required role in `email-copy`'s sense and stay outside the control metric. The frame is
locked in the editor, and only the template's owner can unlock it.

This is where the required elements get an owner. The requirement comes from the neighbors. The
place is the frame. The check runs at the release of every version (`rendering-check.md`, step 4)
and on the size of every send (step 8 below).

**3. Give every block a contract.** For each block in the library, write down: what it carries (the
job, the action, support, or decoration); where its content comes from (static, a substitution, a
selection); its declared size and its minimum; its states, meaning full, short, stand-in and removed
(`block-states.md`); and what leaves together with it when it is removed, such as the heading, the
image, the button, and links pointing at it from other blocks.

**The minimum follows from the layout.** It is the smallest number of items at which no layout of
the block, in the narrowest or the widest of your environments, leaves an empty cell. Whether the
block's heading is still true at the minimum is a question for `email-copy`.

**4. The base layer carries the job.** Every element that carries the job of the message or its
action is live text. A button is text on a colored cell rather than an image of a button. A phone
number, an address, a code and a deadline are text. A QR code comes with the link it encodes,
for the reader who sees it on the same phone they would scan it with. A chart comes with its
figure written out.

**A violation is fixed by moving the action into text, not by adding an image of it.** An image that
carries information gets a text alternative that serves the same purpose; a decorative image gets an
empty one, so assistive technology skips it (WCAG 1.1.1; its scope is in `SKILL.md`).

**5. Declare every layer above the base, and give each one a fallback on which the job survives.**
The layers are dark scheme tuning, web fonts, background images, animation, interactive parts and
video. **The deletion test:** remove the layer, and the message still does its job. A layer that
fails the test is part of the base, built on the assumption that every environment will show it.

**6. Hold color in both schemes.** Measure the contrast of text that carries the job or the action
against its real background in each scheme (the reference measure is WCAG 1.4.3). Do
not let color be the only sign of an action (1.4.1). Give a dark logo on a transparent background an
outline or a backing. Under every background image, set a background color on which the text still
reads if the image never arrives. Text over an image that carries the job also exists as live text.

**7. Hold the narrowest width.** A block reflows to one column at the narrowest width among your
environments, and nothing requires scrolling in two directions (the reference measure is WCAG
1.4.10). Tap targets meet WCAG 2.5.8 or are spaced the way the criterion allows. A link inside a line
of text is one of the criterion's exceptions.

**8. Set a size budget and an order.** The job, the action and the required elements sit **above the
earliest clip point** found in your environments (`rendering-check.md`, step 2). You find the clip
point with a seed send of a deliberately long message. The size of an assembled message depends on
the send, because selections and substitutions change it, so check it on every send: automatically if
your platform can, otherwise on the longest assembly.

**An index message**, meaning a digest or a roundup whose length varies by design, also carries the
route out as a text link at the top of the frame, because keeping it under the budget is not
something you can guarantee.

**9. Carry a text part.** Every message carries a text part with the job, the action's link and the
required elements. Alternative parts are ordered by increasing faithfulness to the original, and a
client shows the last one it supports (RFC 2046, section 5.1.4), so the text part is what a client or
a reader that declines HTML sees. If your platform generates it, read it at release: the order of the
job in it has to match the HTML.

**10. Version and release.** Every change to the frame or the block library is a new version, with a
record of what changed, when, by whom and why, in the sense `program-audit-and-ops` gives the word.
A version ships only after the check in `rendering-check.md`. Stamp its identifier on every send
before anything happens to that send. Keep the previous version available until you have read the
control metric once on the new one.

Comparing two versions as an experiment is `experiments-and-holdouts`. Reading the result by
environment belongs here, because an average across environments hides a break in one of them.

**11. Retire templates.** A template no send has used for a full program cycle leaves the registry,
and no flow can select it. A flow still sending on a retired template is a finding for whoever is on
duty.

## Thresholds and timings

| Value | What sets it |
|---|---|
| Minimum of a block | the block's layout in your narrowest and widest environments |
| Contrast, target size, reflow | WCAG 2.2 as the reference measure; its scope is in `SKILL.md` |
| Clip point and size budget | a seed send of a long message in each of your environments |
| Cycle after which an unused template retires | your own program's cycle (`email-program`) |

## Edge cases

- **The brand book asks for messages built from images.** The brand lives in a layer and the job
  lives in the base. A message built entirely from images cannot be edited without going back to the
  layout, and it loses its job in every environment that does not show images. The argument is
  settled by the deletion test, not by taste.
- **One template for two brands.** A frame per brand, one shared library: two senders carry
  different required elements.
- **Long values and translations.** A block holds the longest value the field's format contract
  allows (`personalization`), and a button holds its longest translation. A button label cut short
  loses its verb or its outcome.
- **A service message.** The same steps with a reduced library. Whether a promotional insert changes
  the class of a service message is `transactional-messaging` and `contact-orchestration`; a service
  frame does not reserve a place for one by default.
- **Forwarding.** A forwarded message is reassembled by somebody else's client. The web version link
  in the frame is how it can still be seen as released.
- **The editor lets people unlock the frame.** A send with an unlocked frame is a send outside the
  version, with everything the second failure mode describes.

## Failure mode

**The signal:** the template holds only where the author looks. The environment click index fell in
one environment of one provider, the other environments of that provider rose, and the preview looks
clean.

**What to do:** open the seed mailbox for that environment and toggle its conditions
(`rendering-check.md`). If it is broken, pause the flows on that version through
`program-audit-and-ops`, which does not send a correction for broken layout, roll back to the
previous version, and add the condition that let the defect through to your matrix.

**The second signal, which behaves the opposite way:** the indices are flat and the click rate falls
in every environment at once. People are building messages around the frame: an image pasted into an
HTML block, a copy of an old message. The defect is identical in every environment, so the index
cannot see it. **The question that separates the two:** which version did the send go out on? The
sign is a growing share of sends with no released version. Quiet removal of a block gives the same
flat indices (`block-states.md`); the order to read the causes in is in `SKILL.md`.

**What to do:** bring those sends into the registry or stop them, and ask which block the library was
missing.
