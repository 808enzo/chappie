---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-06
---

# Vocabulary of onsite capture

The three mechanics assume these terms. The first pair, *session* and *person*, is the reason most
arguments about pop-up frequency never resolve: the two sides are counting different things.

## The unit

**Session.** One visit, by a browser, to your site. It is what you show a widget to, and at that
moment you may not know who is behind it.

**Person.** The profile a message is addressed to. Capture is the act of turning the first into
the second.

**Visitor state.** What you know at display time: anonymous; known and reachable; known and
unreachable; already gave what this point asks for. You read state live and it can be wrong, because
recognition runs on the device rather than on the person.

## The point

**Capture point.** A place and a reason where the site asks for a contact: stage of intent,
audience, ask, exchange, and what starts on submission.

**Ask.** What the form requests, meaning the fields.

**Exchange.** What the visitor gets in return. A well built exchange is impossible without the
contact: a restock notice needs an address, a discount code does not.

**Ladder.** Splitting the ask across steps: the identifier now, attributes later. Also called
progressive profiling.

**Capture source.** The profile field naming the point a contact came from. Without it, quality by
point is unreadable and cannot be reconstructed later. It is a field on a person's record, so it
expires with that record; the history it feeds survives in counts by point and period, which hold
no person.

## The rule

**Display rule.** Targeting by state, readiness signal, frequency, gap, precedence in a collision,
and excluded pages. It governs every onsite widget, not only the ones that ask for something.

**Readiness signal.** The behavior that opens a point: depth, dwell, scroll, a repeat visit, an
add to cart, an attempt to leave. Contrasted with a timer, which fires on everyone alike.

**Exit intent.** A display triggered by signs the visitor is leaving. It relies on a cursor, so it
does not exist on mobile, where the substitutes approximate it and none of them are equivalent.

**Wave.** The volume level of a point. A ladder of waves gets quieter after each refusal: loud
overlay, then side panel, then a static form.

**Gap.** The minimum distance between two displays to the same person, counted in sessions rather
than in time.

**Eligible session.** A session the display rule allowed to see a capture point. It is a property
of the rule, not of the site: change the rule and the count changes, which is why it lives in the
local efficiency readings, the numerator of eligible share and the denominator of impression rate,
and never in the denominator of the control metric.

## The result

**Deliverable address.** A mailbox there accepts mail. It says nothing about who filled in the
form, and a successful delivery does not upgrade it: you tested the address, not the person.

**Channel control.** Whoever answered the confirmation can read that mailbox. It is the strongest
thing a capture point establishes on its own, and it is still not identity.

**Handover state.** The state intake produces, and what it permits next: *requested message*, one
named message the person asked for and nothing beyond it, or the service messages of the one
transaction the address was given for; *marketing*, permission for the program, asked for
separately and recorded; *pending*, submitted with the confirmation or the basis still missing,
and closed by the confirmation window; *suppressed*, a hard exclusion. Leave the state ambiguous
and whoever sends next makes the decision for you, on a guess. Which basis makes a marketing state
permissible is `consent-and-preferences`.

**Usable contact.** New to the base, deliverable, with consent recorded, and confirmed where
confirmed opt in applies. Anything short of that is a row, not a contact. A contact in a requested
message state is not one either: it is usable for the message it asked for, and folding it in with
the rest is how a base ends up larger on paper than in law.

**Restored contact.** A current address or number given by a person the base already holds and
could not reach. Not new to the base, so not a usable contact; it is what a repair point produces,
and it is read on its own line.

**Fixed population.** The sessions you read the control metric against: sessions on the public
pages of the site, defined by a field you can filter on, bots out and the signed-in product area
out. You declare it once and hold it still across readings. Changing it ends the series, so record
any change you have to make with its date and the readings on either side of it.

**Known share.** Sessions recognized as already in the base over the fixed population. Read next
to the usable capture rate: those sessions cannot produce a new usable contact, so the rate drifts
down as the base matures, and the known share says how much of a fall is that. Recognition runs on
the device, so it is a floor and its trend is what you read.

**Usable capture rate.** Usable contacts per thousand sessions of the fixed population. The control
metric of this skill. Not per thousand eligible sessions: the display rule sets eligibility, so
narrowing the rule cuts that denominator faster than it cuts the numerator, and the rate rises while
the base receives fewer contacts.

**Eligible share.** Eligible sessions over the fixed population. Read it next to the usable capture
rate: it separates a rule that reaches more sessions from a rule that converts more of the sessions
it reaches.

**Consent record.** What the person saw, when, on which page, through which point, and which
version of the wording. A ticked box on its own is not a record.

**Confirmed opt in.** A second step where the person confirms the address they entered. Costs part
of the volume, buys a base without borrowed or mistyped addresses. It is what turns a deliverable
address into a controlled one.

**Cannibalization.** Capture rising while the primary action of the same pages falls. Visible only
against a group that was not shown the point.
