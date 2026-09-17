---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Vocabulary for subscription-retention

The terms all three mechanics assume. The last section lists the words this skill shares with its
neighbors, several of them under other meanings.

## The units

**Term.** One billing period of one subscription: its start, its end date, its price, its length, and
what falls due at the end (a charge, a trial's conversion, a price change). The unit of the term mechanic.
The billing system writes its events; the program writes its notices.

**Recovery case.** Opened by a declined charge for a term, or by the store's notification of a failed
renewal; closed by a payment, by the deadline, or by the person's decision. The unit of the recovery
mechanic. It carries a decline class, a deadline written on the day it opens, an access history, and a
count of messages.

**Exit request.** The person's expressed intent to stop, from whichever door: the cancel screen, a
message, the store, the bank, a dispute; or the store's request for consent to a higher price, without
which the subscription stops. The unit of the exit mechanic. It closes as kept, canceled or abandoned,
and a price consent can also close as ended on a price not accepted.

## The term

**Term class.** What the end of the term is: a trial converting to paid; a promotional price converting
to the full price; a term of one year or longer; a short term; a price or terms change scheduled. The
notice calendar follows from it.

**Notice calendar.** The notices a term owes and their deadlines, taken from the class and from the
regimes that apply: the pre-charge notice before a trial or promotional price ends, the notice before an
annual renewal, the notice of a price change, the annual reminder, the notice before a retention discount
ends, each a row of the service register marked "required by law or by the network". The notice before
a resume after a pause is a row of the same register by the library's rule, since no law or network rule
opened here names it.

**Pre-charge notice.** The notice that a charge is coming: what renews, for how long, at what amount and
frequency, on which date, and how to cancel, with a link to the cancellation where the notice is
electronic. It carries no offer.

**Charge event timer.** The timer set on the end date: the billing system has to produce paid, declined,
canceled or paused inside the platform's collection window. A term past the window with no event is a
**"no event" term**, a silent object for `program-audit-and-ops`, and it is not "active".

**Term outcome.** One of: renewed on the date; renewed through recovery, on the recovery date; canceled
with an effective date; ended without decision; paused; ended on a price not accepted.

## The recovery case

**Decline.** The issuer's refusal of a charge, returned as a code. Read into one of five classes before
any retry or message: **hard** (the issuer will never approve; no retry; a new payment method is
needed), **soft** (the issuer cannot approve now; retries run), **stopped at the bank** (the person
blocked the recurring charge at their bank; on a term's first decline an exit request decided outside
the program, not a case; inside an open case, that case's close by decision), **authentication
required** (the person has to confirm on the same card; a retry does not help), **new card available**
(the network holds a replacement; the update comes before the person is asked).

**Retry.** A repeated charge request for the same term. The platforms count it as `attempt_count`;
this library keeps "attempt" for `lapse-and-winback`.

**Retry window.** The span in which retries may run. On a store it is the store's. On your own platform
it is bounded by the card network's ceiling, the platform's schedule and the term's length, so that the
next term's invoice does not fall inside an open case. It is not the access given without payment: that
is the grace.

**Deadline.** The end of the retry window, written into the case on the day it opens. Before it the
subscription is in recovery; on it, with no payment and no word from the person, the case is ended
without decision, and the deadline is the departure date.

**Account updater.** The card networks' service that replaces a stored card's details when the issuer
reissues the card. Runs before the person is asked; its success is the network's work, read beside the
control metric as a payment route.

**Access class.** What the person keeps at a stage of the case: **full** (the grace period), **restricted**
(read-only, export, no new work), **closed**. Each stage carries its class and the date it changes.

**Grace.** The stage of full access without payment while retries run. Apple's and Google's term. Not
longer than the term. Stripe uses "grace period" loosely for a pause of payment collection; that use is
not this one.

**In recovery.** The state of a live subscription with an open recovery case; the platforms call it
`past_due` or "in billing retry". It has a ceiling, the deadline, and inside it the subscription counts
as live for every retention denominator. Read the count in recovery on the end date, by access class,
beside retention: a longer window raises retention by construction.

**Ended without decision.** The close of a recovery case on the deadline with no payment and no word from
the person. The involuntary ending as this library defines it. Its date is the deadline, never the first
decline.

**Payment route.** How a case that paid got there: updated by the network; a retry with no message; the
card updated after message N; paid by hand.

## The exit request

**Source.** The door the request came through: screen, message, store, bank, dispute, price consent.
Each source has an owner of the stage and a script.

**Ownership class.** Who writes on a stage of the request: the program alone; the assignee working from
the program's script; the store alone, with the program reading. A stage with no class has no right to
send, and its silence is read as a miss.

**Reason.** The person's stated cause, chosen once from entries of the theme list `voice-of-customer`
keeps by identifier. A subscription needs at least: price; not using it; a missing feature; switching;
temporary; a bad experience; other or no answer.

**Alternative.** The one thing offered per reason before any offer: a cheaper plan on price; a pause on
temporary or not using it; nothing on the others. Neither lowers the price of a plan: the person pays the
list price of the plan they are on.

**Retention offer.** The one discount, made only on the reason "price" and only after the alternative
was declined. Its depth is `offer-design`'s. Its **window** per person is the offer's length plus one term
at full price; a second exit request inside the window gets no offer.

**Pause.** The subscription's pause: billing stops and, by platform, access stops, until a resume date.
A pause is a term: the resume is a charge with its timer and its notice. Not the pause of marketing
messages that `consent-and-preferences` records as an instruction.

**Effective date.** The date a cancellation takes effect: by default the end of the paid term, with
access kept until then and one button to restore; earlier where a cooling-off right or your policy gives
a refund.

**Restore.** Reversing a cancellation before its effective date; the subscription continues as if never
canceled.

**Abandoned.** An exit request opened with no decision recorded: the screen closed mid-flow; a message
whose promised reply time passed with no closing entry. Not "kept".

**Kept.** An exit request closed by the person's recorded choice to stay: "keep my plan" pressed on a
screen where the cancel button stands on the same step, a pause with a date, a plan change, an accepted
offer, consent to a new price.

**Ended on a price not accepted.** The close of a price consent when the cycle ends without consent. The
store records refusal and silence as one outcome, so do not read the close as a decision.

**Exit decided outside the program.** A cancellation made in the store, a block placed at the bank, or a
dispute: decided before the program saw it, kept out of the control metric's denominator and read beside
it.

**Cooling-off.** A statutory right to cancel within a set number of days of signing up, or, under some
regimes, of a renewal, with a refund. Its arithmetic is left to the reader.

**The store as payer.** For a subscription bought through Apple's or Google's store, the store holds the
payment method, runs the retries and the grace period, and reports by notification; the program reads,
sets the grace length in the store's console, and messages inside the product.

## Words shared with neighbors

- **attempt**: `lapse-and-winback`'s unit, its one finite try to bring a person back. Not used here; a
  repeated charge is a retry.
- **pause**: `consent-and-preferences` records a pause of marketing as an instruction, and
  `messaging-channels` uses the word for a platform's suspension of a template; here the pause is the
  subscription's. The marketing pause and this one live on the person's record as separate fields.
- **grace**: Apple's and Google's term for full access while retries run, used here in that sense. Stripe
  applies "grace period" to a pause of collection, and in `b2b-lifecycle` grace is the time after an event
  a customer promised, past which a step counts as missed. Neither is this.
- **deadline**: in `transactional-messaging`, the moment by which a row has to arrive; here, the end of a
  recovery case's retry window. A message of the case carries both: its own row deadline, and the case
  deadline it names.
- **kept**: `consent-and-preferences` reads a kept share of instructions that chose a preference over a
  withdrawal; here, an exit request closed by a choice to stay.
- **held / hold**: `contact-orchestration` and `messaging-channels` hold a send; here "account hold" is
  Google's name for the closed-access stage and is quoted as theirs.
- **churn**: `metric-definitions` owns the general forms; here only "ended without decision" as an
  outcome class, and the departure date as the case's close.
- **gone / lapsed**: `lapse-and-winback`; a person becomes gone on the effective date or on the deadline,
  not on the day of the decline.
- **service row, promise**: `transactional-messaging`; the notices of the term and the messages of the
  case are its rows, marked "required by law or by the network".
- **basis record, instruction**: `consent-and-preferences`; referenced only.
- **reason, theme**: `voice-of-customer`; the cancel reason is the same list, by identifier.
- **offer**: `offer-design` owns its content and depth; here its place and its window per person.
- **trial**: `welcome-and-activation` owns the period and the activation; here the trial is a term class
  and its first charge a case class.
- **renewal**: `b2b-retention` owns the renewal of a contract held by an account manager; here the renewal is
  the end of a term charged to a card, a debit or a store. The billing method assigns the charge and the
  contract assigns the decision: a contract with an account manager that is paid by card keeps its term and
  its recovery case here and its decision point and renewal case at the neighbor (the edge case "An
  organization paying by card" in `term-end-and-notices.md`).
- **contract term**: `b2b-retention`'s phrase, always two words, for the period a contract commits both
  parties to; invoices split it into billing periods. A term here is one billing period, and the two are
  not interchangeable.
- **cohort**: `crm-reporting`, by entry event; here the entry event is the subscription's start, and a
  term start moved by a recovery changes no cohort.
- **assignee**: `chat-and-bots`; the person who takes an exit request written in a conversation.
