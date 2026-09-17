---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The exit request and the save

The unit here is **the exit request**: the person's expressed intent to stop, from whichever door it
came. Each stage of the work has an ownership class, because two owners write on the same unit: the
program on the cancel screen; the assignee of `chat-and-bots` when the request arrives as a message,
working from the program's script and the same reason list; the app store, where it bills, which decides
alone while the program reads; and the program again when the request arrives from the bank or as a
dispute. Without the class written on the stage, no step has the right to go out, and a silent stage is
read as a miss, not as pending.

## Entry conditions

The person expressed the intent to stop: opened the cancel screen; wrote "cancel my subscription" in any
channel; canceled in the store (Apple's expiration intent "customer cancelled", Google's
SUBSCRIPTION_CANCELED); had the bank block the recurring charge (Mastercard code 21); disputed a renewal
charge as "cancelled recurring"; or the store began asking for consent to a price increase, without
which the subscription stops (`references/term-end-and-notices.md`, step 8).

## Exit conditions

The request closes as one of: canceled, with the effective date, the reason from the shared list and the
source; kept, with what (nothing: "keep my plan" pressed; a pause with a resume date; a plan change; an
offer with its length), written on the person; abandoned, when the person opened the screen and made
no decision in the session, which is not "kept"; for a price consent, ended on a price not accepted.
The confirmation went out; access holds until the effective date; after it the person is handed to
`lapse-and-winback` with the reason code.

## Steps

**1. Route by source, and name the owner of the stage.** *Screen:* the program, steps 2 to 5. *Message:*
the assignee, with a promised reply time written on the request (a timer), the same script as the screen
(one reason question, one alternative, one offer), and a plain exit: California's telephone rule allows
a retention offer only if the business "first clearly and conspicuously informs the consumer that they may
complete the cancellation process at any time by stating that they want to 'cancel'", after which it
"shall promptly process the cancellation"; a voicemail is answered "within one business day";
cancellation is available "in the same medium that the consumer used in the transaction". Read the
message rule the same way: the word "cancel" in the person's reply is the button, and the assignee
processes it without another question. *Store:* the cancellation is done; on Google the user "retains
access to the content until the end of the current billing cycle"; your part is the record, the
confirmation and, until the effective date, a message inside the product about what ends, without an
offer wherever an offer is marketing on a basis you do not hold. *Bank:* the person stopped the charge
themselves; no retry runs (`references/failed-charge-recovery.md`, step 1); record a cancellation
effective now, keep access to the end of the paid term, and confirm with the way back. *Dispute:* refund
or accept the dispute under your acquirer's rules, which are left to you; record a cancellation with the
reason "dispute". *Price consent:* the store asks and the program reads; no offer; the request closes as
`references/term-end-and-notices.md`, step 8, records it.

**2. Keep the cancel button on every step of the screen.** California: termination "exclusively online,
at will, and without engaging any further steps that obstruct or delay", and a discount or retention
benefit only where the business "simultaneously displays a prominently located and continuously and
proximately displayed direct link or button entitled 'click to cancel,' or words to that effect".
Germany's § 312k, in our rendering: a cancellation button leading straight to a confirmation page and a
confirmation button, both permanently available and directly and easily reachable, and a consumer who is
not given them may terminate at any time without a notice period. Paddle, as one platform, "automatically includes a link to cancel the subscription on each page
of the flow" in "regions that require one-click cancellation". The construction rule that follows: a
screen whose only exit is "stay" is an obstruction, and the number of steps before the cancellation is
not capped by a count but by the rule that every step carries the same button and the button ends the
flow without a further step. Authentication before the screen is allowed (California § 17602(d)(3)),
and a person who will not authenticate keeps the offline route.

**3. Ask the reason once, from the shared list.** The entries live in the theme list `voice-of-customer`
versions and keeps by identifier; the screen shows them and keeps no list of its own. A subscription
needs at least these: price; not using it; a missing feature; switching to another product; temporary (a
season, a trip, a budget); a bad experience; other or no answer. Write the answer on the request. After a
cancellation, the post-cancellation survey goes only to people who gave no reason here.

**4. Offer one alternative per reason, before any offer.** *Price:* a cheaper plan; the sign that price
was the reason is the reason itself (`repeat-purchase` reads the same sign at the order; the depth and
the margin of anything cheaper are `offer-design`'s). *Temporary, not using it:* a pause with a length
and a resume date. On Google Play users "can choose to pause their subscription for a period of time
between one week and three months, depending on the recurring period", the pause "takes effect only
after the current billing period ends", and "while the subscription is paused, the user doesn't have
access to the subscription, and they don't
pay the renewal price". On Stripe, pausing payment collection keeps the subscription `active` while
"Stripe doesn't collect payment" and "your customer retains access", with `resumes_at` for the date and
the invoices of the paused periods kept as drafts, marked uncollectible or voided. Chargebee pauses
"Immediately", at "End of Term" or on a scheduled date, and resumes on a date or "indefinitely"; Paddle
schedules the pause "at the start of the next billing period". *A missing feature, a bad experience:* no
alternative; the reason goes to the owner of that part of the experience through `voice-of-customer`'s
closing of the loop. *Switching, other:* no alternative. A plan change and a pause are not a save by
discount: neither lowers the price of a plan, and the person pays the list price of the plan they are on.

**5. Make one offer, only on the reason "price", only after the alternative was declined.** The offer's
form and depth are `offer-design`'s. The rule per person sits here: one retention offer per window of
the offer's own length plus one term at full price; a second exit request inside that window gets the
cancel button and no offer. The one full-price term is a starting point: it holds while the plan's term
length stays the same through the window, so a one-year offer on an annual plan makes a two-year window;
replace it with the observed lag from an offer's end to a second exit request once you hold a year of
them. Write an accepted offer on the person with its end date; it opens a notice
row in `references/term-end-and-notices.md`, step 2: the end of a concessionary price is a
pre-charge notice. Stripe's portal shows "coupons to customers before they cancel their subscriptions";
Paddle offers "a temporary discount" when "customers don't accept a salvage attempt" and applies it to the
subscription.

**6. Set the effective date and confirm.** The default is the end of the paid term with access kept: on
Stripe, "after canceling, customers can still renew subscriptions until the billing period ends"; on
Google Play, access holds "until the end of the current billing cycle". One button restores the
subscription before the date (Google: "a restored subscription continues to renew as if it were not
canceled"). An immediate cancellation with a refund applies where a cooling-off right exists (the
European and United Kingdom distance-contract rights were not opened here and are left to you; the
United Kingdom's DMCC regime, once in force, adds a renewal cooling-off period) or where your policy says
so. The confirmation is a row of `transactional-messaging`: what was canceled, the effective date, what
happens to the person's data, how to come back. Germany's § 312k requires the confirmation immediately,
in text form, with the date and time of receipt and the end date. The same row confirms a cancellation the
assignee took.

**7. Treat a pause as a term.** A pause has a length and a resume date; the resume is a charge, so it
takes the timer on the charge event (`references/term-end-and-notices.md`, step 5) and a notice before
the charge: as a starting point, the same window as before the end of a trial; that holds for pauses
longer than one billing cycle; replace it once you can read the share of resumes that opened a recovery
case. A pause with no resume date is a silent object for `program-audit-and-ops`. A resume whose charge
fails opens a recovery case of class "resume" (`references/failed-charge-recovery.md`, edge cases).

**8. Hand the person over after the effective date.** From that date the person is gone with the reason
code; service rows end with the access; marketing sends follow the consent record
(`consent-and-preferences`: in Canada the existing business relationship runs two years from the last
purchase, lease or written contract, and a win-back goes only on a live basis and by the person's
instructions); the one finite attempt to bring the person back is `lapse-and-winback`'s, with the
reason code on its entry.

## Thresholds and timings

| Quantity | Value | Class |
|---|---|---|
| A voicemail asking to cancel | processed, or the person called back, within one business day | 2, California § 17602(c)(2)(B) |
| Online cancellation | "exclusively online, at will", by button or by an email that needs no further information; authentication allowed | 2, California § 17602(d) |
| The button beside an offer | "click to cancel", continuously and proximately displayed | 2, California § 17602(e)(2) |
| The button in Germany | two clicks through a confirmation page; confirmation immediately in text form | 2, BGB § 312k |
| Pause on Google Play | one week to three months by recurring period, from the end of the billing period | 2, Google |
| Access after cancellation | to the end of the paid cycle; restore before the date | 2, Google; Stripe, product behavior |
| The offer window per person | the offer's length plus one term at full price, until the observed lag from an offer's end to a second exit request replaces the extra term | 5 |
| Notice before a resume after a pause | the trial-end window, until the share of resumes opening a recovery case replaces it | 5 |
| The assignee's promised reply time | yours, written on the request, with a timer | 4, `chat-and-bots` |

## Edge cases

- **Canceled and subscribed again before the effective date.** A plan change, not a departure: the
  request closes as "kept, plan change" when a new subscription to the same product started before the
  effective date. After a cancellation effective at once (a block at the bank, a dispute, a cooling-off
  cancellation) that date has passed, so a new subscription, even on the same day, is a return written
  on the person.
- **The discount seeker.** A second exit request inside the offer window gets the cancel button and no
  offer; the window's end date stands on the person.
- **An exit request during a recovery case.** The case closes by decision; the unpaid term is your
  policy's.
- **An email "cancel me" with no account details.** The assignee identifies the person by the sending
  address and processes it; where the address matches no account, the assignee asks for the one detail
  that finds it, and nothing more. California's online route is a different email: a button or "an
  immediately accessible termination email formatted and provided by the business that a consumer can
  send to the business without additional information", which the business builds so that it already
  names the account.
- **A cancellation in the store while a save screen exists in the app.** The store's screen does not
  call your flow; your screen serves the subscriptions you charge.
- **A written notice of non-renewal on a contract paid by card.** Not an exit request: on a contract
  with an account manager it decides `b2b-retention`'s renewal case. Record its effective date in the
  term register and count it as an exit decided outside the program (`term-end-and-notices.md`, edge
  cases).
- **A cooling-off cancellation.** A full or proportionate refund by the regime; the request closes as
  canceled, effective now, reason "cooling-off".

## Failure modes

**Obstruction.** The sign: the share kept on the screen rises while cancellations through the assignee,
the bank and disputes rise with it, abandoned screens rise, and people who pressed "keep my plan" come
back through another door before the next term ends; at the following term the people kept
leave.

**An offer to everyone.** The sign: the share kept by offer grows and the second exit request arrives at
the offer's end.

**A pause that never resumes.** The sign: pauses without a resume date; resumes that ended in a case with
no message.

**The assignee's silence.** The sign: the person's second message, or a dispute on the charge, after
"cancel" was written in the conversation; the promised time passed with no closing entry.

**A reason list of your own.** The sign: the screen's list does not match the themes of
`voice-of-customer`; the owner of the part of the experience receives no reasons.

**Sources for the rules in this file, each opened 2026-09-15.** The addresses stand in `SKILL.md`:
California § 17602; BGB § 312k; Google Play, Subscription lifecycle; Stripe, Configure the customer
portal, and Pause payment collection; Chargebee, Pause subscription; Paddle, Retain, Cancellation flows;
J.P. Morgan Payments, Authorization retry logic (code 21).
