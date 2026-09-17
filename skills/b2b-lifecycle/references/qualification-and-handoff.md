---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-14
---

# Qualification and the handoff: fit, intent, the threshold, the record, acceptance, the return

The unit here is **the account against the handoff threshold**. The program decides: hand over, hold, return,
or remove.

The contact's basis for being written to is `consent-and-preferences`'; the cap per person is
`contact-orchestration`'s and is checked first. The qualifying bot's script and the fields it collects are
`chat-and-bots`' and `onsite-capture`'s; their answers arrive here as declared signals. The activation event of a
trial is defined in `welcome-and-activation`; here it is a signal. What happens after acceptance is in
`buying-group-and-stalls.md`; what happens after a return is in `sequence-between-touches.md`.

## Entry conditions

- A contact exists with a key, a channel and a basis for messages (`consent-and-preferences`; for a corporate
  recipient the basis is the question of recipient type in `SKILL.md`).
- The contact is attached to an account: by domain, by a company field, by an answer in a form, by a CRM record.
  A contact without an account is raw, and the first job is attachment rather than grading (step 1).
- Sales has named who accepts a handoff and has agreed to a promised time for acceptance (step 5). Without that
  the threshold does not run: a handoff with no receiving side is a mechanic without a second half.

## Exit conditions

The account was accepted by sales (a sales stage, `buying-group-and-stalls.md`); or returned to the sequence
with a re-entry date (`sequence-between-touches.md`); or disqualified with a review date. The handoff record sits
in the CRM as an object; the grade and its version sit on the account; the signals sit in the contact log.

## Steps

**1. Attach the contact to an account, and the account to a buying unit.** The domain of the address is the
default key for corporate mail; a public mailbox domain gives no account, and then the company field of the
form, the bot's answer, or a manual attachment by the account executive does. The buying unit is what makes one
decision: in a group it is a division or a site, in a chain the head office; you define it once and write it into
the vocabulary of your own program. `list-building` merges records of one person; here contacts are attached to
one account, and that is a different join with a different key, so the two are not called by one name. A
contact from a training project, a competitor or an agency working for several clients attaches to its own
account, not to the client's.

**2. Read fit on the account, from your own won deals.** Not a list of traits from somebody's page but a
retrospective: over a window of two to three of your own median cycles, which account traits occur more often
among won deals than among lost and removed ones. The candidates are industry, size measured by the number of
people who would use the product, the presence of a role that can use it, the stack and the integration it
needs, requirements on localization and security, country and legal regime. Disqualifiers are traits under
which the product cannot be applied at all, such as no website for a vendor of a site chat: zero fit whatever
the intent. The anti-profile is the set of traits of accounts that bought and left; ask implementation and
support, they know them by name. Fit is a tier, three steps as platform documentation does it (a strong match,
an acceptable one, a low priority), rather than a score: tiers get revised by version, and a score invents a
precision the retrospective did not give.

**3. Read intent on the contact, aggregate it to the account, and let it decay.** Signals come in three classes.
*Declared:* answers to strong questions in a form or a bot, such as role, size, the task, the horizon, the
current solution, a budget as yes, no or unknown. *Behavioral:* pricing and comparison pages, a return to the site
after a sales touch, a proposal opened, a demo booked, an event registered and attended, an activation event in
the trial. *Structural:* a second contact from the same domain, a role that appeared, a request from a role with
authority. The weight of a signal comes from the retrospective: a strong question is one whose answer variants
differ in won share by at least the minimum detectable effect, as `experiments-and-holdouts` sets it; below it
the question stays a field and does not become a weight. Decay: a signal loses its weight over a window equal to the median
duration of the stage the account stands in. An unsubscribe or a "not interested" is a negative signal on the
contact, not on the account. Aggregation to the account takes the maximum by role rather than the count of
people: three interns reading the blog do not equal one head of department on the pricing page.

**4. The grade is a cell of fit tier by intent step, with a version.** Tier by step gives a grid; the handoff
threshold is a set of cells agreed with sales. Two cells get routes of their own. A strong fit with no intent is
a target for outbound work outside this library, and stays in the sequence meanwhile. A weak fit with high intent
is a raw request: answer it on its merits and do not hand it over until a role or a fit trait appears. The grade
lives on the account with its date and the grid's version.

**5. The handoff threshold is an agreement, written as a version.** Sales and the program choose the cells from
the retrospective: in which cells did the won deals stand at the moment of their handoff. With the cells the
agreement records **who accepts** (the route: by territory, by segment, by rotation), **the promised time of
acceptance** (a parameter of the agreement; as a starting point, by the end of the next working day for a
handoff on the grade, and within the same working hour for an inbound request for a demo or a quote, where the
person is waiting for an answer as a consequence of their own act; that holds for requests arriving in the
receiving side's working hours, a request outside them is owed within the first working hour of the next window,
and both are replaced by your own curve of acceptance and reply share against delay), **what travels** (step 6)
and **what comes back** (step 8). The agreement is revisited at a regular
meeting of both sides on two numbers: the share accepted and the share returned by reason. A threshold under
which everything is accepted, or nothing is, is a defect of the agreement, not of sales.

**6. The handoff record.** What travels: the account and its fit tier with the traits it was built from; the
account's contacts with roles and channels; the answers, verbatim, with their dates; the signals of the recent
windows, pages, returns, events, proposals opened; the source of the first contact and the promise it was
exchanged for (`onsite-capture`); and **the next step** sales owes, with its promised time. What sales may not
re-ask: anything in the record. The contact has already answered, and a second asking reads as "they do not
listen"; the questions a salesperson used to ask by phone belong in the form, so that the salesperson
prepares instead of asking. The record is written into the CRM as an object attached to the deal rather than as
an email to the salesperson: an email gets lost, an object stays with the deal.

**7. Acceptance is an event with an outcome.** Sales accepts, or does not, by the promised time. Not accepted
carries a code from a closed list: not fit on a named trait; not the role; a duplicate of an existing customer
or of an open deal; unreachable, the address is dead; outside the territory; a competitor. Accepted means the
first human touch by its promised time, written as the next step (`buying-group-and-stalls.md`). A promised
time that passed with no outcome is a duty signal (`program-audit-and-ops`): a handoff lying unaccepted is a
silent object, not a healthy one.

**8. The return has three kinds, each with its own continuation.** *"Not now"* comes back with a re-entry
condition and a date: the budget date, the end of the current contract with a competitor minus your own median
cycle, the project's horizon. The account goes into the sequence under its stage, the grade freezes until the
date, signals keep accumulating; the re-entry into the grade on the date is the program's own step, and a date
that passed with no re-entry is a duty signal (`program-audit-and-ops`). *"No answer"* comes back after the number of attempts written in the agreement,
with a flag; the sequence changes channel and content, because the person who does not pick up the phone still
reads; a second handoff happens only on a new structural signal, a new role or a request, not on the sum of old
ones. *"Never"* is a disqualification with a reason and a review date set by the reason's own lifetime, such as
a stack change or growth past a size; the contacts stay in the base under their own basis, the account leaves
the grid. A return twice on the same reason is a request to revise the fit trait, not a third handoff; "twice"
is a starting point that holds for fit reasons and is replaced by your own won share among re-handed accounts.

**9. Rebuild the weights and the cells from the retrospective.** Once per window equal to your own median cycle,
and earlier on an outside signal such as a new product, segment, channel or price plan: for every strong question
and trait, the won share by variant on the closed deals of the window; weights whose difference stopped being
readable come off; a new grid version carries its date, and old grades are not recomputed in hindsight (stage
reports by version are `crm-reporting`'s).

**10. Read the instrument.** The share handed over by cell; the share accepted and the codes of non-acceptance;
the time to acceptance and to the first touch; the share returned by kind; and the won share by cell at the
moment of handoff, the reading that tests the grid, which arrives a cycle later.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Retrospective window for fit traits and weights | two to three of your own median cycles as a starting point; holds while product and segment are stable; replaced when your own shares drift | 4 and 5 |
| Minimum detectable effect between answer variants | `experiments-and-holdouts`' rule | the neighbor's |
| Decay window of a signal | the median duration of the current stage | 4 |
| Promised time of acceptance | the agreement with sales; starting points: by the end of the next working day; within the same working hour for an inbound request, or the first working hour of the next window outside working hours | 4 and 5 |
| Attempts before "no answer" | the agreement with sales | 4 |
| Re-entry date of a "not now" | the condition: budget date, contract end minus your cycle, project horizon | 4 |
| Review date of a disqualification | the lifetime of the reason | 4 |
| Returns on one reason before the trait is revised | twice, as a starting point; fit reasons only; replaced by your won share among re-handed accounts | 5 |
| Rebuild window for weights | your median cycle; earlier on an outside signal | 4 |

## Edge cases

- **One person is the whole company.** An owner-operator, a sole trader: the account and the contact coincide;
  fit and intent are read on one object; the recipient type is an individual subscriber under PECR, not a
  corporate one (`SKILL.md`).
- **The contact left the company.** A bounce saying "no longer works here," an auto-reply: the contact is
  suppressed as unreachable (`deliverability`, `list-building`); the account keeps its stage and grade; coverage
  drops, which is a next step in `buying-group-and-stalls.md`, not a disqualification.
- **One person at two accounts.** A consultant, an agency: fit per account; intent aggregates to the account the
  signal is about, the page or the answer; the cap on the person.
- **The account is already a customer.** A request from a new contact at an existing customer is expansion and
  goes to `b2b-retention` through the account manager; a new deal is handed to sales only where the customer has
  a separate buying unit.
- **An inbound request from a student, a competitor, a job seeker.** Zero fit, high intent: answer on the merits,
  do not hand over, write the trait into the anti-profile.
- **A partner or reseller as an account.** A grid of its own: fit by the partner's channel rather than by end
  use; the partner's deals are not its intent.
- **A public or regulated buyer with a formal procurement.** The threshold still applies; the procurement window
  and the quiet inside it are a stage of `buying-group-and-stalls.md`.
- **Bought without sales.** Self-service converted the account inside the sequence: a win without a handoff; the
  won-deal record for `b2b-retention` is written all the same (`buying-group-and-stalls.md`, step 10).
- **A purchased or scraped address.** This skill gives it no basis (question 5 of the map, `SKILL.md`); the contact
  is outside the grid until a basis exists.

## Failure modes

**Everything qualifies.** The program reports the count handed over; the threshold slides to "downloaded
anything." Sign: the acceptance share falls, non-acceptance codes "not fit" rise, the time to the first touch
grows because sales is drowning. A second cause with the opposite reading: sales accepts everyone on paper and
touches no one; the acceptance share sits near one, the time to the first touch grows, the won share by cell
falls in every cell at once. Remedy: the threshold by version from the retrospective, and acceptance as an event
with an outcome rather than as a stage change.

**Nothing qualifies.** Sales rejects whatever did not come from the pricing page. Sign: the share handed over is
small while signals on accounts rise; "not now" returns come back without dates. Remedy: the cells from the
retrospective of won deals; if the won deals came from cells that are not handed over, the agreement is wrong.

**The grid was trained on survivors.** Weights were derived from won deals without the lost and removed ones,
and every trait of the winners looks predictive. Sign: the weights coincide with a description of the base; the
won share does not differ by cell. Remedy: the denominator from all closed deals of the window.

**No decay.** An account that collected its signals long ago stands in the top cell. Sign: the age of the
signals on handed accounts grows; "unreachable" and "no answer" rise. Remedy: the decay window by stage.

**Acceptance is not recorded.** A handoff is a stage change and nobody confirmed. Sign: the acceptance share is
exactly one or exactly zero; the time to the first touch is unmeasured. Remedy: acceptance as an event with a
promised time and a code.

**A return without a date.** "Not now" goes to the archive. Sign: the share of returns with a re-entry date is
small; accounts re-enter the grid only on a new request. Remedy: the date as a required field of the return.

**The record gets re-asked.** The salesperson asks the form's questions again. Sign: "we already told you"
replies; the share replying to the first touch falls while the time to reply grows. Remedy: the record as an
object on the deal, with the verbatim answers in it.
