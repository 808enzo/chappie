---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# The success plan: the won-deal record, milestones, roles, the QBR

The unit here is **the success plan of an account after the deal**: the outcomes the customer bought for, turned into
milestones with a date, a doer and a sign of completion, and the meetings where the plan is read with the buying group.
The account manager decides, together with the customer's champion; the program sends from an allowed set and keeps the
timers. The record written before the deal is `b2b-lifecycle`'s; scoring the signals of a departure is
`lapse-and-winback`'s; the questions of a survey and the reading of answers are `voice-of-customer`'s.

## Entry conditions

- The deal closed as won, and `b2b-lifecycle`'s won-deal record exists: roles and contacts with their coverage, the
  champion, the promised outcomes and dates, open promises with dates (implementation, integration, training), the
  contract's end date, the part proposed and not bought as an open opportunity, the doubts removed, the roles without
  coverage. For an account that bought without a salesperson, the account manager writes the record from the order form,
  the contract and the first call; `b2b-lifecycle` asks for the record in that case all the same.
- An account manager is assigned, and the contract has been in the register since the day it was signed
  (`renewal-case.md`, step 1).
- The contract is held by an account manager. A subscription on a card, a direct debit or an app store with no contract
  and no account manager belongs to `subscription-retention`, whoever pays; a contract with an account manager that is
  paid by card keeps its charge there and its plan here (`renewal-case.md`, edge cases).

## Exit conditions

A version of the plan closes: at a renewal, into the next version with the outcomes of the new contract term; at a
non-renewal, on the effective date (`renewal-case.md`, step 7). Every milestone carries a sign of completion, a miss with a
record, or a move recorded before its date. Every QBR carries the roles present, the milestones read, and the new promises
with their dates.

## Steps

**1. Accept the won-deal record by a promised time, and start from it.** The account manager accepts the record, or
returns it to the account executive and names the gap: no promised outcomes, no end date or renewal terms, no roles, no
billing contact. A return is the account executive's step with a date. Acceptance is an event with a date, not a changed
field. The account manager's first touch introduces them, confirms the promised outcomes and dates in the record's own
words, and books the first meeting on the plan. The account manager asks nothing the record already holds:
`b2b-lifecycle` sets the same rule for its handoff record (`qualification-and-handoff.md`, step 6), because a second
asking reads as "they do not listen". The promised time of the first touch is a starting point: within two working days
of the close. It holds for contracts whose first promise to the customer is weeks away; where a promise falls due
sooner, the first touch lands before it. Replace it with your own distribution of time from the close to the customer's
first unanswered question ("who do we work with now?"): the first touch has to come before that question. A record not
accepted by its promised time is a silent object for `program-audit-and-ops`.

**2. Write the ownership class of every stage of the contract term before any step goes out.** The stages are
implementation, from the signature to the first milestone of an outcome; use, until the opening date of the renewal case;
the renewal case, until its decision point; after a decision point that renewed the contract, confirmed its continuation or
passed by default, the use of the next contract term, with the account manager's confirmation on a renewal by default
(`renewal-case.md`, step 9); the notice period or the holdover, until the effective date or the ceiling;
and a collection case, while it is open, on top of any stage. The classes:

- *program:* the program writes to the customer's users through its own programs (`welcome-and-activation`,
  `email-program`, `in-product-messaging`), and the account manager receives signals;
- *account manager:* the account manager writes, and the program sends only from an allowed set: service rows
  (`transactional-messaging`), material for a role at the account manager's request, meeting reminders, nothing with a
  price;
- *shared:* one queue of touches per account with the account manager's touches in it, the account cadence of
  `b2b-lifecycle` (`sequence-between-touches.md`, step 5) applied after the deal;
- *finance:* the billing team writes, the program sends only finance's templates, and the account manager joins by the
  class of non-payment (`invoice-collection.md`, step 1).

Implementation and use take the shared class. The renewal case, the notice period and the holdover belong to the account
manager. A collection case belongs to finance. A stage with no class has no right to send, and silence in a stage a
person owns reads as a miss, not as pending. The account manager's own phone or messaging account is an origin without
registration (`messaging-channels`): its messages travel outside the program and are not counted in it, and a STOP said
to it is a withdrawal for the record (`consent-and-preferences`). Log on the account the questions the customer writes
to the account manager directly; otherwise they stay outside the support systems and tied to no case
(`transactional-messaging`).

**3. Turn the promised outcomes into milestones.** An outcome is what the customer bought for, in the words of the
won-deal record: a support response time, a second team at work in the product, a report closed in a day instead of a
week. A feature of the product is not an outcome. Each outcome gets one or more milestones, each with a sign of completion
(an event in the product, a document, a confirmation by a customer role), a date, and a doer, who is a customer role or
one of yours. A promise the customer made ("IT connects single sign-on by the first of the month") is the customer's step
with the grace of `b2b-lifecycle`'s register (`buying-group-and-stalls.md`, step 5). Your own promises (implementation,
integration, training) run a timer from the promised time, not from an event. A milestone without a date is not a
milestone, and the plan does not accept "when it is ready". The first milestone is the customer's first measurable
result; the time to it is a criterion for the scoring in `lapse-and-winback` and a line beside the control metric.

**4. Map the roles after the deal.** Start from the roles of the won-deal record and add the ones the contract needs
afterward: the administrator of the tool at the customer, users by team, the champion, the economic buyer with the
authority to renew, procurement and legal for the renewal paperwork, and the billing contact who pays the invoices.
Coverage is the count of roles with a live contact (a channel, a basis, a touch inside the stage's window), as in
`b2b-lifecycle` (`buying-group-and-stalls.md`, step 2), out of the roles your renewed contracts had covered by the opening
date of their renewal case. Derive that set from a retrospective of renewed and non-renewed contracts, not from someone
else's list. A role without coverage is the account manager's step with a date. The way to a missing role is one of the
four lawful ways in `b2b-lifecycle` (step 4 of the same file); a contact named by a colleague gets a record with its
source and a first message that states the source (`consent-and-preferences`).

**5. A change of role is a step, not a status.** A contact left the company (a bounce saying "no longer works here", an
auto-reply): `list-building` and `deliverability` suppress the address, the role's coverage drops, and the account
manager's step is to find the successor through the remaining contacts. The economic buyer changed: the new person did not
make the decision to buy, so a meeting with them on the plan goes before the next opening date of a renewal case, or first
in the case if one is already open. A champion leaving and an economic buyer changing are alarming actions for the scoring
in `lapse-and-winback` (`early-interception.md`, step 2).

**6. The QBR is the meeting where the plan is read with the buying group.** It runs no less often than the plan's
milestones fall due, and at least once in a contract term, dated no later than the opening date of the renewal case (`renewal-case.md`, step 3); the industry's name stays
whatever the cadence. The agenda comes from the plan: milestones with their signs (kept, missed, moved); use against the
contract's entitlement; open issues and escalations (`chat-and-bots`); answers to the relational ask and open obligations
(`voice-of-customer`); changes of role; the outcomes of the next period with their dates and doers. The program sends the
pre-read and the reminders; the booking confirmation and the "please confirm" are service rows, as in `b2b-lifecycle`
(`sequence-between-touches.md`, step 7). The account manager writes the summary: the roles present, the new version of
the plan, and the promises with dates, each of them a timer.

**The QBR before the renewal case opens includes the economic buyer.** If the economic buyer does not come, a written
summary of the plan for the contract term goes to them with a request to confirm receipt, and the account manager's next
step is a meeting through the champion (the first of `b2b-lifecycle`'s four ways). A renewal case that opens with no
contact holding authority opens without the person who decides.

**7. Run the relational ask on the account's cadence.** Its form, its questions, the cap per person and the reading of
answers are `voice-of-customer`'s (`asking.md`, step 7: a relational ask runs on the program's calendar with a lifetime
cap per person); the cadence per account is set here. The ask goes to the plan's roles: users, the administrator, the
champion, the economic buyer, and not the billing contact. It goes once per contract term, timed so that its window closes
before the QBR that precedes the renewal case, and the answers get read in that meeting. That is a starting point: it
holds for contracts of a year or longer, and for shorter contracts it becomes once per year of the relationship; replace
it with your response share per version of the ask and with the neighbor's cap per person. An obligation from an answer
goes to the account manager, and the closure goes to the person who answered, with the account manager copied
(`voice-of-customer`, `closing-the-loop.md`, the edge case of an answer on behalf of an organization). No ask goes while a
collection case is open, or to a person with an open issue about a problem.

**8. Keep the program's touches after the deal inside the account cadence.** The cap per person is
`contact-orchestration`'s, and the program checks it first. On top of it runs one queue per account with the account
manager's touches in it, `b2b-lifecycle`'s form, applied here after the deal. A marketing offer of expansion stands
while a milestone is missed past its grace, a collection case is open, an issue about a problem is open, or a renewal
case is open (`expansion-and-contraction.md`, step 2). The account manager's correspondence on the contract (the plan,
the renewal, the invoices) is not a program touch. A request from a role with authority that nobody be written to is a
suppression on the account with the scope "program touches" (`consent-and-preferences`, as in `b2b-lifecycle`); it does
not stop the correspondence on the contract.

**9. Send the signals into the neighbor's scoring; build no score here.** Scoring the signals of a departure belongs to
`lapse-and-winback` in full, an account's included. The contract supplies criteria of both of its classes
(`early-interception.md`, step 2): *a drop in level*, such as the share of seats in use against the account's own norm or
the time to the first milestone; *an alarming action*, such as the champion leaving, the economic buyer changing, a request
to reduce the entitlement, a request for the terms of data export or termination, or a procurement tender by the customer
in your category. The account manager's look is the validation (step 5 of that file: the units are few, and each is
expensive), and the neighbor's zones arrive here as the account manager's validation queue. A signal inside a renewal
case's window becomes a risk entry in the case (`renewal-case.md`, step 5), not a separate campaign, and no monetary
argument goes out on a signal (step 6 of the neighbor's file). A contact's objection to profiling removes that contact's
signals from the scoring, by the rule of `consent-and-preferences`, as `b2b-lifecycle` does for its grade.

**10. Close the version of the plan.** At a renewal, write a new version: the outcomes of the next contract term, the
milestones, the roles, the cadence of QBRs. At a non-renewal, the plan closes on the effective date, and the promises made
up to that date are kept, the terms of exit included (`renewal-case.md`, step 10).

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Promised time of the account manager's first touch | within two working days of the close, as a starting point; before the earliest promise to the customer; replaced by your time to the customer's first unanswered question | 5 |
| Grace on a customer's promise | the rule of `b2b-lifecycle`'s register | the neighbor's |
| Roles covered by the opening date | the retrospective of the segment's renewed and non-renewed contracts | 4 |
| Window for a live contact | the stage's window, as in `b2b-lifecycle` | 4 |
| QBR cadence | no less often than the plan's milestones fall due; at least one meeting with the economic buyer before the renewal case opens | 4 |
| Relational ask per account | once per contract term, its window closed before the QBR that precedes the renewal case, as a starting point; contracts of a year or longer; replaced by your response share and the neighbor's cap per person | 5 |

## Edge cases

- **Bought without a salesperson.** No won-deal record exists; the account manager writes it from the order form, the
  contract and the first call, and the plan starts from the first milestone of use.
- **The plan and the renewal held by two people.** A customer success manager holds the plan, and an account manager
  holds the renewal and the amendments. The classes stay the same, and the stages are split between the two by name. The
  meeting before the opening date is joint; otherwise the renewal opens without knowledge of the plan.
- **A small contract with no dedicated account manager.** A pool holds the account. The plan is read from product events
  and the relational ask, and a written summary of the plan goes to the economic buyer before the opening date instead of
  a QBR. The renewal stages still belong to an account manager of the pool, not to the program: the program does not run
  a decision on a contract.
- **A third-party integrator runs the implementation.** The integrator's promises are milestones on the customer's side,
  with timers; a date that passes is the account manager's step toward the champion and the integrator, with a new date.
- **The customer was acquired, or acquired another company.** The roles change, and a meeting with the new economic buyer
  comes first. The contract follows its assignment clause; the users of the acquired company become an amendment
  (`expansion-and-contraction.md`) or a separate contract; a changed buying unit is a new account in `b2b-lifecycle`.
- **Several buying units at one customer.** Each has its own plan, its own renewal case and its own amendments; an
  economic buyer shared between them is a contact at several accounts.
- **A contract through a reseller.** The customer's contract is with the reseller: the plan runs with the customer, the
  renewal case runs with both parties, and the invoices and their collection stay with the reseller.
- **The customer declines meetings.** Record the refusal in the plan; a written summary with a confirmation of receipt
  from the economic buyer replaces the QBR.

## Failure modes

**A plan of features.** The milestones are product setup steps, the customer's outcomes are missing, and the QBR shows
usage charts. The sign: milestones carry no sign of completion from the customer's side; non-renewals arrive with the code
"no value" while usage is high. Remedy: outcomes in the words of the won-deal record, and a sign of completion from the
customer's side.

**A QBR without the person who decides.** The sign: the roles present are users and the champion only; the renewal case
opens with no contact holding authority, and the decision stalls in procurement. A second cause with the opposite
reading: the economic buyer comes, but the plan does not change after the meeting; meetings happen, no new dated
milestones follow, and the share of moved milestones grows. Remedy: the meeting before the opening date with the economic
buyer, or a written summary with a confirmation; promises with dates in the summary of every meeting.

**The silent account.** The sign: the plan's version is older than the QBR cadence; milestones passed with no record; no
account manager touch for longer than the stage. A second cause with the opposite reading: too many touches, with the
program and the account manager writing to the same roles in the same week, and unsubscribes inside the account. Remedy:
the ownership class of the stage, and one queue per account.

**A change of role nobody noticed.** The sign: "no longer works here" bounces with no step from the account manager; the
champion's or the economic buyer's role uncovered on the opening date of the renewal case. Remedy: every change of role is
a step with a date (step 5).

**The won-deal record never accepted.** The sign: the account manager's first touches ask what the record already holds;
promised dates of the first month are missed. Remedy: acceptance as an event with a promised time (step 1).

This file rests on no statute or platform rule; the regimes it touches are in `SKILL.md`.
