---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Reading answers by the parts of the experience, and closing the loop into the process

The unit here is **the part of the experience**, with the theme as its second axis. A part is what an answer
is attributed to: the store, the courier, the picker, the supplier batch, the shift, the product, the flow and
its message version, the screen, the assignee of a conversation.

The experience record, where it lives and how deep its history goes, is `martech-stack`'s. The report page on
which a score stands beside its response share is `crm-reporting`'s. A hypothesis about a mechanic that came out
of the reading is tested in `experiments-and-holdouts`.

## Entry conditions

Answers are accumulated with keys and instrument versions. Each answer joins a record of the experience, and
that record carries its parts: the order knows the store, the courier, the picker, the batch, the shift and the
items; the conversation knows its assignee and topic; the flow knows the message version. A theme list exists
(step 1), and the reading has a rhythm and an owner.

## Exit conditions

For the period, every part above the readable floor has its excess by theme against exposure. Every theme
taken up has a decision record. Changes are verified on experiences that happened after them. The people who
named a theme received the message about the change. No reading is unversioned.

## Steps

**1. Code every verbatim into themes in the person's words; one list, versioned.** Themes come from a sample of
real answers, not from the organization chart: "the courier left it at the door without ringing," not
"logistics" (the same device as the topic list in `chat-and-bots`). Two axes per answer: the theme and the
part. Sentiment comes from the score, not from the text; a text that contradicts its score (five stars and a
complaint) gets a flag, and the obligation opens on the text (`closing-the-loop.md`). Machine coding is checked
by hand on a random sample each period, sized from the readable floor (step 4). Answers with no key are coded
the same way and read as their own series.

**2. Join each answer to the parts of the experience.** The order record knows the store, the courier, the
picker, the batch, the shift and the items; the conversation record knows the assignee and the topic; the flow
record knows the message version. Attribution to an individual employee comes last: check the batch and the
shift first, because a picker on a shift that received a bad batch will carry that batch's complaints. An
answer about a part delivered by a third party is attributed to the third party and read against the contract
with them, not against your own processes.

**3. Normalize by exposure.** The signal is not the number of answers carrying a theme but a rate: answers
carrying theme X about experiences that contained part P, divided by the period's experiences containing part
P, compared with the same rate on the other parts of the same kind and on the same part in earlier periods. The
same reading in shares: a part's share of the answers carrying the theme against its share of the period's
experiences, its exposure. To take invented numbers: when a product is in four orders out of ten and in four
complaints out of ten, that is the baseline; seven complaints out of ten is an excess. Both forms say the same
thing, that the part's rate is above the rate of the whole; what is never compared is a theme's share among
the answers about one part with that part's share of experiences, which are two different fractions. A part
with no siblings (the site, the app) has an exposure of one
and no siblings: it is read against its own earlier periods and across its own versions, which are its parts of
the same kind. A theme with no part (price) is read as its share among all answers against earlier periods.
Raw complaint counts are never ranked by part: on counts, the biggest store is always the worst.

**4. The readable floor per cell.** A cell is one part in one period. Below the floor, a cell is not read;
periods get pooled, parts do not. The floor follows from the error you accept: for a share, the half-width of
a rough 95% interval is about 1 over the square root of the number of answers, so the floor is set by the
smallest difference you would act on. As a starting point, a few dozen answers per cell per period; that holds
for scales with the spread of a 0 to 10 or a 1 to 5 score, and it is replaced by the floor you compute from
your own smallest actionable difference. A rating of five from one answer against a rating of 4.8 from a
hundred, to take an invented pair, is the same floor said in words.

**5. Priority of a theme is width times depth.** The share of answers that mention the theme, multiplied by
the gap between the mean score of those answers and the mean score of the rest. The cost and the feasibility
of a change are the owner's call and are not in the formula. The order of reading: excess by part first
(where), then priority by theme (what). Signals that arrived on their own (complaints, public reviews, the
topics of issues from `chat-and-bots`) are read beside as an independent series and do not enter the priority
of the asked population: they come from a different population.

**6. The rhythm and the two audiences.** Daily, to the owners of parts: the director of a store gets the
answers about that store and the open obligations with their timers. Once per period, to the owners of
processes and to the program: the excess by part, the priority by theme, the decision records, and beside them,
always, the response share, coverage (answers over experiences), the closed-on-time share and the count of
unidentified negative public reviews. A score does not go up the chain alone: in `crm-reporting` a score
reported by itself is a row of the vanity register, and the response share and the population asked stand
beside it in the same report row.

**7. Baseline and resets.** The baseline of a score and of an excess is the part's own history (a self
baseline). Reset it only on a change of instrument: collection mode, wording, scale, order, delay, carrier or
population. Never reset it on an event the reading exists to catch: a new supplier, a new template, a new store
manager. The overall score moves when the mix of parts changes (more orders from a worse store); split the
change into mix and within-part change, the way `crm-reporting` splits a base-wide change into mix and
within-cohort change.

**8. The decision record.** For every theme taken up: the theme and the part, the excess, the owner, the
deadline, the change and its date, the verification metric (the theme's share among answers about experiences
after the change against before, on the same part), and who gets told. Three numbers inform the choice: how
many people it touches (width), the money at stake (margin, `offer-design` and `crm-program-design`), and the
depth (the score gap). A theme not taken up gets a written "not now" with a review date, the way `segmentation`
treats the remainder and `crm-program-design` treats its queue.

**9. Verify the change on experiences after it, not on the calendar.** Compare answers about experiences that
happened after the change with answers about experiences before it, on the same part; the theme's excess is
expected back at the baseline. When the instrument changed at the same time, or the response share moved, the
reading is not clean. A change to a mechanic (a template, a delay, an offer) is tested in
`experiments-and-holdouts`; a change to a process (picking, storage, a schedule) is verified by the theme's
share. A change declared done whose excess did not fall is not done.

**10. Close the outer loop to the people who raised the theme.** Those whose answer carried the theme get one
message when the change is live: "you told us X; we changed Y." One message, only to those who named it, with
the change stated, with no promotion; a touch under the cap, class automated flow. When the change touches the
question itself, the instrument gets a new version.

**11. Hand over to neighbors.** The person's words and objections go to `email-copy` as raw material; reasons
for not returning go to `repeat-purchase` and `lapse-and-winback` as the reason table; a hypothesis about a
mechanic goes to `experiments-and-holdouts` as a card: the hypothesis, the answers behind it, the success
criterion, how it will be tested; a preference answer (what to receive, how often) is a preference, not a
survey attribute, and goes to the preference center of `consent-and-preferences`; product and supply defects
go to their owners outside this library with the reading by part; themes go into the topic list of the bot in
`chat-and-bots`. The entry signal for referral goes to `loyalty-program-design` as the share of respondents
scoring nine or ten (`metric-definitions`) on the relational ask of the last cycle, on the active base as the
neighbor defines it, read only with the response share above the floor the neighbor sets; a transactional ask
after one purchase reads one experience, not the relationship, and does not stand in for it.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Readable floor per cell | 1 over the square root of n against the smallest difference you would act on; a few dozen answers per cell per period as a starting point | 3 and 5 |
| Size of the hand check of machine coding | the same floor | 3 |
| Priority of a theme | the share of answers mentioning it, times the gap in mean score | 3 |
| Excess by part | answers carrying the theme on experiences with the part, per experience with the part, against the other parts of the same kind and the part's earlier periods; the same as the part's share of the theme's answers against its exposure | 4 |
| Reading rhythm | daily to the owners of parts; once per read cycle of the program to the owners of processes (`crm-program-design`) | the neighbor's |
| Verification window | experiences after the date of the change, until the readable floor is reached | 3 |

## Edge cases

- **A theme with no part** (price, assortment). The owner is a function; the reading is by theme only.
- **A new part with no history** (a new store). Read against parts of the same kind at the same age, the way
  `crm-reporting` reads cohorts at equal age.
- **Season.** Counts grow with volume, which normalization removes, but an excess can be seasonal too: compare
  with the same window a cycle earlier (`promo-calendar`).
- **A part closed mid-period.** Its cell is read up to the closure; no change is verified on it.
- **Several languages.** One theme list by identifier; wording per language.
- **An employee named.** Attribution to the shift and the batch before the person; access limited.
- **An answer not about you** (a competitor, the weather). Tagged out of scope; excluded from priority; the
  obligation closes as out of scope.
- **A theme the business will not fix** (a price above a competitor's, by decision). "Not now" with the
  reason; the people who named it get an explanation, not a promise.

## Failure modes

**The score as a manager's KPI.** The store asks for tens, chooses whom to ask, helps at the tablet. Signs:
the score rises while complaints per order through support and returns do not; the distribution of scores is
bimodal; the response share diverges by store; asks over experiences fall for that store. Remedy: the score
does not enter individual pay without its counterweights (asks over experiences, complaints per order);
sampling and sending are central, and a part does not decide whom to ask.

**Raw counts.** The biggest store is the worst. Remedy: exposure.

**The person blamed before the batch.** A picker dismissed for a supplier's roses. Sign: the excess coincides
in time across every picker on the shift. Remedy: the order of attribution, batch and shift before the person.

**Themes from the organization chart.** "Logistics" hides "left at the door without ringing." Sign: themes
with no change anyone could make. Remedy: the theme list from a sample of answers.

**A decision with no verification.** The change is declared; the excess did not fall. Sign: the same theme
with the same excess in the next period. Remedy: step 9.

**The outer loop never closed.** People see nothing changed. Sign: the response share among earlier
respondents falls faster than among new ones. Remedy: step 10.

**An instrument change read as a change in the experience.** Moving from calls to self-completion moved the
score. Remedy: a new baseline; collection modes read apart.
