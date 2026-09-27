---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Vocabulary for b2b-retention

The terms all four mechanics assume. When the customer, the account manager and finance disagree about "the renewal",
check first whether one of them means the end date and another the decision point, or whether one means the account and
another one of its contracts. The last section lists the words this skill shares with its neighbors, several of them under
other meanings.

## What sets this work apart

Three properties set it apart from the rest of the library.

1. **The people who use the product are not the person who decides.** Users work in the product every day. The renewal
   belongs to the economic buyer the account manager met once during the sale, together with procurement and its
   calendar. You read use on people and the decision on the contract. Before the deal, `b2b-lifecycle` keeps the same
   split: the grade on the account, the basis on the person.
2. **The decision date is not the end date.** A contract that renews automatically renews by silence. The last day the
   customer can still refuse falls one notice period before the end, and a renewal conversation after that day decides
   nothing. A renewal calendar built on end dates runs late by the notice period, by construction, so the decision point
   carries a timer from its recorded date instead of waiting for an event.
3. **Three hands on one contract, and one of them is not marketing.** The program writes to the customer's users and to
   roles from an allowed set, the account manager holds the plan and the renewal, and finance holds the invoice and its
   collection. The ownership class of every stage is written before any step, and silence in a stage a person owns reads
   as a miss.

Two words are not used here. "Review" has its senses counted in `crm-program-design` and `program-audit-and-ops`, so the
meeting with the buying group goes by the industry's name, QBR, whatever its cadence. "Owner" is counted too: after the
deal, the salesperson is the account manager, as in `b2b-lifecycle`.

## The units

**Success plan.** The outcomes the customer bought for, taken from the won-deal record and carried as milestones with a
date, a doer and a sign of completion, read with the buying group at QBRs. One per account, with a new version at each
renewal.

**Renewal case.** One contract term on its way to its decision point. It opens on its opening date and closes as decided by
the decision point or in one of the remainder classes. The unit of the control metric.

**Amendment.** A change to the entitlement of a live contract inside its term: seats, usage volume or modules, up or down.

**Collection case.** An invoice under a contract not paid by its payment date. It opens on the next day, carries a ceiling
from the day it opens, and closes as paid, settled, terminated or written off.

## The contract

**Contract register.** One row per contract, written on the day of the signature: the buying unit, the start and end of the
contract term, the renewal class, the notice period and its counting rule, the form and address of notice, the price change
rule and its notice, the entitlement, the invoice schedule and payment terms, the cure period and suspension procedure, the
contractual response time, the governing law, and the billing method.

**Contract term.** The period a contract commits both parties to; invoices can split it into several billing periods.
Always two words here (see "term" in the last section).

**Renewal class.** Automatic renewal for a set term; a new term by signature; evergreen after the initial term.

**Decision point.** The last day the customer still decides: the end date minus the notice period, for an automatic
renewal; the end date, for a contract that needs a signature; the last day of notice before each anniversary with an exit
right, each its own case; through a reseller, the earlier of the customer's last day of notice to the reseller and the
reseller's to you. An evergreen contract has none until one of the parties gives notice.

**Opening date.** The day a renewal case opens: the decision point minus the customer's approval time on the original deal
(its approval and procurement stages, from the deal's stage history), minus your own approval time, minus any dead period
inside the window. The QBR before the case is dated no later than this day.

**Notice required by law.** A notice the provider has to serve before the time for a notice of non-renewal, where a statute
sets one, such as New York's General Obligations Law § 5-903. A row with its own method of service.

**Entitlement.** What the contract entitles the customer to use: seats, usage volume, modules.

**Co-term.** Aligning an amendment's end date with the live contract's end date, so that one buying unit has one decision
point.

**True-up.** An invoice for use past the entitlement, under a clause that provides for one.

**Contraction.** A reduction of the entitlement: inside the term, as far as the contract allows; at a renewal, a term of the
decision.

## The renewal case

**Decided by the decision point.** One of three forms recorded by the end of that day: a signed renewal; a written
confirmation of continuation from the economic buyer or the signatory, on an automatically renewing contract; a written
notice of non-renewal.

**Confirmation of continuation.** A dated written statement from a contact with authority that an automatically renewing
contract continues.

**Notice of non-renewal.** The customer's written statement that the contract will not renew. It carries a reason code and
an effective date.

**Protective notice.** A notice of non-renewal sent to reopen the terms: a decision, after which the case stays open until
the effective date.

**Reason code.** An entry of the theme list that `voice-of-customer` keeps by identifier.

**Renewed by default.** An automatically renewing contract that passed its decision point with no recorded decision and
renewed under its own provision. A class of the remainder, not a decision. Until the payment date of the new term's first
invoice it can still move to ended (a dispute settled as termination, a provision that does not hold, a completed switch).

**Undecided at the end.** A contract that needs a signature and reached its end date with neither a signature nor a notice.

**Holdover.** Service continuing past the end date under a written extension that has an end date and a price. That end
date is the **ceiling**. Without the writing there is no holdover, and access ends on the end date.

**Decided late.** A renewal signed after the decision point, inside a holdover.

**Ended.** A case that closed when the ceiling passed, or with no holdover.

**Effective date.** The date a notice of non-renewal takes effect: the end of the contract term.

**Days ahead.** How many days before the decision point the decision was recorded.

## The plan

**Won-deal record.** The object `b2b-lifecycle` hands over at a win: roles and coverage, the champion, the promised outcomes
and dates, open promises, the end date, the part not bought, the roles without coverage. **Its acceptance** is an event by a
promised time, or a return to the account executive that names the gap.

**Promised outcome.** What the customer bought for, in the record's words; a feature of the product is not one.

**Milestone.** A dated point on the way to an outcome, with a doer and a sign of completion.

**Sign of completion.** The evidence that a milestone was kept: an event in the product, a document, a confirmation by a
customer role.

**QBR.** The meeting where the plan is read with the buying group. The industry's name, kept whatever the cadence. **The QBR
before the renewal case** is dated no later than the opening date and includes the economic buyer, or a written summary goes to the economic buyer with a request to
confirm receipt.

**Ownership class.** Who writes in a stage of the contract term: the program; the account manager, with the program on an
allowed set; shared, with one queue per account; finance, with the program on finance's templates.

**Allowed set.** What the program may send in a stage it does not own: service rows, material for a role on request,
meeting reminders, nothing with a price.

**Readiness check.** The four conditions under which no expansion offer goes out: a milestone missed past its grace, an
open collection case, an open issue about a problem, an open renewal case.

**Relational ask per account.** The relational ask of `voice-of-customer`, sent to the plan's roles once per contract term
as a starting point, with its window closed before the QBR that precedes the renewal case.

## The collection case

**Class of non-payment.** Not received or not registered; disputed; approved for a payment run; cash shortfall; silence.
Read before any reminder.

**Cure period.** The time a contract gives to pay after a notice of non-payment, before suspension or termination.

**Ceiling.** The top of a state opened by an event, written on the day it opens: the end of the cure period for a
collection case, the end date of the written extension for a holdover. Where two states are open at once, the earliest
ending holds: past the end of the contract term, a collection case runs on a debt, not on a live contract.

**Access class.** Full; restricted or suspended; closed. Set by the contract, and each change comes with the contract's
notice.

**Payment route.** How a case that paid got there: after reminder N, after the account manager's call, after a fix to the
order or the billing details, in installments.

**Statutory interest and compensation.** What the law on late payment between businesses gives the creditor without a
reminder, in the European Union and the United Kingdom. Charged or not by a written policy.

## Seams with neighbors

Seven seams get crossed by accident, so state them outright.

- **The billing method assigns the charge; the contract assigns the decision.** A subscription charged to a card, a
  direct debit or an app store is `subscription-retention`'s even when a company pays: its term, the notices before the
  charge, the recovery case. A contract held by an account manager is this skill's: the plan, the decision point, the
  renewal case, the amendments. A contract billed by invoice is entirely here, the collection of an unpaid invoice
  included. The one split term is a contract with an account manager that is paid by card: the charge and its failure
  run in the neighbor's recovery case, the decision point and the renewal case run here, and a written notice of
  non-renewal on it is this skill's decision rather than the neighbor's exit request. Hold two conditions on the split. Give
  the recovery case a deadline no shorter than the contract's cure period, and change access or close it only with the
  contract's notice, since a suspension without that notice is your breach. Write the effective date of a notice of
  non-renewal into the neighbor's term register, where it counts as an exit decided outside the neighbor's program. The
  contract register names who holds each part.
- **An account in collection or in holdover is not gone.** Each state has a ceiling written on the day it opens: the end
  of the cure period, or the end date of a written extension. Until the ceiling the contract is live for every retention
  denominator, and the departure date is the day the state closes. Where two states are open at once, the earliest ending
  holds: a cure period that runs past the end of the contract term collects a debt, not a live contract, so the contract is
  live until the effective date of the non-renewal or of the termination, whichever comes first. The rule has a price: a longer cure period or holdover
  raises retention by construction, so the count and revenue of contracts in collection and in holdover stand beside the
  retention line. A holdover without a written extension does not exist; access ends on the end date.
- **The scoring of signals is the neighbor's; the contract's criteria are this skill's.** `lapse-and-winback` scores the
  signals of a departure, an account's included. The contract supplies criteria (seats in use against the account's own
  norm, the champion leaving, a request to reduce, a request for exit terms), the account manager validates, and a signal
  inside a renewal case becomes a risk entry in the case, not a campaign.
- **The won deal ends `b2b-lifecycle`'s work.** Before the close the account is the neighbor's, and so is the won-deal
  record; accepting that record by a promised time is this skill's first step. A new buying unit at an existing customer
  goes back to the neighbor as a new account.
- **The account cadence after the deal is set here.** `contact-orchestration` checks the cap per person first, and
  `b2b-lifecycle` runs one queue per account before the deal. After the close, the same form runs here, with the ownership
  classes of the contract term.
- **A notice, an invoice and a reminder carry no offer.** They are service rows of `transactional-messaging`, and the
  notice New York requires travels by personal service or certified mail, outside the program's channels. An expansion
  offer stands while a renewal case or a collection case is open.
- **The account manager's correspondence on the contract is not a program touch.** A request from a role with authority
  that nobody be written to suppresses the program's touches on the account (`consent-and-preferences`) and leaves the
  correspondence on the plan, the renewal and the invoices standing.

## Words shared with neighbors

- **term**: `subscription-retention`'s unit, one billing period of one subscription (or its commitment period). Here only
  "contract term", the period a contract commits both parties to, which invoices can split into billing periods.
- **renewal**: in `subscription-retention`, the end of a term charged to a card, a direct debit or an app store; here, the
  renewal of a contract held by an account manager. The billing method assigns the charge, the contract assigns the
  decision, and a contract paid by card is the one split term (`renewal-case.md`, edge cases).
- **recovery case, exit request**: `subscription-retention`'s units. The collection case takes the recovery case's form on
  an invoice; a notice of non-renewal is an exit under a contract, not from a screen.
- **review**: its senses are counted in `crm-program-design` and `program-audit-and-ops`. Not used here; the meeting with
  the buying group is the QBR.
- **owner**: not used. The salesperson before the deal is the account executive (`b2b-lifecycle`); after it, the account
  manager.
- **handoff**: `b2b-lifecycle` (the program passing an account to sales) and `chat-and-bots` (a bot passing an issue to a
  person). A won account reaching the account manager is called here the acceptance of the won-deal record.
- **grace**: in `b2b-lifecycle`, the time after a customer's promise past which a step counts as missed, used here in that
  sense inside the register of next steps; in `subscription-retention`, access without payment, which is not used here. A
  collection case has a cure period instead.
- **deadline**: in `transactional-messaging`, the moment a row has to arrive; in `subscription-retention`, the end of a
  retry window. Here the top of a state is its ceiling.
- **access class**: `subscription-retention`'s classes, in the same sense, set by the contract.
- **account, contact, account executive, champion, role, coverage, next step, promised time, account cadence, dead
  period, won-deal record**: `b2b-lifecycle`'s, in the same senses after the deal.
- **pre-lapse signal, scoring zone, validation, attempt**: `lapse-and-winback`'s. The contract supplies criteria, the zones
  arrive here as a validation queue, and the attempt to bring an account back runs there.
- **relational ask, obligation**: `voice-of-customer`'s; here the cadence per account.
- **service row**: `transactional-messaging`'s. Notices required by law or by the contract, invoices and reminders are its
  rows.
- **basis record, instruction, scope**: `consent-and-preferences`'. The account-level "do not contact" is a suppression with
  the scope "program touches", as in `b2b-lifecycle`.
- **offer**: `offer-design` owns the depth of a concession at renewal and in an amendment.
- **churn, revenue churn, net revenue churn, retention**: the general forms are `metric-definitions`'; here only the
  departure dates that close the cases.
- **cohort**: `crm-reporting`'s, by entry event; here the entry event is the contract's start, and a renewal changes no
  cohort.
- **activation**: `welcome-and-activation` defines the activation event of the customer's users; the first milestone here
  is the customer's first measurable result, not that event.
- **readable floor**: `segmentation`'s, which decides whether the control metric reads by quarter or by month.
