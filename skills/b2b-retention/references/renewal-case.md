---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The renewal case: the decision point, the opening date, the decision, the holdover

The unit here is **the renewal case**: one contract term on its way to its decision point. The customer decides; the
account manager runs the case, and the program sends notices and material from the allowed set. The depth of any
concession is `offer-design`'s; the class of a service row is `transactional-messaging`'s; the one attempt to bring back an
account that left is `lapse-and-winback`'s.

## Entry conditions

A live contract held by an account manager, billed by invoice (the billing method stands in the register, step 1; a
contract paid by card is the split term of the edge cases); or a written notice of non-renewal received at any point in
the term; or the customer's request to renew early.

## Exit conditions

The case closes as one of these.

- **Decided by the decision point:** a signed renewal (an order form, a renewal agreement, an amendment that extends the
  term) with its terms recorded: unchanged, with expansion, with contraction, with a price change, with a change of term
  length; a written confirmation of continuation from a contact with authority, on a contract that renews automatically;
  a written notice of non-renewal with a reason code and an effective date.
- **The remainder:** renewed by default, meaning an automatically renewing contract passed its decision point with no
  recorded decision; undecided at the end, meaning a contract that needs a signature reached its end date with neither a
  signature nor a notice, and then became decided late (signed during a holdover) or ended (the ceiling passed, or there
  was no holdover).

Recorded with it: the decision point, the opening date, the notices required by law and by the contract with their dates
and methods, the decision date, the terms, the reason code.

## Steps

**1. Write the contract register on the day of the signature.** The fields: the buying unit and the account; the start
and end of the contract term; the renewal class, which is automatic renewal for a set term, a new term by signature, or
evergreen after the initial term; the notice period for non-renewal, its counting rule (calendar or business days, "no
later than", the date of receipt or of dispatch), and the form and address of the notice; the rule for a price change at
renewal and its notice period; the entitlement (seats, usage volume, modules); the invoice schedule and the payment terms;
the cure period for non-payment and the suspension procedure; the contractual response time of support, where the
contract has one (the routing in `chat-and-bots` reads it); the governing law; the billing method, which is invoice here,
while a card, a direct debit and an app store go to `subscription-retention`. Which system holds the register, and how
fresh its fields are, is `martech-stack`'s question. Contracts signed before the register existed enter it through a pass
over the archive, and on the first day the register runs, every contract whose decision point has already passed with no
record comes out as a list, not as one line.

**2. The decision point is the last day the customer still decides.** For an automatic renewal, it is the end date minus
the notice period, counted by the contract's own rule. For a contract that needs a signature, it is the end date. For a
multi-year contract with an exit right at each anniversary, every such anniversary is a decision point of its own and opens a
case of its own: the last day of notice before it. Silence there continues the contract under its provision, and the case
closes as renewed by default. For a contract through a reseller, it is the earlier of two last days: the customer's last day
of notice to the reseller and the reseller's last day of notice to you. An
evergreen contract past its initial term has no decision point until one of the parties gives notice (see the edge cases).
The decision point goes into the register on the day of the signature and gets a timer. A contract with no decision point
recorded counts on its end date in the remainder (`SKILL.md`, the control metric). The dead periods of the buying organization
(`b2b-lifecycle`, `sequence-between-touches.md`, step 9) do not move the decision point: the contractual date stands as
written, and the opening date moves instead (step 3).

**A notice required by law is a row with its own method.** In New York, General Obligations Law § 5-903 makes an automatic
renewal provision in "a contract for service, maintenance or repair to or for any real or personal property"
unenforceable against the recipient unless the provider gives written notice, "served personally or by certified mail",
at least 15 and not more than 30 days before the time for serving notice of non-renewal; a "person" includes a firm and a
corporation, and the section does not apply where the renewal period is one month or less (the quotations and the address
are in `SKILL.md`). The notice is a row of the service register whose method is personal service or certified mail, not a
message from the program; record its date and method in the case. Whether a software contract is a contract "for
service, maintenance or repair" is a question for counsel. In Germany, § 309 of the Civil Code, the rule on tacit
extensions included, does not apply to standard terms used against a business (§ 310(1)), while § 307 still applies where
it leads to the invalidity of the terms § 309 names: the consumer rule does not carry over to a business contract as it
stands, and it does not disappear either. The consumer renewal regimes of California and the United Kingdom do not reach
organizations (`subscription-retention`).

**3. Count the opening date back from the customer's approval time, not from the end date.** The opening date is the
decision point minus the customer's approval time, minus your own approval time for the terms. The QBR before the case
(`success-plan-and-qbr.md`, step 6) is dated no later than the opening date, so its timer is the opening date itself. Take
the customer's approval time from the original deal: the time it spent in the approval and procurement stages up to the
signature, from that deal's stage history in the CRM, since `b2b-lifecycle` gives every stage a duration of its own. The
won-deal record carries outcomes and dates, not stage durations. Where no stage history exists, the starting
point is a quarter before the decision point; it holds for annual contracts with one buying unit; replace it with your own
distribution of time from the renewal proposal to the signature, by contract class. A dead period of the customer that
falls inside the case's window moves the opening date earlier by its length.

**4. Open the case on its opening date, with its ceiling.** The ceiling is the decision point, written on the day the case
opens. The case keeps a register of next steps in `b2b-lifecycle`'s form (`buying-group-and-stalls.md`, step 5: one next
step, a doer, a promised time, the customer's step with a grace): the record of the QBR before the case
(`success-plan-and-qbr.md`, step 6), or the meeting itself as the first step where it did not happen by the opening date;
the renewal proposal, your approval of the terms, and the customer's steps (supplier registration, a security
questionnaire, legal redlines, a purchase order), each with a date. The ownership class is the account manager's. The
program sends only from the allowed set (`success-plan-and-qbr.md`, step 2): the notices required by law and by the
contract, the material the account manager asks for (a summary of the plan for the term), and meeting reminders. No offer
with a price and no promotional send goes to the account's contacts until the case closes.

**5. Build the renewal proposal from the plan and the entitlement.** The terms: a price change under the contract's rule
and with its notice period, so that a notice not sent in time keeps the old price or goes into the case as an exception,
and never raises the price retroactively; the entitlement by use, so that unused seats enter the proposal as a contraction
instead of surfacing at the signature (`expansion-and-contraction.md`, step 7); amendments that arrived inside the case's
window, folded into the proposal (`expansion-and-contraction.md`, step 3); an option on term length. The depth of any
concession is `offer-design`'s, and a concession for signing before the decision point stands beside the control metric.
Risks from the plan and the zones from `lapse-and-winback`'s scoring become risk entries in the case, each with a step and
a date.

**6. Record the decision in one of three forms.** A signed renewal with its terms. A written confirmation of continuation
on an automatically renewing contract, from the economic buyer or the contract's signatory, dated and kept in the case. A
written notice of non-renewal, with its date of receipt and a reason code. A verbal "we will renew" is a next step, not a
decision. The reason code comes from the theme list `voice-of-customer` keeps by identifier, as in
`subscription-retention`; a contract needs at least these entries: budget; switched to another vendor (which one); no use
or no value; the customer was acquired or merged; the project closed; price; a missing feature; service quality; a
protective notice.

**7. A written notice of non-renewal is an exit with an effective date.** Confirm receipt in writing, with the date of
receipt under the contract's rule; the effective date is the end of the contract term. Offer one alternative per reason,
before any concession: for "no use", a contraction of the entitlement; for "budget", a contraction, a shorter term or a
smaller package; for "no value", a repair of the plan, only if a milestone can be kept before the effective date; for
"switched", nothing beyond the terms of exit (step 10). A discount for silence is not the program's instrument
(`b2b-lifecycle`). **A protective notice**, sent to reopen the terms, does not close the case: the case stays open with the
effective date as its ceiling. A renewal signed before the effective date and a notice that takes effect are both
decisions made by the decision point, and the date moves only the split between them, the way a cancellation and a restore
do in `subscription-retention`. Record a notice that arrived in a form other than the contract's with its date of receipt;
whether the form is valid is a question for counsel, and the form is never used to renew a contract against the
customer's plainly stated will.

**8. A holdover exists only in writing and with a ceiling.** A contract that needs a signature reached its end date with
neither a signature nor a notice, and the service continues: that happens only under a written extension with an end date
(the ceiling) and a price. Without one, access ends under the contract on the end date, so a silent holdover does not
exist. Until the ceiling the contract is live for every retention denominator. The departure date is the date the case
closes: a signature makes it decided late, with the new term running from the original end date; the ceiling passing with
no signature ends it, and the departure date is the ceiling. The rule has a price. On every day of a holdover a contract
nobody signed counts as retained, so the count and revenue of contracts in holdover on the period's end date stand beside
retention, together with whether the holdover is invoiced.

**9. Renewed by default is a class, not a success.** An automatically renewing contract passed its decision point with no
recorded decision and renewed under its own provision. Record the class. The account manager's step is a written
confirmation before the payment date of the new term's first invoice (from the invoice schedule); the confirmation does not
change the class. Read the class's fate beside the metric: how many such contracts opened a collection case on the renewal
invoice, and how many sent a notice of non-renewal in the next term. A renewal by default can still come apart before
the payment date of the new term's first invoice: a dispute on that invoice settled as termination, a provision that does
not hold without the notice the law requires, a completed switch. The case then moves to ended, and the day it ended is the
departure date. Each term is its own case, so a contract renewed by default twice stands in the remainder twice. In New York, without the notice § 5-903 requires, the
provision may not hold against the customer, so the register keeps the date and method of service.

**10. The exit after a non-renewal: data, access, hand-off.** The service rows of `transactional-messaging`: the
confirmation of the notice with its effective date; the window for exporting data and the date of deletion; the end of
access. Where you process personal data on the customer's behalf, at the end of the services the data are deleted or
returned at the customer's choice (GDPR Article 28(3)(g)), with the form and timing set by the data processing agreement.
For a cloud service in the European Union, the customer's request to switch to another provider runs on its own clock
under the Data Act (`SKILL.md`): a notice period of no more than two months, a transitional period of no more than 30
calendar days, and data retrieval for at least 30 calendar days after it; none of these waits for the decision point.
After the effective date the account is gone, with its reason code: the one finite attempt to bring it back is
`lapse-and-winback`'s, and marketing sends to its contacts follow the basis record (`consent-and-preferences`: in Canada
the exception covers a written contract within two years).

**11. Close the case with a record.** The outcome; the decision date and how many days ahead of the decision point it came;
the terms; the reason code; the notices with their dates and methods; the days of holdover. The control metric and the lines
beside it come from this record and from nothing else.

## Thresholds and timings

| Quantity | Value | Class |
|---|---|---|
| Notice before the time for serving notice of non-renewal, on a contract for service, maintenance or repair of property in New York | at least 15 and not more than 30 days before that time, served personally or by certified mail | 2, NY General Obligations Law § 5-903(2) |
| Renewal period to which § 5-903 does not apply | one month or less | 2, NY General Obligations Law § 5-903(3) |
| Decision point | the end date minus the notice period under the contract's rule; the end date for a contract that needs a signature; each anniversary with an exit right; through a reseller, the earlier of the two last days of notice | 4 |
| Opening date of the case | the decision point minus the customer's approval time on the original deal (approval and procurement stages, from the deal's stage history), minus your approval time, minus any dead period inside the window; the QBR before the case no later than this date | 4 |
| Customer's approval time with no record | a quarter before the decision point, as a starting point; annual contracts with one buying unit; replaced by your own distribution from proposal to signature | 5 |
| Ceiling of a holdover | the end date of the written extension | 4 |
| Confirmation of a contract renewed by default | before the payment date of the new term's first invoice | 4 |
| Personal data at the end of a processor's services | deleted or returned at the controller's choice | 2, GDPR Article 28(3)(g) |
| Notice period for switching a cloud service in the European Union | no more than two months | 2, Data Act Article 25(2)(d) |
| Transitional period | no more than 30 calendar days; where that is technically unfeasible, notice within 14 working days and an alternative of no more than seven months | 2, Data Act Article 25(2)(a) and 25(4) |
| Data retrieval after the transitional period | at least 30 calendar days | 2, Data Act Article 25(2)(g) |
| Switching charges | none from January 12, 2027; until then, no more than the costs directly linked to the switch | 2, Data Act Article 29(1) to (3) |
| Exception from a written contract in Canada | a written contract within two years | 2, through `consent-and-preferences` |

## Edge cases

- **An evergreen contract past its initial term.** It has no decision point until someone gives notice, so it stays
  outside the control metric's denominator, with its count and revenue beside it; a growing share of evergreen contracts
  is the sign that the denominator is emptying. The plan and the QBRs run on their own cadence
  (`success-plan-and-qbr.md`), and a notice of non-renewal opens a renewal case with the end of the notice period as its
  ceiling.
- **A contract paid by card.** An organization with a signed contract, a notice period and an account manager, whose
  charges go to a card: the term, the notices before the charge and the recovery case are `subscription-retention`'s,
  because the billing method assigns the charge; the decision point and the renewal case are here, because a term in the
  neighbor's register carries no notice period and no decision point. Both registers carry the contract's identifier, a
  written notice of non-renewal on it is this case's decision and opens no exit request at the neighbor, and a recovery
  case open on the decision point is a risk entry here, not an answer. Give the neighbor's recovery case on such a contract a
  deadline no shorter than the contract's cure period, and change access only with the contract's notice. Write the
  effective date of a notice of non-renewal into the neighbor's term register, where it counts as an exit decided outside the
  neighbor's program.
- **Contracts with aligned end dates.** One decision point makes one case per buying unit
  (`expansion-and-contraction.md`, step 3).
- **A multi-year contract with price steps.** The decision point sits at the end of the multi-year term, and at
  every anniversary with an exit right, each a case of its own (step 2); a price step is a term of the contract, not an
  event of the case.
- **A contract through a reseller.** The register carries both notice periods, the customer's to the reseller and the
  reseller's to you, and the decision point is the earlier of the two last days (step 2). The decision arrives as the
  reseller's order; the case runs with both parties; the
  notice under § 5-903 comes from the party to the customer's contract.
- **A public buyer.** A renewal is the exercise of an option by a date the contract sets, and that date is the decision
  point; an option not exercised in time leaves the case undecided at the end. Service continues only under a written extension
  with an end date, such as a bridge order the buyer's rules allow; otherwise access ends on the end date, even while the
  buyer runs a new procurement. That procurement is a deal in `b2b-lifecycle`'s procurement window, and a contract won
  after the case ended is recorded as a return.
- **The customer acquired mid-term.** The contract follows its assignment clause, and the opening date moves earlier: the
  new economic buyer has a different approval time and no record of it.
- **The economic buyer left during the case.** Covering the role is the account manager's step with a date
  (`success-plan-and-qbr.md`, step 5); the signature belongs to the signatory under the contract.
- **A price change notice not sent in time.** The old price holds, or you record an exception; the price does not rise
  retroactively.
- **A notice "at the current volume".** A customer who writes "we will not renew at this volume" gives the reason "budget"
  or "no use" and invites the alternative of a contraction; it is not a notice to end the whole contract until the customer
  says so.

## Failure modes

**Nobody wrote the decision point.** The sign: notices of non-renewal "arrive late" and you reject them as late; disputes
over automatic renewals; renewals discovered from the invoice. Remedy: the decision point in the register on the day of
the signature, and a pass over the archive that comes out as a list.

**The renewal starts at the end date.** The sign: holdovers grow; decisions arrive few days ahead of the decision point;
procurement asks to extend the contract by a month. A second cause with the opposite reading: the case opens early, but
no QBR with the economic buyer came before it, so the days ahead are many and the decision still waits until the last
week. Remedy: the opening date from the approval time, and the QBR with the economic buyer before the case.

**Renewed by default, read as a success.** The sign: the renewed share is high while renewal invoices go to collection and
next-term notices of non-renewal grow. A second cause: the notice the law requires was never served, and the renewal does
not hold against the customer. Remedy: the class "renewed by default" with a confirmation before the payment date, and
the date and method of service in the register.

**A holdover that never ends.** The sign: contracts past their end date still "active"; holdover revenue with no invoices.
Remedy: a written extension with a ceiling, or the end of access under the contract.

**The concession as the save.** The sign: concessions cluster in cases with a protective notice; protective notices arrive
earlier every year, because customers have learned the pause. Remedy: one alternative per reason; the concession is
`offer-design`'s; a discount for silence is not an instrument.

**Sources for the rules in this file, each opened 2026-09-15.** The addresses stand in `SKILL.md`: New York General
Obligations Law § 5-903; Bürgerliches Gesetzbuch § 310; Regulation (EU) 2023/2854 (Data Act), Articles 25 and 29;
Regulation (EU) 2016/679, Article 28.
