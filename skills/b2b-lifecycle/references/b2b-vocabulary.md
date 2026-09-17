---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-14
---

# Vocabulary of the pre-deal account

The three mechanics assume these terms. Four of them are units. When marketing and sales disagree about a lead,
check first whether one of them means the contact and the other the account, or whether one means a signal and
the other the grade the signal moved. Several words are shared with neighbors, and those are marked at the end.

## The units

**Account.** The buying organization, or the buying unit inside it that you define: a legal entity, a division,
a site. The unit of the grade, the stage, the next step and the control metric. Not a user's login in the
product.

**Contact.** A person at the account, with a key and a channel. Consent, the cap and suppression sit on the
contact. In `list-building` a contact is a record with an address; here a contact is always attached to an
account.

**Signal.** An observed act of a contact, or a fact about the account, that changes the reading of readiness.
Three classes: declared (an answer), behavioral (a visit, an open, an attendance, an activation event), and
structural (a new role, a new contact from the domain, a request from a role with authority). In
`onsite-capture` a readiness signal opens a capture point on the site; here a signal moves the account's grade.

**Next step.** The one thing owed to the account next: the doer, the content, the promised time.
The program's step is a send; the account executive's step is a task with a date; the customer's step is an
event the customer promised, with a grace.

## People and seats

**Account executive.** The salesperson who holds the account from acceptance to the decision. In most CRMs the
field is called the account owner; this library counts the senses of "owner" in `crm-program-design`, so the
sales term is used. After the deal the seat is the account manager (`b2b-retention`, `chat-and-bots`).

**Role.** A contact's place in the account's decision: user, technical evaluator, economic buyer, procurement
and legal, champion, blocker; the list is yours, derived from your own won deals. The role sits on the contact
at the account, and a contact can hold more than one.

**Champion.** The contact who carries the deal inside: replies, brings colleagues, requests material for other
roles, names dates. Read by acts, not by title.

**Coverage.** The number of the account's roles with a live contact (channel, basis, a touch inside the window),
out of the roles that more than half of the segment's won deals had covered by this stage.

## Grading and the handoff

**Fit.** The account's tier by the traits that occur more often among won deals than among lost and removed
ones; three steps; a disqualifier gives zero. A property of the account, carried with a version.

**Intent.** The account's step by the contacts' signals, weighted from the retrospective and decaying over the
stage's window; aggregated by the maximum of a role, not by the count of people.

**Grade.** The cell of fit tier by intent step, with its date and the grid's version.

**Handoff threshold.** The set of cells at which the account is handed to sales: an agreement of both sides,
with its version, the route, the promised time of acceptance, and the lists of what travels and what comes back.

**Handoff.** The program passing an account to sales, with the handoff record. In `chat-and-bots` a handoff is
the bot passing an issue to a person; the same word for a different act, marked on both sides.

**Handoff record.** An object in the CRM: the tier with its traits, the contacts with roles, the verbatim answers
with dates, the signals of the window, the source and promise of the first contact, and the next step with its
promised time.

**Acceptance.** An event: sales accepted the account by the promised time, or did not, with a code from a closed
list. The industry calls an accepted account a sales accepted lead.

**MQL, SAL, SQL, PQL.** The industry's names for stages: an account above the handoff threshold; one accepted by
sales; one confirmed by sales as ready for a proposal; one confirmed by its behavior in the product. Names of
stages here, not units.

**Return.** An account sent from sales back to the program: "not now," with a re-entry date; "no answer," with a
flag; "never," a disqualification with a review date.

**Disqualification.** Removing an account from the grade for a reason, with a review date set by the reason's
lifetime. The contacts stay under their own basis.

## Stages and the sequence

**Stage.** The account's state in the cycle: by the grid before the handoff, by the CRM after it. Each stage has
an ownership class and a median duration of its own. In `crm-reporting` a stage share is the share of a cohort
that reached the stage by an age.

**Ownership class.** Who writes to the account in a stage: the program; the account executive, with the program
limited to an allowed set; or shared, with one queue of touches.

**Sequence.** The program's ordered touches to one account in one stage, each with an exit signal and a recheck
before sending. One per account. Not a thread, which in `chat-and-bots` is the tool's container of messages.

**Account cadence.** The number of program touches an account receives per window across all its contacts, with
the account executive's touches in the same queue. Runs on top of the cap per person
(`contact-orchestration`, which names the second cap on the account) and is checked after it.

**Dead period.** A stretch of the buying organization's calendar in which touches and timers stand: the end of
its fiscal year and quarters, vacations, trade shows, a procurement window.

## Steps, stalls and closes

**Promised time.** The time of the next step; for the customer's step, the time the customer named, with the
grace running after it. The same timer as in `transactional-messaging` and `voice-of-customer`, in the other
direction: there the organization names the time to the person; here the customer names it to the account
executive, or sales names it to the program.

**Grace.** The time after an event the customer promised, past which the step counts as missed.

**Stall.** An account idle in a stage with no kept step for longer than the stage's threshold. An event for the
account executive and their manager.

**In step.** The account's state for a period: no step missed in the period and a next step recorded at its
end; for an account that closed or was returned in the period, no step missed before the exit and the exit's
record in place, a close code or the return's kind and date.

**Close code.** The reason for a loss, from a closed list, with a re-entry date. Silence is not a code.

**Won-deal record.** The object handed to `b2b-retention`: roles and coverage, the champion, the promised
outcomes and dates, open promises, the renewal date, the roles without coverage.

## Words shared with neighbors

**Handoff:** with `chat-and-bots`, in a different sense, marked on both sides. **Promised time:** with
`transactional-messaging` and `voice-of-customer`, the same timer, named by the other side. **Coverage:** in
`voice-of-customer` answers over experiences, in `segmentation` the share of the base falling into at least one segment of a set,
in `program-audit-and-ops` a coverage hole is a stage no mechanic touches; here, roles with a live contact.
**Signal:** beside the readiness signal of `onsite-capture`. **Stage:** with `crm-reporting`, one object, read
there as a cohort share. **Activation:** `welcome-and-activation` defines the event; here it is a signal.
**Deduplication** is not used in this skill:
merging records of one person is `list-building`'s, not repeating an argument in a second channel is
`contact-orchestration`'s, and attaching contacts to an account is called attachment.
