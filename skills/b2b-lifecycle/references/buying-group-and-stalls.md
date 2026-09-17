---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-14
---

# The buying group and the stall: roles, coverage, the next step, silence, the close

The unit here is **the account in a sales stage, with its group**. The account executive decides which role is
missing, what to do with silence, and how to close; the program supplies material and keeps the register of
next steps and its timers.

Acceptance and the return are in `qualification-and-handoff.md`; what the program may send in a sales stage and
the account cadence are in `sequence-between-touches.md`. Price and terms are `offer-design`'s. The basis for
writing to a person, and the basis for a colleague's address obtained from somebody else, are
`consent-and-preferences`' and the legal section of `SKILL.md`. After the win, everything is `b2b-retention`'s.

## Entry conditions

- The account was accepted (`qualification-and-handoff.md`, step 7) and stands in a sales stage or a shared one.
- An account executive is assigned, and at least one contact has a channel.
- The CRM has a role field on the contact and a next-step field on the account with a date. The next-step field
  is any dated object attached to the account or to its open deal: a task, an activity, a scheduled send; a text
  field with no date, as some CRMs ship it, does not count. Without those two fields the register is impossible,
  and the mechanic does not start.

## Exit conditions

A decision of the buying group: won, with the record handed to `b2b-retention` (step 10); lost, with a close
code and a re-entry date (step 9); "not now," with a return to the sequence (`sequence-between-touches.md`, step
12). The register closes with a close entry.

## Steps

**1. Derive the roles from your own won deals, not from somebody's list.** A retrospective: for the won deals of
the window, which roles are recorded on the contacts and in which stage each first appeared; which roles the lost
deals lacked. The usual roles are the user, the technical evaluator, the economic buyer who holds the budget,
procurement and legal for the contract, the data and security, the champion who wants it and carries it inside,
and the blocker. Your list is your own, and a role that appeared in none of your won deals does not enter the
register. A contact can hold more than one role (platform documentation models it that way); the role sits on
the contact at the account, not on the person in general.

**2. Coverage is a count per role.** For each role in the register: does the account have a contact with it;
does that contact have a channel and a basis; were they on a touch, a meeting or a reply, inside the stage's
window. Coverage is the number of roles with a live contact, out of the roles that the won deals of this segment
had covered by this stage. A role enters that set when more than half of the segment's won deals had it covered by
the stage; as a starting point that holds while the window's won deals number enough to read a half, and it is
replaced by your own won share against the coverage of each role. An account with one contact in
the evaluation stage is single-threaded: the deal
lives as long as one person does, and a deal run for months by email with one person is a risk that happened to
work, not a method.

**3. The champion is read by acts, not by title.** The champion is the contact who replies, brings colleagues,
requests material for other roles, names dates. A title does not make one. A single champion who does not decide
is coverage without the economic buyer, and the deal stalls at "waiting for management." Finding a champion is
luck; covering the roles is the plan.

**4. Reach a missing role lawfully.** Four ways, in this order. Through the champion: a request to pass on the
material written for the role and to bring the colleague to the next meeting. A "forward to a colleague" link in
the material itself. An event or a piece written for the role, to which the champion invites. Direct contact
with an address obtained from the champion or found in public, with a notice in the first message of where the
address came from and on what basis (GDPR Article 14(3)(b), `SKILL.md`), inside the recipient's regime: a
corporate subscriber under PECR; a legal person under national law within Article 13(5) of the ePrivacy
directive; under CASL, a conspicuously published address with content relevant to the role, or an address the
person disclosed to you themselves, while an address a colleague handed over carries no implied consent there.
The notice is a duty of transparency, not a basis: the basis for the person is `consent-and-preferences`' and
exists before the first message, or the fourth way is closed and the first three remain. A purchased list is
not a way. The first message to a new role comes from the account executive, not from the program: the program
writes to those already at the account on their own basis.

**5. The register of next steps.** At any moment the account has exactly one next step: the doer
(the program, the account executive, or the customer with the account executive watching), the content, the
promised time. Where several dated items are open at once, a scheduled send, two tasks, a customer's promise, the
next step is the earliest by promised time, and the rest queue behind it. The account executive's step is a task
with a date in the CRM; the program's step is a send with its time; **the customer's step** is an event the
customer promised ("we decide by the fifteenth," "legal returns the contract next week") with a grace: as a
starting point, one working day; that holds for promises with a date, and it is replaced by your own share of
customer promises kept. The timer runs from the promised time, not from an event: "they did not answer by the
date" generates no event on its own. A step without a date is not a step; "reach out later" is not accepted by
the register.

**6. A stall is read against the stage's own distribution.** Every stage has its own median and upper quartile
of idle time with no kept step, from the closed deals of the window. A stall is an account idle in a stage with
no kept step for longer than the stage's upper quartile; that is a starting point, it holds for stages with a
readable number of closed deals, and it is replaced by your own curve of won share against idle time, with the
threshold where the won share halves. The quartile is fixed per version and recomputed with the rebuild of the
retrospective (`qualification-and-handoff.md`, step 9), not continuously: a threshold that follows the idle
times it shortens tightens on its own success and loosens on its own neglect. A stalled account is a signal to
the account executive and their manager, not to the program; the program does not "warm up" a stalled deal on
its own initiative.

**7. What the program does on a stall.** At the account executive's request, and by the code of the silence.
*A role is missing:* material for the role, through the champion (step 4). *A role has a doubt:* a case of the same
industry, a calculation, the answer to that role's objection. *A customer's promise passed:* one step by the
account executive in their own name asking for a new date, not a program email. *No answer from anyone:*
a re-qualification through the champion, is the project alive, did the priority change, and if there is no answer
by that step's promised time, a "not now" return with a date or a "no decision" loss. A discount on a stall is
not the program's instrument: terms are `offer-design`'s, and a discount for silence teaches the buyer to be
silent.

**8. Dates the customer promised are timers.** The budget committee, the tender date, the end of the pilot, the
signing date: each is a customer's step with a grace; passed with no event, it becomes the account executive's
step on the next working day. The grace and that step run on the account's working days, so a dead period
(`sequence-between-touches.md`, step 9) holds the timers and does not cancel them: the promise stands as the
customer made it, and its step lands on the first working day after the dead period.

**9. Close as lost: a code and a re-entry date.** Codes from a closed list: chose a competitor (which one; their
renewal date if known); no budget (the date of their budget cycle); no decision (the project stopped; a review
date by your own median cycle); not fit (into the anti-profile). The re-entry date is required for every code but
"not fit." "Silence" is not a code: silence closes as "no decision" after the re-qualification of step 7. A
partial win, the account buying less than proposed, is not a loss code: the account is a customer, the deal
closes as won,
and the unsold part goes into the record of step 10 as an open opportunity for `b2b-retention`; it does not
re-enter the grid, which is the rule for an existing customer (`qualification-and-handoff.md`, edge cases).

**10. Close as won: the record for `b2b-retention`.** What travels: the roles and contacts with their coverage;
the champion; what was promised and by whom, outcomes, dates and terms, from the proposal and the correspondence;
open promises with their dates, implementation, integration, training; the renewal or contract end date; the
part proposed and not bought, as an open opportunity; the codes of the doubts that were removed; and who at the
account took no part, the roles without coverage, which is the renewal's risk. The record is an object in the CRM on the day of the close; the account manager accepts
it as a handoff with a promised time of a first touch, which is the neighbor's rule. Every pre-deal sequence
stops the same day (`sequence-between-touches.md`).

**11. Read the mechanic.** Coverage by role by stage; the in-step share (`SKILL.md`); idle time by stage against
its median; the share of customer promises kept by their date; loss codes; and the won share by coverage at the
vendor evaluation stage, which tests the role register and arrives a cycle later.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| The role register and "covered by this stage" | the retrospective of the segment's won deals | 4 |
| Grace on a customer's promised time | one working day, as a starting point | 5 |
| Stall threshold | the stage's upper quartile of idle time; replaced by your won share against idle time | 4 and 5 |
| Re-entry date by loss code | their renewal, their budget cycle, your own median cycle | 4 |
| Promised time of the account manager's first touch after a win | `b2b-retention` | the neighbor's |

## Edge cases

- **The champion left the company.** Coverage drops to zero on the champion's role; the deal does not close by
  itself: the account executive's step goes through the remaining contacts; with no contact left, "no decision"
  with a date by your cycle; a new person in the same seat is a new contact, not an heir to the basis.
- **Procurement by tender.** Inside the procurement window the program's touches stand and steps follow the
  procurement's own rules only; the dates of those rules are customer's steps with no grace.
- **Several buying units at one customer.** Each is its own account with its own group; a shared economic buyer
  is a contact at several accounts.
- **A role with no channel.** A contact named as champion with no address: coverage does not count them; material
  goes through the champion.
- **Won, implementation not started.** Open promises go into the won-deal record; the implementation timers are
  `b2b-retention`'s.
- **A "no decision" close, or a "not now" return, to clean the pipeline.** A code or a return with no
  re-qualification behind it is a signal to the manager; the share of "no decision" closes and of "not now"
  returns without a step 7 record is read beside the metric.

## Failure modes

**Single-threaded.** The whole deal hangs on one contact. Sign: coverage of one in the evaluation stage; loss
codes "no decision" and silence dominate; the contact's departure closes the deal. A second cause with the
opposite reading: coverage is high, but every contact is a user and there is no economic buyer; deals reach
approval and lose on "no budget." Remedy: coverage by role, not by headcount.

**Forever "in progress."** A sales stage with no step for months. Sign: idle time above the quartile at a growing
share of accounts; the in-step share falls; cycle length by cohort grows. Remedy: the step with a date as a
required field, the stall signal to the manager.

**The empty step.** "Follow up" with no content is set and kept. Sign: the in-step share is high, the share of
accounts changing stage in the period is low, the share reaching a decision is low. Remedy: a step carries
content and a role; the stage-change share stands beside the metric.

**A date with no timer.** The customer promised, nobody is waiting. Sign: the share of promises with a recorded
date is small; the account executive's steps read "check status" with no date. Remedy: the promised time as a
field of the customer's step.

**A discount for silence.** A stalled deal gets "revived" with terms. Sign: the share of deals with a concession
grows with idle time; buyers have learned the pause. Remedy: a stall closes with a role or a re-qualification;
terms are `offer-design`'s.

**Won with no record.** The account manager starts blind. Sign: the first touches after the deal ask questions
the correspondence already answered; the renewal is lost to a role that was never in the deal. Remedy: the
won-deal record as an object on the day of the close.
