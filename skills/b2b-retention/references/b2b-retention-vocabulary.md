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
