---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The recovery case: a charge that failed

The unit here is **the recovery case**: opened by a declined charge for a term, or by the store's
notification of a failed renewal, and closed by a payment, by the end of the retry window, or by the
person's decision. The payment platform runs the retries; the program runs the messages and the access
decision; the app store, where it bills, runs both and only reports. This file decides what a decline
means, how long the case lives, what the person keeps while it lives, what they are told and when, and
what the record says when it closes.

## Entry conditions

A charge for a term returned a decline, on a card or a direct debit, other than a block at the bank on
the term's first decline (step 1); or the store reported a failed renewal (Apple's DID_FAIL_TO_RENEW,
Google's SUBSCRIPTION_IN_GRACE_PERIOD or SUBSCRIPTION_ON_HOLD). The
first charge after a trial is an entry too, in the class "first charge". The term is registered and its
notices went out (`references/term-end-and-notices.md`).

## Exit conditions

The case closes as one of: paid, with the route (updated by the network, retry N with no message, card
updated after message N, paid by hand); ended without decision, on the deadline; closed by the person's
decision (a cancellation, a dispute, a block at the bank), which hands the case to
`references/exit-and-save.md`. Recorded with it: the decline class, the deadline, the access history, the
number of messages, the days without payment.

## Steps

**1. Classify the decline before any retry and before any message.** Five classes, read from the code
the issuer returned.

- *Hard:* the issuer will never approve. Visa's Category 1, "Issuer will never approve", where "the
  merchant is not permitted to reattempt the transaction", and response code 14, after which "Merchants
  must not reattempt any transaction using the same account number"; Mastercard's advice code 03, "Do not
  try again. Obtain another type of payment from consumer."; on Stripe the hard decline codes
  `incorrect_number`, `lost_card`, `pickup_card`, `stolen_card`, `highest_risk_level` and
  `transaction_not_allowed`. No retry runs; a new payment method is needed; the message goes now.
- *Soft:* the issuer cannot approve at this time. Visa's Category 2, with reattempts allowed "up to 15
  times in 30 days"; Mastercard's codes 24 to 30, "Retry after 1 hour" through "Retry after 10 days",
  where the issuer sets the interval. Retries run on the schedule; the message follows step 4.
- *Stopped at the bank:* the person told their bank to stop the recurring charge. Mastercard's code 21,
  "Do not try again. Issuer has blocked recurring payment transaction"; on Stripe
  `revocation_of_authorization` and `revocation_of_all_authorizations`. No retry either way. On the
  term's first decline it opens no recovery case: it is an exit request with the source "bank", decided
  outside the program (`references/exit-and-save.md`, step 1). Inside a recovery case already open, it
  closes the case by the person's decision.
- *Authentication required:* the bank wants the person to confirm (3-D Secure; on Stripe the decline
  code `authentication_required`, or a payment that `requires_action`). A retry does not help; the person
  has to act, on the same card. The message carries the confirmation link, not a request for a new card,
  and reminders follow until the person confirms or the case ends.
- *New card available:* the network holds a replacement. Mastercard's code 01, "New account information
  available"; on Stripe the event `payment_method.automatically_updated`. The network's update comes
  first and the retry follows it; the person is not asked until an update fails to arrive.

Stripe lists nine hard decline codes and retries none of them until a new payment method arrives: "the
payment only executes if you obtain a new payment method". Read the list for whether a retry runs and
the class for what the person hears. Two of the nine are a block at the bank and one is a request to
authenticate, and a "new card needed" message on those asks for a card from a person who stopped the
charge or only has to confirm it.

An app store returns no classes: it reports "in billing retry" and "in grace period", and those states
are what you read.

**2. Set the case deadline from the term and the network rules.** The ceilings come from outside: Visa,
at most 15 reattempts in 30 days on Category 2; Mastercard, the "retry after" interval in the code;
Stripe's Smart Retries, "a specific number of times within a time period: 1 week, 2 weeks, 3 weeks, 1
month, or 2 months", with "8 tries within 2 weeks" as the recommended default and a custom schedule of "up
to three retries"; Chargebee, "up to 4 attempts" with an interval of up to 45 days between them; direct
debits on Stripe, retried only for "Insufficient funds", ACH twice within 40 days, SEPA, Bacs and
Australian BECS twice within 30 days, ACSS and New Zealand BECS once within 30 days, each under its
mandate; Apple, a billing retry state where the store "attempts to collect payment for up to 60 days";
Google, a grace period followed by an account hold whose default length is "60 days minus any grace
period duration", with "additional attempts to charge the payment method for up to 48 hours" before the
hold. The deadline is the end of the retry window; write it into the case on the day the case opens:
before it the subscription is in recovery, after it the case is ended without decision. On a store the
window is the store's: Apple's 60 days, and Google's default 60 days of grace and hold together, run past
the next end date of a monthly plan, and the deadline is theirs. On your own platform, choose the window
(a parameter of yours) no longer than the term: a window that runs past the next end date puts that
term's invoice inside the open case, since on Stripe a `past_due` subscription "continues to create
invoices". The window is not the access you give without payment. That is the grace of step 3; after the
grace the window runs with access restricted or closed, and its price is every day on which a
subscription that neither pays nor is served still counts as live (`SKILL.md`, the first seam).

**3. Give each stage of the case an access class, and cap the grace at the term.** Three classes.
*Full:* the grace period. Apple's Billing Grace Period is 3, 16 or 28 days, and 3 or 6 days on a weekly
subscription, and "if you choose to enable Billing Grace Period, ensure that you provide full service for
the subscription throughout the grace period"; on Google, "during a grace period, the user should still
have access to their subscription entitlement"; on Stripe a `past_due` subscription keeps whatever access
you give it. *Restricted:* read-only, export, no new work. *Closed:* Google's account hold, where "you
should block access to the subscription entitlement"; Stripe's `unpaid`, where you "revoke access to
your product". Each stage carries its class and the date it changes; a change of access is an event of
the service row. A payment inside the grace period leaves the billing cycle where it was (Apple: no
interruption "to the subscriber's days of paid service" if recovered "within the grace period"). On
Apple and Google a payment after the grace period but inside the window starts a new cycle on the
recovery date; on another platform the cycle follows its own setting. The grace does not outlast the
term: Apple cuts a 16 or 28 day grace to 6 days on a weekly subscription "to ensure it isn't longer than
the subscription itself", and the same ceiling holds for you.

**4. Time the messages to the retry schedule, not to the calendar.** The class of every message is a
service row: an exception fired by a state change in `transactional-messaging`; a row a withdrawal does
not stop in `consent-and-preferences`; a utility template with no offer inside in `messaging-channels`;
a mandatory notice in `contact-orchestration`, never suppressed and counted against the cap, since that
skill exempts only what the person is waiting for. The order: (a) at the decline, when the class needs
the person (hard, authentication required), the message goes at once
with the link to update the payment method and the date access changes; when the class is soft, the first
retry runs in silence and the message follows the first failed retry; (b) before the last retry, with
the deadline; (c) at every change of access class; (d) on the deadline, a closing message with the way
back, which is a new subscription and not "pay the old invoice" where the platform has closed the
subscription (on Stripe `canceled` "is a terminal state that can't be updated"). Every message names the
date of the next retry and the date access changes, and every date it names starts a timer. Silent
retries produce no messages. The link to the payment page lives as long as the case: on Stripe the
hosted link stops working when the status changes to `unpaid` or `canceled` and when "the subscription's
current renewal period expired". For a store-billed subscription the message goes inside the product with
a deep link to the store's payment page (Apple's Manage Payments page; on Google, in-app messaging for
payment issues "is shown during grace period and account hold once per day"): an email that says "update
your card with us" to a person whose payment the store holds is a routing error.

**5. Retry at once after the person acts, and confirm.** Charge a card updated after a failed charge without
waiting for the schedule. Chargebee can "immediately try to charge the card" on a card update. Stripe's
page says only that after a hard decline scheduled retries "only execute after detecting a new payment
method", not that they run at once, so on Stripe charge the open invoice yourself when the update
arrives. Charge a confirmed authentication the same way. The result goes back as a confirmation: paid,
or declined again
with its class. A person who updated a card and heard nothing asks "did it work?" by entering the card a
second time or by writing to support; count both beside the inquiries, since the question was asked
without words.

**6. Close on the deadline.** The case closes as ended without decision; access closes; the subscription
takes the platform's end state (on Stripe, after the final retry, "cancel the subscription", "mark the
subscription as unpaid" or "leave the subscription past-due"; take the first or the second, because an
open case with no end breaks every retention denominator). The record on the person: gone, reason
"payment", date the deadline. The person goes to `lapse-and-winback` with the reason code "payment", and
the first message of that attempt is the way back, with the payment method fixed, not an offer. A payment
after the deadline (on Stripe, paying the most recent invoice returns the subscription to `active`
"regardless of whether the payment is done before or after the latest invoice due date"; on Google, "when
a subscription recovers from account hold, the renewal date resets") starts a new term on the recovery
date; the case does not reopen, and "returned" is written on the person.

**7. Run the four billing methods apart.** *Card:* steps 1 to 6 in full. *Direct debit:* retries only for
insufficient funds, under the mandate, in the window of the debit type; cases of class "debit". *Store:*
the store runs the retries and the grace period; you set the grace length in its console and send the
in-product message; cases of class "store", closed on the store's notifications (Apple's DID_RECOVER and
EXPIRED, Google's SUBSCRIPTION_RECOVERED and SUBSCRIPTION_CANCELED). *Invoice:* `b2b-retention`. Wallets
and buy-now-pay-later providers follow their own rules and are left to you.

**8. Close the case with a record.** The outcome; the route where it paid (network update; retry N
with no message; card updated after message N; by hand); days without payment; whether access was
interrupted; the number of messages. The control metric in `SKILL.md` and the lines beside it come from
this record and from nothing else.

## Thresholds and timings

| Quantity | Value | Class |
|---|---|---|
| Retries on Visa Category 1, response code 14, Mastercard codes 03 and 21 | none | 2, Visa AI10325; Mastercard codes as rendered by J.P. Morgan Payments |
| Retries on Visa Category 2 | at most 15 in 30 days | 2, Visa AI10325 |
| Mastercard retry intervals | codes 24 to 30: after 1 hour, 24 hours, 2, 4, 6, 8, 10 days | 2, as rendered by J.P. Morgan Payments |
| Smart Retries | a window of 1 week to 2 months; recommended 8 tries in 2 weeks; custom schedule up to 3 retries | 2, Stripe, product behavior |
| Direct debit retries on Stripe | ACH 2 in 40 days; SEPA, Bacs, AU BECS 2 in 30 days; ACSS, NZ BECS 1 in 30 days; insufficient funds only | 2, Stripe, product behavior |
| Chargebee dunning | up to 4 attempts, interval up to 45 days | 2, Chargebee, product behavior |
| Apple Billing Grace Period | 3, 16 or 28 days; 3 or 6 on weekly subscriptions | 2, Apple |
| Apple billing retry | up to 60 days | 2, Apple |
| Google grace period and account hold | 60 days together by default; up to 48 hours of extra charge attempts before the hold | 2, Google |
| Stripe hosted payment link | invalid 30 days after the trial ending email, on `unpaid` or `canceled`, and when the renewal period expires | 2, Stripe, product behavior |
| Case deadline | the end of the retry window, written on the day the case opens | construction |
| Retry window on your own platform | no longer than the term; the access given without payment is the grace, not the window | 4 |
| Silent retries before the first message on a soft decline | one | construction |

## Edge cases

- **The person cancels while the case is open.** The case closes by the person's decision, not by the
  deadline; an exit request opens with the source "screen" or "message"; the unpaid term is a matter of
  your policy.
- **A dispute during the case.** As "stopped at the bank": no retries, the case closes by decision, an
  exit request of class "dispute" opens.
- **A contract with an account manager, paid by card.** The case runs here, on a split term
  (`term-end-and-notices.md`, edge cases). Its deadline is no shorter than the contract's cure period, read
  from `b2b-retention`'s contract register, and access changes, and the case closes on its deadline, only
  with the notice the contract requires: a suspension without that notice breaches the contract. A written
  notice of non-renewal that arrives while the case is open decides the renewal case at `b2b-retention`,
  and the case closes by that decision.
- **The new card is declined too.** The same case, a new decline class, the deadline unchanged.
- **A payment after the deadline.** Step 6: a new term, the case stays closed, "returned" on the person.
- **A weekly plan in a store with your grace set to 28 days.** The store cuts it to 6; your access timer
  follows the store's notification, not your setting.
- **A resume after a pause that fails.** Google moves the subscription "into account hold directly when
  the subscription resumes from a paused state with a failed form of payment", with no grace period; a
  case of class "resume", messaged as a hard decline.

## Failure modes

**Retries on a hard decline.** The sign: repeated retries with the same code in the log; a network fee
for excessive reattempts on the acquirer's statement.

**A request for a card the network already replaced.** The sign: the update event precedes the message;
the person answers "I changed nothing".

**Past due forever.** The sign: the share of `past_due` inside "active" grows while revenue per active
subscription falls; cases with no deadline.

**A message to the wrong payer.** The sign: "update your card" emails to people whose payment the store
holds; the link leads to an empty page.

**A case with no messages.** The sign: cases closed on the deadline with zero messages. The row's route is
down, which `program-audit-and-ops` reads as the row's heartbeat (`transactional-messaging`).

**Sources for the rules in this file, each opened 2026-09-15.** The addresses stand in `SKILL.md`: Visa
article AI10325; J.P. Morgan Payments, Authorization retry logic; Stripe, Automate payment retries, How
subscriptions work, Automate customer emails, and How cards work; Chargebee, Dunning; Apple, Enable
Billing Grace Period, and Reducing involuntary subscriber churn; Google Play, Subscriptions, and
Subscription lifecycle.
