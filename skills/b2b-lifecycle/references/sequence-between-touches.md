---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-14
---

# The sequence between touches: who writes in which stage, what, to whom at the account, and when to stop

The unit here is **the account in a stage**. The program decides what to send, to which contact, and when to
stop; the stage is set by the account executive or by the grade.

The form of a step, its firing event, eligibility, delay, recheck before sending and expiry, is
`triggered-messages`'. The cap per person
and the moment it is checked are `contact-orchestration`'s. The regular newsletter an account falls into after
its sequence ends is `email-program`'s. Price and terms in any message are `offer-design`'s. The activation event
and the series toward it are `welcome-and-activation`'s. The register of next steps that this sequence answers to
in a sales stage is in `buying-group-and-stalls.md`.

## Entry conditions

- The account has a stage, from the grid of `qualification-and-handoff.md` or from the CRM after the handoff,
  and at least one contact with a channel and a basis.
- The stage is assigned to one of three ownership classes (step 1). Without a class the sequence does not start:
  nobody knows whether writing is allowed.
- The sequence has content for the stage and the role (step 2) and an exit signal on every step (step 3).

## Exit conditions

The stage changed, so the stage's sequence closes and the next one starts by the new stage; the account was
handed over and accepted; the account closed as won, which stops every pre-deal sequence the same day, or as
lost, which starts the after-loss sequence with its re-entry date; the account was disqualified or suppressed; a
contact withdrew their basis, which stops that contact only.

## Steps

**1. Assign stages to ownership classes.** Three classes. *The program's:* before the handoff and after a return;
the program writes, the account executive receives signals. *The account executive's:* from acceptance to the
decision; the account executive writes, and the program writes only from an allowed set, events, material for a
role, meeting reminders, replies to signals, and nothing with a price in it. *Shared:* the evaluation and
selection stages, where the account executive assigns roles and requests material, and the program sends it by
rule. The rule of a shared stage: the account has one queue of touches, the account executive's and the
program's stand in it together, and the program does not send a step when the account executive touched the
account inside the cadence (step 5). The stage list comes from your own CRM, not from somebody else's page:
derive it from the retrospective of won deals, the states every one of them passed through, and a stage with no
median duration of its own is a note, not a stage.

**2. Content by decision stage and by role, from the map of doubts.** The buying organization's stages of
decision: framing the problem, weighing the kinds of solution, evaluating vendors, approval and procurement. Roles
come from `buying-group-and-stalls.md`. At each crossing sits a doubt and what removes it, and that table is the
content plan: while framing, analyses of the task with no product in them; while weighing kinds, comparisons of
approaches and the criteria of choice; while evaluating, cases of the same industry and size, calculations,
answers to the objections of each role (integration and security for the technical evaluator, payback and risk
for the economic buyer, "what Monday looks like" for the user, contract, data and compliance for procurement
and legal); during approval, what the account executive asks for. Every message reads on its own with links to
the key materials: a series is read by different people at the account, and one message will be forwarded to a
manager out of context. Price and terms appear only in the program's stages and only from `offer-design`.

**3. Every step exits on a signal, not on a count.** A step is defined as `triggered-messages` defines one:
firing event, eligibility, delay, and a **recheck before sending**: the stage is the same, the account was not
handed over, the account executive did not touch it inside the cadence, the contact did not withdraw their basis,
the account has no open issue about a problem (`chat-and-bots`), and no dead period is running. The exit signal of a step is the stage's own
target act, a demo requested, a reply, a registration, rather than "three emails sent." The stage's sequence is
finite: after its last step the account moves to the regular program of `email-program`, in the engagement tier
its response puts it in, and stays in the grade, where signals keep accumulating.

**4. To whom at the account.** The recipient of a step is the contact whose role the step was written for; with
one contact, that one; with several, by role, and one step does not go to two contacts of the same account
inside one cadence window (step 5). Material for a role that is not among the contacts goes to the champion with
a request to pass it on (`buying-group-and-stalls.md`, step 4), not into the void. The recipient is chosen at
send, not when the segment is built (`contact-orchestration`: the moment the cap is checked).

**5. The account cadence.** The cap per person is `contact-orchestration`'s and is checked first. On top of it
runs the account cadence: how many program touches the account receives per window across all its contacts
together, with the account executive's touches counted in the same queue. One account runs one sequence, whoever
its contacts are, so in the program's stages the cadence is the sequence's own interval between steps. In the
account executive's and shared stages, as a starting point, one program touch per account per working week;
that holds for evaluation and approval stages, and it is replaced by your own reply share and the share of "too
many emails" objections per cadence version. `contact-orchestration` names a second cap on the account in its
policy and counts load on the company in its inventory; the value of that cap and the rule over the count live
here, because they follow from the buying group.

**6. Events as steps of the sequence.** A registration is a declared signal carrying a role and a company; on
those you select who gets a seat at an event with limited places. Reminders run from the recorded time of the
event, a dynamic delay: the day before, the agenda and the materials; hours before, a reminder that asks for
confirmation; minutes before, the link. Those three are starting points; they hold for an event the person
registered for themselves, and they are replaced by your own attendance share per reminder version. Of the
three, the agenda with the materials is a touch under the cadence; the confirmation ask and the link are service
rows, as for a meeting (step 7). Not confirmed for an in-person event moves the person to the online branch. After the event, three branches by what
happened: *attended,* the material on the topic and a step by the account executive if the role has authority;
*registered and did not attend,* the recording and one step, not two; *watched the recording,* as attended, with
the delay of the viewing. A registration without attendance does not count as intent; it is a declared signal
whose weight the retrospective sets.

**7. Meetings with the account executive run the same reminder chain,** from the recorded meeting time: the
agenda and the materials, the reminder with a confirmation ask, the link. An unconfirmed meeting is a signal to
the account executive before it starts, not after. The confirmation of the booking is a row of the service
register of `transactional-messaging` (a confirmation of what the person set in motion), not a touch; so are the
"please confirm" and the link; the material "for the meeting" is a touch.

**8. After a sales touch, the follow-ups run by rule.** A proposal sent and opened with no reply by the time the
customer promised: the program has nothing to do, the timer is the account executive's
(`buying-group-and-stalls.md`). Opened with no reply after the window written in the agreement, your own median
time to a reply on a proposal: one step of the program, an invitation to discuss with a date, sent in the account
executive's name and by the account executive's rule. The summary after a demo is written by the account
executive; the program sends the materials the summary promised, as the account executive's task. No step of the
program after a sales touch carries a price.

**9. Dead periods.** The buying organization's calendar, not yours: the end of its fiscal year and quarters,
vacation troughs, trade shows, and for public buyers the quiet inside a procurement window (`promo-calendar`
hands the axis here). In a dead period the sequence stands and the stall timers of `buying-group-and-stalls.md`
do not run. A promise the customer made stands as they made it; the grace and the account executive's step after
it run on the account's working days, so a promise that passes into a dead period gets its step on the first
working day after it. The calendar sits on the account, because different customers
have different fiscal years; as a starting point it comes from industry and country, and it is replaced by your
own reply data by week of the year.

**10. The trial as a stage input.** Trial states, active, passive, setup unfinished, period ending, are inputs to
the stage rather than a sequence: the series toward the activation event and the nudges inside the product are
`welcome-and-activation`'s and `in-product-messaging`'s. Here the activation event is a signal into the grade;
"period ending" at a fit account is the account executive's next step, not a program email with a discount; at
an unfit account it is the expiry notice and self-service.

**11. A signal to the account executive instead of a message.** In the account executive's stages a return of a
contact to the site, a proposal opened, a new contact from the domain is not a reason for a program step but a
signal to the account executive the same day, saying what the contact did and which role they hold. A daily
digest of "your accounts visited" is the usual carrier.

**12. After a loss.** A lost account, with its close code and re-entry date (`buying-group-and-stalls.md`, step
9), goes into the after-loss sequence: no price, materials by the reason (chose a competitor: what sets you
apart, timed to their renewal date; no budget: timed to the start of their budget cycle; no decision: by signal).
The cadence is slower than before the deal: as a starting point, no more than one touch per your own median
cycle; that holds for losses with a date, and it is replaced by your own share of accounts returning to the
grade. The return to the grade happens on a structural signal or on the date.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Ownership classes of stages | the agreement with sales; the stages themselves from your CRM by retrospective | 4 |
| Account cadence | one sequence per account; in the program's stages the sequence's own interval; in the account executive's and shared stages one program touch per account per working week, as a starting point | 4 and 5 |
| Event and meeting reminders | the day before: agenda; hours before: confirmation; minutes before: link, as starting points | 5 |
| "Proposal opened, no reply" window | your own median time to a reply on a proposal; the agreement | 4 |
| Dead periods | the buying organization's calendar; industry and country as a start; your own reply data by week | 4 and 5 |
| Cadence after a loss | no more than one touch per your own median cycle, as a starting point | 5 |
| Length of a stage's sequence | by the exit signal; finite; the tail is the regular newsletter | 4 |

## Edge cases

- **Two contacts in two stages.** One contact of the account is in a program stage, subscribed to the blog; the
  other is in a sales stage. The stage is one and belongs to the account: the sales stage takes precedence; the
  blog contact receives the newsletter, not the sequence.
- **The account executive is on vacation.** An account in a sales stage with no touches keeps its stall timer
  running; a substitute named by the handoff route (`qualification-and-handoff.md`, step 5) takes the account
  executive's steps for the time, and the relationship key that `chat-and-bots` routes by points at the
  substitute for the same time.
- **A contact asks to be written less.** A preference of the person (`consent-and-preferences`) sits on the
  person; the account cadence stays, and steps go to another contact of the role or to the champion.
- **The account asks that nobody be written to.** A request from a role with authority: a suppression on the
  account with the scope "program touches"; the account executive's correspondence on an open deal is not a
  touch; the scope is a row for `consent-and-preferences`.
- **An open issue.** The account has an open issue about a problem (`chat-and-bots`): the sequence stands until
  it closes; a signal to the account executive.
- **Weekends and off hours.** A step does not go out when sales and support are not answering: sends run in the
  receiving side's working window, in its time zone.
- **A considered purchase by one person.** Real estate, education, a car: the unit is the person as their own
  account; the decision stages and the sequence are the same; the buying group is the household, so
  `buying-group-and-stalls.md` applies in part, with the roles of payer and user.

## Failure modes

**The sequence outlived the deal.** A won account keeps receiving "why choose us." Sign: program touches after
the won date; complaints from the account manager. A second cause with the opposite reading: the stop fired on
the close, the deal was lost, and after the loss there is silence: zero touches, zero returns to the grade.
Remedy: exit by stage with a branch for won and lost.

**Two contacts, two sequences.** The technical contact gets the economic buyer's material, the head of
department gets the integration guide; or both get the same thing on the same day. Sign: steps with identical
content to one account inside one window; unsubscribes inside one account after one day. Remedy: the recipient
by role at send and the account cadence.

**The sales stage as silence.** The account executive "has" the account, the program is quiet by rule, the
account executive does not touch it. Sign: accounts in sales stages with no touch for longer than the stage's
median; the in-step share falls. Remedy: the next step with a promised time as a required field of the stage
(`buying-group-and-stalls.md`), and the signal to the account executive on a return.

**Content not by stage.** An account still framing its problem gets calculations and cases. Sign: replies and
clicks by stage are lower in early stages than in late ones at the same cadence. Remedy: the map of doubts by
stage.

**An event read as intent.** A webinar registration counted as readiness, and the account was handed over. Sign:
non-acceptance codes "not the role" and "no answer" among accounts handed over after events. Remedy: the branch
by attendance, the weight from the retrospective.

**A pause with no reason.** A dead period declared for the whole base by your own calendar. Sign: for customers
with a different fiscal year, silence in their live period. Remedy: the calendar on the account.
