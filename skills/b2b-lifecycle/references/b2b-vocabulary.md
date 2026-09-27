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

## What sets this work apart

Three properties make this work unlike its neighbors.

1. **The one who reads is not the one who decides, and the one who decides is several people.** A contact acts:
   opens, returns, replies. An account decides. Every reading runs on two objects at once. Fit is a property of
   the account; intent is an act of a contact, aggregated to the account; consent, the cap and suppression stay on
   the person (`consent-and-preferences`, `contact-orchestration`). A grade computed on a person grades whoever
   was told to submit the request (`rfm-segments` says the same of its grid: cut it on the account, choose the
   recipient separately).
2. **Two hands hold one account in time.** The program and the salesperson take turns, and who
   writes in which stage is a construction rather than a courtesy. Between sales touches the account is silent by
   default, and silence is the failure this skill exists against: every account past the handoff carries a **next
   step** with a doer and a promised time, and the timer runs from the promised time rather than
   from an event.
3. **The decision has a calendar, and it is not yours.** Budget cycles, quarter ends, procurement windows, dates
   the customer promised: timers run from those, not from send dates (`promo-calendar` hands the budget cycle of
   the buying organization here as a construction).

Two words are not used here. The salesperson who holds the account before the deal is the **account executive**;
in most CRMs the field is called the account owner, and this library counts the senses of "owner" elsewhere
(`crm-program-design`), so the sales term is used instead. After the deal the same seat is the account manager
(`b2b-retention`, `chat-and-bots`). The program's ordered touches to one account are its **sequence**, not a
thread: in `chat-and-bots` a thread is the tool's container of messages.

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

## Seams with neighbors

Seven seams get crossed by accident, so state them outright.

- **The grade is on the account; the basis is on the person.** Fit and intent are read on the account. Whether a
  given contact may be written to at all is the neighbor's question (`consent-and-preferences`), and a contact's
  objection removes that contact's signals from the grade without touching the account's fit.
- **The cap is the neighbor's; the account cadence is this skill's.** `contact-orchestration` caps touches per
  person and checks it first; its policy names a second cap on the account for B2B, and its inventory counts load
  on the company beside load on the person. The value of that second cap and the rule over it, one sequence per
  account with the salesperson's touches in the same queue, follow from the buying group and live here
  (`references/sequence-between-touches.md`, step 5).
- **The activation event is the neighbor's; reading it is this skill's.** `welcome-and-activation` defines the
  activation event and runs the series toward it. Here the event is a signal into the grade, and "trial ending"
  at a fit account is the account executive's next step, not a discount email.
- **The bot qualifies; the program grades.** `chat-and-bots` collects answers and passes an issue to a person. The
  answers are declared signals here; the handoff in this skill is the program passing an account to sales, a
  different act with the same word, marked in both vocabularies.
- **Stage shares are read by the neighbor; stage ownership is set here.** `crm-reporting` reads stages on a
  cohort at their settling age. Which stage the program may write in, and the stage's own median duration, are
  set in this skill.
- **The meeting confirmation is a service row; the material before the meeting is a touch.** The confirmation
  and the "please confirm" belong to the service register of `transactional-messaging`. The plan and the
  materials sent before the meeting count as program touches under the cadence.
- **The salesperson's touch is a step in the register, not a message of the program.** The program never
  writes in the account executive's name what the account executive did not ask for; a proposal opened with no
  reply is the salesperson's timer first.

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
