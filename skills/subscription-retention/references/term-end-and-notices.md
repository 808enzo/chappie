---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The term and its notices

The unit here is **the term**: one billing period of one subscription, with its start, its end date, its
price, and what falls due at the end. The billing system writes the events of a term; the program writes
the notices; the law and the card networks set what the notices say and when they go. This file decides
what has to happen before a term ends, and what the record says afterward.

## Entry conditions

A live subscription with an end date; or a trial or promotional period with a conversion date; or a
price or terms change scheduled for a subscription. The subscription is paid and charged to a card, a
direct debit or an app store: a contract billed by invoice belongs to `b2b-retention`. The confirmation at
signup has already gone as a row of `transactional-messaging`, the confirmation of a distance contract,
and Visa's rule that an electronic copy of the terms goes out at enrollment "even if no amount was due at
the time" is met there.

## Exit conditions

For every term: its class; a notice calendar derived from the class, with what each notice says and
when it goes; a timer on the charge event at the end date; and the term's outcome recorded as one of:
renewed on the date; renewed through recovery on the recovery date; canceled with an effective date;
ended without decision; paused; ended on a price not accepted.

## Steps

**1. Register the term.** Per subscription: start and end of the term, price, term length, billing
method (card, direct debit, Apple or Google store, invoice), and the class of the term: a trial converting
to paid; a promotional price converting to the full price; a term of one year or longer; a short term (a
month, a week); a price or terms change scheduled. Beside it, the person's regime: the country, and
whether the person is a consumer or an organization (the ten questions in `consent-and-preferences`; an
organization with a contract billed by invoice goes to `b2b-retention`, an organization paying by card
stays here, and a contract with an account manager paid by card is a split term, in the edge cases).
Counted by end date and class, the register is also the renewal calendar: the weeks in which notices,
charges and recovery cases will crowd. A promotion placed near those weeks is `promo-calendar`'s.

**2. Build the notice calendar from the class.** Every notice is a row of the service register in
`transactional-messaging`, marked "required by law or by the network", with its own deadline. Where two
regimes apply, one notice serves both only if it goes inside every window, after the latest "at least"
and before the earliest "at most", and carries every list of contents; where the windows do not meet,
send two. California settles its own overlap: an offer that needs both its trial notice and its annual
notice needs "only the notice specified in paragraph (2)", the annual one.

- *The end of a trial or a promotional period.* Visa requires "an electronic reminder notification
  (i.e., email or SMS / text) a link to online cancellation at least seven (7) days before initiating a
  recurring transaction if" the trial or promotional period "has expired" or "the nature of the recurring
  agreement has changed (for example, the price or billing period)". California requires, for a trial or
  a promotional price that applied for more than 31 days, a notice "at least 3 days before and at most 21
  days before the expiration" of that period. Stripe, as one platform, sends a trial ending reminder "7
  days before a free trial ends". The content follows California's list: that the service "will
  automatically renew unless the consumer cancels", "the length and any additional terms of the renewal
  period", "the amount or range of costs" and the frequency, "one or more methods by which a consumer can
  cancel", a link "that directs the consumer to the cancellation process" when the notice is electronic,
  and contact information.
- *A term of one year or longer.* California: "at least 15 days and not more than 45 days before" the
  renewal. The United Kingdom, once Part 4 Chapter 2 of the DMCC Act 2024 is in force: a reminder notice
  "in respect of each renewal payment that relates to the end of a relevant six-month period", with
  contents and timing to come from regulations that did not exist on the day this was written. Germany:
  standard terms may extend a contract tacitly only for an indefinite period, with a right to terminate
  at any time on at most one month's notice (BGB § 309 no. 9, our rendering), so an annual term there does
  not roll into another year. Section 309 sets no notice before the end; a notice you send says what the
  contract becomes.
- *A price or terms change.* California: notice of a fee change "no less than 7 days and no more than 30
  days before the fee change takes effect", with "information regarding how to cancel", and notice of any
  material change with the same information. Apple, for store-billed subscriptions, runs the notice
  itself: subscribers "must consent to the price increase before their next renewal date" when the
  increase "is more than 50% of the current price and the difference in price exceeds approximately US$5
  per period for non-annual subscriptions, or US$50 per year for annual subscriptions", when "the
  subscriber is located in a region that requires consent for any price changes", or when "the subscriber
  experienced a price increase for that subscription within the past 12 months"; otherwise Apple notifies
  without consent; the minimum notice is "7 days for weekly subscriptions, 27 days for 1 month
  subscriptions, and 30 days for subscription durations longer than 1 month", and Apple's first email
  goes 7 days before the renewal on a weekly subscription, 27 days on a monthly one, and 60 days on
  2-month, 3-month, 6-month and annual ones.
- *The annual reminder.* California, for an annual agreement: a reminder each year "in the same medium
  that resulted in the activation" or the medium the customer is accustomed to, disclosing the product,
  "the frequency and amount of charges" and "the means to cancel".
- *The end of a retention discount.* It is the end of a promotional price and takes the trial-end row:
  California's 3 to 21 days where the promotional price applied for more than 31 days, Visa's seven days
  for a changed agreement. The exit mechanic opens the row when it records an accepted offer
  (`references/exit-and-save.md`, step 5).
- *A resume after a pause.* No rule opened here names it. The library gives it the trial-end window as a
  starting point, and the exit mechanic opens the row when it records the pause
  (`references/exit-and-save.md`, step 7).

**3. A notice carries no offer.** "Renew at a discount" inside a pre-charge notice turns the row into
marketing three times over: with the law (`transactional-messaging` loses the service class), with the
messaging platform's gatekeeper (`messaging-channels`: a utility template with an offer is recategorized
as marketing), and with the consent record (`consent-and-preferences`: a withdrawal now stops it, and the
person renews without notice). The offer goes as its own message on its own basis; a "renew early and
save" campaign is `promo-calendar`'s and `offer-design`'s.

**4. Handle the card that expires inside the term before the charge.** Two things run ahead of the end
date. The network's automatic update: Stripe "works with card networks and automatically attempts to
update saved card details whenever a customer receives a new card (for example, replacing an expired card
or one that was reported lost or stolen)", "widely supported in the United States" with international
support that "varies from country to country", and "it isn't possible to identify cards that support
automatic updates". And the expiring card notice: Stripe sends one "1 month before your customer's card on
file expires". Order them: the network first, the person second; the request to the person goes when the
card expires before the end date and no update has arrived. A card fixed before the charge opens no
recovery case, and the term renews on its date.

**5. Set the timer on the charge event.** On the end date the billing system has to produce one of four
events: paid, declined, canceled, paused. The event is what the record reads; a date with no event is not
"active". Take the collection window from the platform's documentation, or, where the platform states
none, set a duty threshold: as a starting point, one billing cycle of the platform's invoicing; that
holds for cards and direct debits, not for invoices sent by hand; replace it with the observed lag from
end date to event once you hold two cycles of it. A term past the window with no event is a "no event"
term, a silent object for `program-audit-and-ops`: a billing job that died, a webhook that stopped, a
store notification pipeline that broke. A store-billed term produces its event as a notification, and any
of these counts: Apple's DID_RENEW, DID_FAIL_TO_RENEW and EXPIRED; Google's SUBSCRIPTION_RENEWED,
SUBSCRIPTION_IN_GRACE_PERIOD, SUBSCRIPTION_ON_HOLD, SUBSCRIPTION_PAUSED and SUBSCRIPTION_EXPIRED. Watch
fewer than the store's end states, and a paused or expired term reads as silent.

**6. Record the outcome on the term.** Renewed on the date. Renewed through recovery: on Apple and
Google, a recovery inside the grace period leaves the billing cycle where it was, and a recovery after the
grace period but inside the retry window starts a new cycle on the recovery date (Apple: "the new
billing date is established on the date of recovery"; Google: "the billing date moves to the date of
recovery"), so the next term's start moves. The subscription stays in its cohort in `crm-reporting`: the
cohort's entry event is the subscription's start, and a recovery moves a term, not that event. Canceled,
with the effective date from the exit mechanic. Ended without decision, on the deadline of the recovery
case. Paused, with the resume date. Ended on a price not accepted, from step 8.

**7. Treat the trial's first charge as its own class.** A trial that ends without a payment method opens
no recovery case where the platform stops billing: on Stripe a subscription is `paused` when it "has
ended its trial period without a default payment method" and the trial settings say `pause`, and Stripe
then states: "Invoices are no longer created for the subscription." Under any other setting, read what
the platform does at the trial's end before concluding that no case opens. Converting that person is
`welcome-and-activation`'s work; this file only sends the notice of step 2 and records the outcome. A
trial with a card on file ends in a first charge; its decline opens a recovery case of class "first
charge" in `references/failed-charge-recovery.md`, read on its own line, because the person entered the
card for the trial and no charge has succeeded on it yet.

**8. Open a price consent as an exit request.** Where consent to the new price is required, the store
asks, and Apple's page puts silence and refusal in one sentence: "If a subscriber doesn't agree to the
new price or takes no action, Apple will continue to request consent approximately weekly through email,
push notifications, and in-app messaging until their subscription expires at the end of their current
billing cycle." Open an exit request with the source "price consent" on the day the store's first
request goes, not on the day the subscription expires: opened at expiry, the class would hold only the
people who never consented. It closes as kept when the person consents, as canceled when the person
cancels meanwhile, and as ended on a price not accepted when the cycle ends without consent. No screen
and no offer: an offer at this point is a way around the consent.

## Thresholds and timings

| Quantity | Value | Class |
|---|---|---|
| Reminder before the first charge after a trial, a promotion or a changed agreement | at least 7 days, electronic, with a link to online cancellation | 2, Visa AI09067 |
| Notice before the end of a trial or promotional price that applied for more than 31 days | 3 to 21 days before | 2, California § 17602(b)(1) |
| Notice before the renewal of a term of one year or longer | 15 to 45 days before | 2, California § 17602(b)(2) |
| Notice of a fee change | 7 to 30 days before it takes effect | 2, California § 17602(g)(2) |
| Annual reminder | once a year, in the same medium | 2, California § 17602(h) |
| Retention of consent verification | at least three years, or one year after termination, whichever is longer | 2, California § 17602(a)(6) |
| Applicability of the AB 2863 amendments | contracts entered into, amended or extended on or after July 1, 2025 | 2, California § 17601(b) |
| Initial term and tacit extension in Germany | at most two years; extension only indefinite with a notice period of at most one month | 2, BGB § 309 no. 9 |
| Reminder notice in the United Kingdom | per renewal payment relating to the end of a relevant six-month period | 2, DMCC Act 2024 s. 258, not in force on 2026-09-15 |
| Consent to a price increase on Apple | over 50% and over about US$5 per period or US$50 per year; a region requiring consent; a second increase within 12 months | 2, Apple |
| Minimum notice of a price change on Apple | 7 days weekly, 27 monthly, 30 longer; first email 7 days before on weekly, 27 on monthly, 60 on 2-month to annual | 2, Apple |
| Expiring card notice | 1 month before expiry | 2, Stripe, product behavior |
| Trial ending reminder | 7 days before | 2, Stripe, product behavior |
| Collection window for the charge event | one billing cycle of the platform's invoicing, until two cycles of observed lag replace it | 5 |

## Edge cases

- **An annual plan bought through a store.** The store sends the price notices and consent requests; you
  send none of those. You keep the timer on the store's notifications, and whether your own annual
  reminder is still owed where a statute requires one is a question for counsel.
- **A plan change inside the term.** Proration by the platform's setting, with or without a reset of the
  term; a notice of changed terms goes when the next term's price changes.
- **A subscription with a commitment period.** On Google Play a user-initiated cancellation "takes effect
  at the end of the current commitment period"; the term is the commitment period, not the payment.
- **An organization paying by card.** Consumer law does not reach it; the network rules do, since they
  bind the merchant. Without a signed contract and an account manager, the whole term is yours. With
  both, the term is split: the charge, the notices before it and the recovery case stay here, because the
  billing method assigns the charge; the decision point and the renewal case are `b2b-retention`'s,
  because the contract assigns the decision. Both registers carry the contract's identifier. Hold two
  conditions on the split. The recovery case gets a deadline no shorter than the contract's cure period,
  and it changes access or closes only with the notice the contract requires, since a suspension without
  that notice breaches the contract (`failed-charge-recovery.md`, edge cases). A written notice of
  non-renewal is the decision of the neighbor's renewal case and opens no exit request here: write its
  effective date into the term register, charge no term after that date, and count the notice as an exit
  decided outside the program. The signs of a broken split: access closed on the recovery case's deadline
  before the cure period ends; a charge after the effective date of a notice; one notice that opens a
  recovery case and an exit request here and a renewal case at the neighbor. The remedy: take the deadline
  from the contract register, write the effective date into the term register, and let the notice decide
  the renewal case, whose decision closes any open recovery case.

## Failure modes

**The charge went through with no notice.** The sign: refund requests and "cancelled recurring" disputes
concentrated in the days after annual renewals. Visa widened issuers' dispute rights for purchases made
"through a trial period" where "the cardholder was not clearly advised of further billing after the
purchase date".

**The term ended in silence.** The sign: the count of active subscriptions holds while revenue for the
period falls; "no event" terms accumulate on one billing method. A billing job or a webhook is down.

**The notice became marketing.** The sign: people who withdrew marketing consent got no notice and renewed
without one; a utility template was recategorized (`messaging-channels`).

**Sources for the rules in this file, each opened 2026-09-15.** The addresses stand in `SKILL.md`:
California §§ 17601 and 17602; Visa article AI09067; BGB § 309; DMCC Act 2024 s. 258 and the government
response of April 2, 2026; Apple, Manage pricing for auto-renewable subscriptions, and Reducing
involuntary subscriber churn; Google Play, Subscription lifecycle; Stripe, Automate customer emails, How
cards work, and How subscriptions work.
