---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# The display rule: who sees a widget, when, how often, and which one wins

The register says where the site may ask. The display rule decides whether any of it opens on this
screen, for this visitor, right now. It governs every onsite widget, including the ones that ask
for nothing: a recommendation block, a survey and a proactive chat opener compete for the same
screen as a subscription form, and only a site level rule can settle that.

## Entry conditions

The register of capture points exists. Visitor state can be read at display time, at minimum
whether the person is already in the base. There is one place where the rule executes.

## Exit conditions

A written rule, running in a system: who each point is visible to, which signal opens it, how many
times, what a refusal changes, which point wins a collision, and how mobile differs from desktop.

## Steps

**1. Split the audience by state, not by segment.** Four states: anonymous; known and reachable;
known and unreachable; already gave what this point asks for. The base rule is **never ask for
what you already have**. A subscriber shown a subscription form reads it as being forgotten.

**2. Choose a readiness signal instead of a timer.** Signals worth using: pages or product cards
viewed this session, scroll depth on the page, time on a specific page, a repeat visit, an item
added to the cart, an attempt to leave. Join them with *or* rather than *and*: people reach
readiness by different routes, and a strict conjunction excludes everyone who arrived by a route
it does not name.

Delay is a parameter, taken from your own analytics, and the two distributions come from two
different populations: time to the primary action, among the sessions that reached it; time to
exit, among the sessions that left without it. Put the display **after the median time to the
primary action and well before the median time to exit**. Compute both before you believe the
rule, because the order is not guaranteed: where the leavers leave sooner than the buyers decide,
the exit median comes first, and then there is no timer that is late enough for one group and
early enough for the other. When the two sit close together or in that order, the signal has to
be behavior, not time.

**3. Build the ladder of waves.** The first wave is the loudest, and there is only one of it.
Closing it without acting is an answer rather than an accident: the second wave is quieter, a side
panel or an inline block, and it offers something different. The third is a static form that sits
on the page and interrupts nobody. **Every refusal lowers the volume; none of them raises the
frequency.**

**4. Set frequency and the gap.**

- One display per session **per person**, not per point, or three points add up to three windows.
  The cap counts what interrupts: an overlay, a side panel, a proactive chat opener. A static
  inline block does not spend it, and neither does something the person opens themselves, the
  icon or notifications area from the edge cases below; otherwise the third wave, which
  interrupts nobody, would lock the screen against every other point.
- After a close, the point stays quiet until the next visit, and returns there one wave quieter.
- After several consecutive closes, it stops appearing at all. The number comes from your own
  data: submissions among people who closed the same point before, by how many times they had
  closed it. You can read that distribution only on people who were shown the point beyond the
  current cap, and the cap removes them: once it stands at three, nobody sees a fourth display,
  and the fourth display's submissions are unobservable. So fix the number by version, hold a
  small share of people past it, and recompute from that share on a retrospective rather than
  continuously. Expect the readable signal to run out within the first few repeats.
- After a submission, the point is off for that person permanently.

**5. Resolve collisions.** When two points want one screen, the one closer to the decision wins: a
service display (back in stock, order status) outranks a capture point, a point on the product
page outranks one on the category, and a category point outranks a site wide one. The underlying
rule is the one orchestration uses, **more specific and more perishable wins**; the difference is
that the unit here is a screen in a session rather than a person over a period. The loser is not
queued behind the winner in the same session: it returns on its own signal in a later session,
under the same cap. Count how often each point loses, in its register row. A point that loses
every collision has no audience, and that is the failure mode of `capture-points.md` arriving by
a different door: the answer is to retire it or move it, not to raise its rank.

**6. Separate the devices.** A mobile rule is not a shrunken desktop rule. The form takes the whole
screen, so a loud wave costs more, and exit intent does not exist without a cursor. The
substitutes, a sharp scroll upward, a back gesture, inactivity after activity, are not equivalent
to leaving, and each needs its own threshold.

**7. Check where the rule executes.** Widgets from two vendors cannot see each other: each obeys
its own frequency and the visitor gets the sum. Then the rule has to run on the site itself, as
one layer deciding who owns the screen today. A rule that lives only in a meeting is not a rule.
The same holds at the edge of a signed-in product area: the widget layer of the public pages and the
display layer of `in-product-messaging` see each other, or a person crossing from the catalog into
the account gets both.

## Thresholds and timings

Every display threshold is a parameter taken from your own behavioral analytics. There is no
industry correct moment, because it depends on how long choosing takes in your category.

One absolute, dictated by a platform rather than taste: never let an overlay obscure the entire
page, and never send the person to a separate page for their input. The search engine's
guidance on intrusive dialogs names newsletter sign-up prompts, says intrusive overlays may lead to
poor search performance, and recommends a banner over a full-page interstitial. It sets no size, no
delay and no device, so those stay parameters from your own data. The ad format standards the
browser enforces bind third-party ads, not your own point. Quotes and dates are in `SKILL.md`,
under Platforms.

## Edge cases

- **A known person on a new device.** Recognition runs on the device, so a regular customer on a
  new phone falls under the anonymous rule. The fix is not in targeting but at intake: the
  submitted address is matched against the base and attached to the existing profile as a
  pending change, which becomes the profile's only after the confirmation click proves control
  (`intake-and-usable-contacts.md`, step 1), instead of creating a second one. The wording has to
  survive meeting your own customer, which "get your first order discount" does not.
- **Arrival from an email.** The link names a person, so for this session the state is *known*,
  with whatever that person has already given. A point asking for what they gave stays closed;
  one asking for something else, a phone number, a restock alert, may open. Two things keep the
  link from being more than a session-level guess: a forwarded email brings someone else under
  the same link, and a person in the *requested message* state arrived from the one message they
  asked for and is not in the marketing base at all. So the link sets the state for the display
  rule, and the match at intake decides who the address belongs to. A subscription form that
  still opens for the subscriber who clicked through is the defect: the rule is keyed to the
  session rather than to state.
- **A reader rather than a buyer.** The same article serves both. The readiness signal here is
  reaching the end of the piece, not elapsed time.
- **Campaign traffic on a landing page.** The form is the purpose of the page, not an
  interruption, so the gap rule does not apply to it.
- **Coming back to something closed.** A closed window can stay retrievable through an icon or a
  notifications area. That is how you recover the people who closed it reflexively: it turns a
  refusal into something reversible, and opening it is the person's act, so it does not spend
  the session's display.

## Failure modes

**The rule lives in someone's head, not in a system.** Diagnose it by asking where exactly the
restriction executes and getting no answer. Common shapes: two widget vendors; a point built for
new visitors left on "show to everyone"; a campaign that ended while its window stayed.

**The quiet, expensive one: capture rises and orders fall.** The widget is read by its own
conversion, which looks good, and nobody checks what happened to the page it opened on. This is
visible only against a group that was not shown the point. Designing that comparison is
`experiments-and-holdouts`; what belongs here is the obligation to demand it before rolling a
point out to the bottom of the funnel, meaning the cart, the checkout, or the page of an expensive
item.
