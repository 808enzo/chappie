---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-06
---

# Capture points: where the site asks, and for what

A capture point is a place and a reason: a stage of intent, an audience, an ask, something offered
in exchange, and whatever starts the moment the form is submitted. This file builds the set of
them. Whether any one of them may appear on a given screen is a separate question, answered in
`display-rules.md`.

## Entry conditions

Traffic that does not end in a purchase. A program with a concrete next step that needs the
contact. A way to tell, at display time, who is already known to you: without it every point asks
people who signed up long ago.

## Exit conditions

A written register of points. Each row names the stage of intent, the audience, the ask, the
exchange, what happens in the first minutes after submission, the owner, and the review date.

## Steps

**1. Map the site by stage of intent, not by page.** Five stages:

| Stage | Where it lives | What the visitor lacks |
|---|---|---|
| Arrival | home page, campaign landing page, article | a reason to stay |
| Choosing | catalog, category, search results | a way to narrow down |
| Evaluating | product page, comparison | confidence in one option |
| Deciding | cart, checkout | a reason to finish now |
| Service | delivery, payment, order status, support | an answer |

The stage decides what you can plausibly offer. An offer that belongs to another stage reads as
noise no matter how well it is written.

**2. Name the exchange as a thing, not as a subscription.** "Leave your email for news" asks
someone to pay now for a benefit later. What works at each stage is specific: keep what I was
looking at, tell me when it is back, hold this price, send the selection matching what I picked,
open the private sale, answer the question that is blocking my choice.

The test: **the exchange should be impossible without the contact.** A discount is possible
without an address, since you can show the code on screen. A back in stock notice is not. The
first kind buys contacts and the second kind earns them; read what that costs you in your own
cohorts, split by capture source (`intake-and-usable-contacts.md`, step 6).

**3. Size the ask from the exchange, not from appetite.** Ask for what you need in order to
deliver what you promised: an address to send to, a phone number to call, the attributes the
selection is built from. Every additional field costs you abandonment, and you can measure the
rate on your own forms: submissions over displays, split by number of fields, across at least two
of your own forms.

**4. Build the ladder.** First screen: the identifier, plus at most one field the exchange cannot
work without. Second screen: what improves the very next step, such as interest category, gender
or city. Everything else comes later, by email or in the account.

**Save what the first screen collected before showing the second.** A multi step form that keeps
nothing until the end discards every contact that stopped partway, and those are contacts the
person already handed over.

Which attributes the base needs, and in what order they are collected, belongs to `list-building`.
What stays here is that the first rung is short and lives in a form on the site.

**5. Name the exclusions.** Pages where nothing interrupts:

- checkout and payment, where interrupting a purchase trades revenue for a row in the base;
- support, order status and error pages, where the person is solving a problem;
- any screen where another form is already open.

A format limit sits beside these on every page rather than on a list of pages: no overlay that
obscures the entire page, under the search engine's guidance on intrusive dialogs (`SKILL.md`,
Platforms).

The exclusion is about interruption, not about fields. The checkout takes an address for the order,
and that field is still intake: it is validated in place like any other
(`intake-and-usable-contacts.md`, step 1), and the contact it produces holds the *requested
message* state for the service messages of that transaction and nothing beyond them
(`transactional-messaging` owns those messages; a typo there is a defect of this screen). A
marketing tick box beside that field is a capture point of its own, with its own register row and
its own cohort, and step 7 of the intake file reads what that cohort is worth.

**6. Put the points in one register and give each an owner.** Without it points get added per
campaign, never removed after it, and by the end of the year they compete for one screen with
nobody accountable for any of them.

## Thresholds and timings

- **One point equals one stage, one audience, one exchange.** Two points offering the same thing
  at the same stage are not a set, they are a duplicate: each eats the other's displays and both
  become unreadable.
- **Number of fields on the first screen** comes from your own abandonment statistics, split by
  field count, not from a rule of thumb.
- **Review the register quarterly, as a starting rhythm.** Shorten it where points get added
  faster than that. It is a rhythm, not an expiry date: a point lives as long as its exchange
  stays true, meaning the product line still exists, the sale is still running, the guide is still
  current.

## Edge cases

- **Out of stock item.** Capture here is service, not marketing: the person is asking to be told.
  The point sits on the product page with no inventory, the promise is kept by an event rather
  than a newsletter, and confirmed opt in does not apply to it (`intake-and-usable-contacts.md`).
- **Known but unreachable.** The address bounced, the number changed, consent was never recorded.
  A repair point asks for a current contact rather than a new one, and it cannot pay in a first
  purchase discount: this person has bought from you before. What it collects is not new to the
  base, so it never enters the control metric; it is read on its own line, restored contacts per
  thousand sessions shown the point (`SKILL.md`, control metric).
- **Subscribe and buy in the same session.** The person gives the address at a point before the
  purchase and orders minutes later. `welcome-and-activation` does not start its series for them,
  and it counts them: once that group is large enough to move its number, the point is standing
  in front of a purchase that was going to happen. Move it after the purchase: the order
  confirmation page is a stage of its own, the person is known, the exchange is what comes after
  the order (tracking, care, the next selection) rather than a first order discount, and the
  marketing ask stays a separate tick with its own record. The register carries both positions as
  two rows, and the share of same-session buyers by point is what decides between them.
- **The web push invitation.** A capture point where the ask is the browser's permission and the
  exchange is something only a notification can deliver: word the moment an item is back, word
  when a price moves. The site's own pre-prompt is the point, the display rule governs it like any widget, and
  the browser's native prompt behind it is `push-notifications`': what the browser allows, the
  endpoint that results, and how the ask is read. It is not a usable contact and never enters the
  control metric; the neighbor reads it as new endpoints per thousand sessions of the same fixed
  population.
- **B2B and a long cycle.** Whoever makes the call needs the qualification; the form does not.
  It goes on the second rung or into the conversation, and the first screen keeps the
  identifier. Working the lead afterwards is `b2b-lifecycle`.
- **An offline customer visiting the site for the first time.** Known to the stores, unknown to
  the site. The point must be able to recognize a card or phone number instead of creating a
  second profile; the stitching itself is `list-building`.
- **A quiz or product selector.** Show the result first and ask for the contact after it. The
  person has already paid in time, and charging a second price for their own result reads as a
  trick. Derive the number of questions from your own step by step completion data, and state
  that number on the first screen.
- **A content page with nothing to sell.** The exchange is more of what they came to read. A
  contact bought with a discount on an article arrives in the base with no interest in buying.

## Failure mode

**Points get created for a campaign and stay forever.** The symptoms: two windows on one page
promising unrelated things from the same brand; a form offering a discount on a collection that
sold out months ago; a register row with no owner. The damage is not irritation, it is loss of
control, because the impressions are spent by dead points and the live one never reaches an
audience.

The answer is the register with an owner and a review date, plus one question at every launch:
which existing point does this one replace?
