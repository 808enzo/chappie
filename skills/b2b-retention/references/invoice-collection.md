---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The collection case: an invoice unpaid under a contract

The unit here is **the collection case**: an invoice under a contract that was not paid by its payment date. Finance runs
it; the account manager joins by the class of non-payment; the program sends finance's templates. The form is the one
`subscription-retention` proposed from its recovery case: a ceiling written on the day the case opens, an access class per
stage, and a close by decision or by expiry. The contract sets the window, not a card network. The class of a service row
is `transactional-messaging`'s; the attempt to bring back an account that left is `lapse-and-winback`'s.

## Entry conditions

An invoice under a contract (for a renewal, a billing period, a true-up or an amendment) was not paid by its payment date.
Before that date, the invoice and the reminder about it are rows of the service register (`transactional-messaging`: a
payment outside an order, such as an invoice, is a transaction of its own). A failed charge on a card or a direct debit is
`subscription-retention`'s.

## Exit conditions

Paid, with its route: after reminder N; after the account manager's call; after a fix to the purchase order or the billing
details; in installments on a recorded schedule. Settled with a credit note on a dispute. The contract terminated for
non-payment under its terms, with the departure date on the day the termination takes effect. Written off together with
the end of the contract. Recorded with it: the class of non-payment, the ceiling, the access history, the number of
messages, the days overdue, and whether statutory interest and compensation were charged.

## Steps

**1. Classify the non-payment before any reminder.** Five classes.

- *Not received or not registered:* no purchase order number, the wrong legal entity or address, the supplier not set up
  in the customer's payables system. A reminder does not help; the invoice needs a fix or a registration, and the step is
  finance's, with the billing contact.
- *Disputed:* the amount, the entitlement, a true-up, the quality of the service. Collection on the disputed part stands,
  the undisputed part goes on to payment, and the account manager takes the dispute to the champion with a date.
- *Approved for a payment run:* the customer named the date of its payment run. That is the customer's promise, a step
  with a grace, and not a reason for reminders.
- *Cash shortfall:* the customer said so, or the signs show it. The account manager and finance agree a payment schedule on
  the record, or apply the contract's terms.
- *Silence:* none of the above; reminders run on the schedule of step 4.

**2. Write the ceiling on the day the case opens.** The ceiling is the end of the cure period under the contract: the
notice of non-payment, the cure period, the suspension and the termination come from its terms, and where the contract is
silent, from your policy, written before the first invoice. Until the ceiling, the contract is live for every retention
denominator. The departure date is the day the case closes by termination, not the first day overdue. A case with no
ceiling does not exist. A cure period that runs past the end of the contract term keeps the case open on a debt, not on a
live contract: the contract is live until the effective date of the non-renewal or of the termination, whichever comes
first.

**3. Give each stage an access class, by the contract.** Full, until the notice of suspension and the end of the cure
period; restricted or suspended, after the notice the contract requires, from a stated date; closed, after termination.
Every change is an event of a service row, with notice in the contract's form. A suspension without the contract's notice
is your breach of the contract, not the customer's.

**4. Time the messages to the customer's payables process, not to the calendar.** Before the payment date, confirm that
the invoice was received and matched to the purchase order: before the date that confirmation catches the class "not
received", and after it the invoice is already overdue. On the day after the payment date, send a reminder to the billing
contact with the invoice and order numbers. After that, follow the policy's schedule; escalate to the account manager and
the champion on the classes "disputed" and "cash shortfall", and after the number of unanswered reminders the policy sets;
send the formal notice of suspension in the contract's form. Finance writes; the program sends finance's templates; the
account manager writes to the roles; marketing offers to the account stand (`success-plan-and-qbr.md`, step 8). No
reminder goes out while a payment is already processing.

**5. Confirm the payment.** Tell the billing contact and the account manager, and bring restricted access back on the day
of the payment. A payer who hears nothing asks with a second payment or a message to support, and both count with the
inquiries.

**6. Close on the ceiling.** When the ceiling passes with neither payment nor settlement, terminate under the contract, or
extend the cure period in writing with a new ceiling, recorded as a decision with a date; no case is left without a
ceiling. A termination is the departure date, and the account is gone with the reason code "non-payment". The attempt to
bring it back is `lapse-and-winback`'s, and its first message is the way back with the debt settled, not an offer.

**7. Treat statutory interest and compensation as a written policy, not a reaction.** In the European Union and the United
Kingdom the right to interest and to a fixed compensation arises without a reminder (`SKILL.md`); whether you charge them
is set by a policy per class of customer, written before the first invoice. A "not received" caused by your own error is a
delay the debtor is not responsible for (Directive 2011/7/EU, Article 3(1)(b)), so charge no interest on it.

**8. Close the case with a record.** The class; the payment route; the days overdue; the access history; the number of
messages; interest and compensation, charged or not. The lines beside the control metric come from this record.

## Thresholds and timings

| Quantity | Value | Class |
|---|---|---|
| Statutory interest for late payment between businesses in the European Union | simple interest at the reference rate plus at least eight percentage points | 2, Directive 2011/7/EU, Article 2(6) and (7) |
| When interest starts in the European Union | the day after the payment date fixed in the contract; with none fixed, 30 calendar days after the debtor receives the invoice | 2, Directive 2011/7/EU, Article 3(3) |
| Payment period in a contract between businesses in the European Union | no more than 60 calendar days, unless expressly agreed otherwise and not grossly unfair to the creditor | 2, Directive 2011/7/EU, Article 3(5) |
| Compensation for recovery costs in the European Union | at least EUR 40, without a reminder, plus reasonable recovery costs above it | 2, Directive 2011/7/EU, Article 6 |
| Statutory interest in the United Kingdom | 8% a year over the official dealing rate in force on June 30 or December 31 before interest starts | 2, Late Payment of Commercial Debts (Rate of Interest) (No. 3) Order 2002, article 4 |
| When interest starts in the United Kingdom | the day after the agreed payment day; with none, the last day of the relevant 30-day period, counted from the later of the supplier's performance and the purchaser's notice of the amount; for a public authority purchaser, an agreed day later than the relevant 30-day period gives way to that period; for any other purchaser, an agreed day later than the relevant 60-day period gives way to that period unless the agreed day is not grossly unfair to the supplier | 2, Late Payment of Commercial Debts (Interest) Act 1998, section 4(2) to (2I) |
| Fixed compensation in the United Kingdom | £40 for a debt under £1,000; £70 from £1,000 to under £10,000; £100 from £10,000; plus reasonable recovery costs above it | 2, Late Payment of Commercial Debts (Interest) Act 1998, section 5A |
| Ceiling of the case | the end of the cure period under the contract or the policy, written on the day the case opens | 4 |
| Reminder schedule and escalation threshold | finance's policy | 4 |

## Edge cases

- **The renewal invoice of a contract renewed by default.** Class "disputed", with the reason "we did not renew": the
  account manager seeks the decision (`renewal-case.md`, step 9), and collection on the dispute stands.
- **A partial payment.** The case runs on the balance, and the ceiling does not move.
- **A payment after termination.** A new contract, or a reinstatement by agreement; the case does not reopen, and the
  account gets a return on its record.
- **A public buyer.** In the European Union, payment periods for public authorities have an article of their own in the
  Directive (Article 4), which was not opened here and is left to you with the national law. In the United Kingdom, an
  agreed payment day later than the relevant 30-day period gives way to that period when the purchaser is a public
  authority (section 4(2D)).
- **A reseller that does not pay.** The case runs with the reseller; the customer's access follows the reseller's contract.
- **The customer's insolvency.** Collection follows the proceedings, with counsel; the case closes by termination or by a
  write-off on that decision, with a date.
- **Collection in the United States.** The federal Fair Debt Collection Practices Act defines a debt as an obligation of a
  consumer for personal, family or household purposes; a company's debt under a business contract falls outside that
  definition, and state laws were not opened here.

## Failure modes

**Reminders on a disputed invoice.** The sign: replies saying "we are disputing this" to reminders; escalations from
finance to the economic buyer; a notice of non-renewal with the code "service quality". Remedy: classify before any
reminder (step 1).

**The wrong payer.** The sign: reminders go to the champion or to users instead of the billing contact; replies saying
"forwarding to accounts payable"; the class "not received" discovered after the payment date. Remedy: the billing contact
as a role in the plan (`success-plan-and-qbr.md`, step 4), and the confirmation of receipt before the payment date (step 4).

**Suspension without notice.** The sign: access closed before the date of the contract's notice; "you cut us off" messages
reaching the account manager. Remedy: the access class by the contract (step 3).

**Overdue forever.** The sign: cases with no ceiling; contracts overdue for longer than their cure period still "active";
billed revenue holds while receipts stop. Remedy: the ceiling on the day the case opens (step 2).

**Interest charged for your own error.** The sign: interest on invoices of class "not received"; interest disputes from
customers with no history of late payment. Remedy: classify before charging (step 7).

**Sources for the rules in this file, each opened 2026-09-15.** The addresses stand in `SKILL.md`: Directive 2011/7/EU,
Articles 2, 3 and 6; Late Payment of Commercial Debts (Interest) Act 1998, sections 1, 2, 4 and 5A; Late Payment of
Commercial Debts (Rate of Interest) (No. 3) Order 2002, article 4; 15 U.S.C. § 1692a.
