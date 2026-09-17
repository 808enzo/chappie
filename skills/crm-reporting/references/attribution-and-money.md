---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-13
---

# Money in the report: credit, cause, and the attribution model

The unit here is **the conversion and its credit**. Here you decide which question a money line answers,
which model computes it, what window and anchor the model uses, what is excluded from credit, and what stands
beside the figure. The conversion key, the credit rule and whether channel figures add up are written into the
definition (`metric-definitions`); a control group is built and read in `experiments-and-holdouts`.

## Entry conditions

The report names money the program "brought"; channels compete for budget on credit; attributed revenue and a
holdout read disagree; the model is about to change.

## Exit conditions

Every money line names its question. One model per decision, with a window derived from your own lags, a named
anchor and a list of exclusions. Channel lines deduplicated, with double credit on a line of its own. The
unidentified share published. The incremental figure beside the attributed one wherever a holdout exists, and
the attribution multiple read per channel.

## Steps

**1. Name the question each money line answers.** Three questions need three instruments:

- how much came through a channel (credit): an attribution model;
- how much would not have come without it (cause): a control group (`experiments-and-holdouts`);
- how to split a budget across channels: one model for every channel competing for that budget, plus a cause
  check on the largest of them.

A line called "revenue from CRM" says which question it answers. Never label an attributed figure "effect".

**2. Choose the model for the decision, and keep one model per decision.** Every channel competing for the same
budget reads on the same model: a channel on a model of its own compares to nothing, and moving one channel to a
new model means moving all of them. `metric-definitions` names the method in force; you make the choice here.

| Decision | Model | Check |
|---|---|---|
| Which step or touch of a flow to keep | last touch inside the flow, window from your lags | a local control group on the step |
| The budget across your own channels | one rule for every channel, deduplicated | the global control group, and the attribution multiple per channel |
| Whether the program pays at all | no model answers it | the global control group |
| A long cycle with the sale offline | a window from the send, matched by identifier | incremental reads by stage |

A rule that weights touches by position has weights nobody can verify, and every team argues for the position
its own channel holds: use one only with the agreement written down and a control group checking it. A model
trained on your data needs volume and a long history; without both, do not use one. Record the model, window,
anchor, conversion key, exclusions and version date.

**3. Derive the attribution window from your own lags.** For conversions that followed a touch, take the time
from touch to conversion. Compare it with people who got no touch: the control group, or the same population in
a period with no send. The untouched people met the same condition as the touched: for a trigger, people who
abandoned a cart and got no message, not the whole base, whose lower rate would stretch the window over the
decay of the intent itself. The window ends where the daily conversion rate of touched people falls to the rate
of untouched ones. Without a control, start with the point where your own lag distribution levels off; that
holds where the purchase cycle is stable, and you replace it at the first control group read. A touch that
reaches the same person again before the lag tail has run out (a daily trigger, a daily digest) cuts the lag
distribution at its own cadence: every conversion falls within one cadence of some touch, the distribution
levels off at the cadence, and the window it gives measures how often you send. Such a channel gets no window
from lags; hold out a share of the people it fires on (`experiments-and-holdouts`), and until that read its money line
says that the window equals the send cadence and was not derived. A window longer than the purchase cycle
credits the touch with purchases the person was going to repeat anyway. Keep the window shorter than the
reporting period; where your lags run longer, lengthen the period rather than cut the window
(`metric-definitions`).

**4. Name the anchor.** The send (or delivery), the open, or the click. A window anchored on the click misses
people who read the message and came back directly; a window anchored on the send credits everyone who got it
and bought, and it is the widest of the three. Anchor on the narrowest signal the channel records for that
person: the click; where there is none, the read or display receipt; where there is none either (a text, a
visit to a store), the delivery. Match by an identifier such as the phone number or the customer number. Within
a flow, name the anchor per channel. Channels on different anchors do not add up, so for the budget decision
(step 2) put every competing channel on one anchor, the widest that all of them have, delivery plus an
identifier; the click and read signals stay as diagnosis, on the assisted line and in the channel's own skill.
No signal tells apart two channels delivered to one person inside one window with no click on either, and last
touch on delivery then credits the channel that sends more often. Write the tie rule into the credit rule
(`metric-definitions`), and read the pair on the attribution multiple per channel, where credit that cadence
inflated shows as a rising multiple.

**5. Exclude conversions already under way.** An order started, a visit booked before the send, a checkout in
progress: none of them gets credit from the touch. Service messages earn no credit (`transactional-messaging`).
A code handed out for signing up credits the signup, not the email that delivered the code: count orders that
used a signup code on a line of their own.

**6. Net out cancellations and returns by the freeze date.** Credited orders canceled or returned inside the
return window leave the credited revenue. Until that window closes, the line is provisional
(`regular-report.md`, step 7). A partial refund follows the definition. Web analytics that never learns about
returns overstates revenue.

**7. Deduplicate, and show double credit.** Under the model, every conversion key receives credit once in total
(the weights sum to one), so channel lines add up to the deduplicated total. Where a page shows each channel's
claim from its own tool, put the sum of claims, the deduplicated total and their difference beside each other,
and call the difference double credit. Never add claims.

Take a worked example with invented numbers. The email tool claims 420 orders, the push tool 260, the text tool
140: 820 claims. Matched on the order key under one rule for all three, they are 610 distinct orders. Double
credit is 210. Where the tools claim on windows and anchors of their own, the difference also holds claims the
model rejects: show duplicates and claims outside the model as two lines.

**8. Publish what the model cannot see.** The share of revenue with no identified person (offline sales, guest
checkout), and on the website the share of sessions without consent to analytics (see the legal regime in
`SKILL.md`). Compute attribution shares on identified or consented revenue, and say so on the line. Put a
channel's share of revenue beside total revenue.

**9. Show assisted conversions on a line of their own.** Conversions credited to another channel that had a
program touch inside the window before them, per channel. Never add them to direct credit. When direct credit
falls and assisted conversions do not, the message lost its direct route (a missing address, a missing link):
that is a diagnosis, not a failing channel.

**10. Put the incremental figure beside the attributed one.** Where a control group exists, place the
incremental revenue from its read, with the interval and the read date, beside the attributed revenue for the
same population and period. The attributed figure divided by the incremental one is the attribution multiple;
read it per channel. An increment at or below zero leaves the multiple undefined, and the line then reads
credit with no measured effect. A multiple that rises along with attributed revenue means credit is growing
faster than the effect. The increments of separate campaigns do not add up to the program's increment:
overlapping campaigns share people, and only a global control group reads the program.

Take a worked example with invented numbers. On the population a control group was drawn from, attributed email
revenue equals 4% of the revenue of the people who received email, and the difference against the control group
is 1%. The attribution multiple is 4.

**11. A change of model is a change of definition.** A break marker and a restatement note
(`regular-report.md`, step 10), and the old and the new model side by side until the first freeze date under the
new one. Do not switch mid-cycle to the model that shows your own channel in a better light.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| Attribution window | the point where the daily conversion rate of touched people falls to the rate of untouched people | parameter |
| Window with no control group | the point where your own lag distribution levels off; replaced at the first control group read | starting heuristic |
| Anchor | the narrowest signal the channel records: the click, else the read or display receipt, else delivery plus an identifier; one anchor for every channel competing for a budget | follows from the channel and the decision |
| Two models side by side | until the first freeze date under the new model | follows from the definition |
| Attribution multiple | at every control group read, per channel | follows from the definition |

## Edge cases

- **A long cycle with the sale offline.** Match by identifier, anchor the window on the send and derive it from
  your own lags to the visit or booking, exclude people who booked before the send, and read intermediate stages
  at their own ages (`cohort-reading.md`, step 10).
- **Promo codes as a way to identify a channel.** A code identifies a channel only if it is handed out nowhere
  else. A shared code leaks, and a code posted on coupon sites credits the channel with orders it never touched.
- **A channel with no click.** Anchor on the read or display receipt where the channel gives one, else on delivery,
  plus an identifier (step 4).
- **Two channels with no click reach one person inside one window.** No signal tells them apart, and last touch
  on delivery pays the channel that sends more often: settle it by the tie rule written into the credit rule, and
  read the pair on the attribution multiple (step 4).
- **A daily trigger or a daily digest.** The send cadence cuts the lag distribution, which levels off there; no
  window follows from it. Hold out a share of the people it fires on, and until that read the line says the window equals the
  send cadence and was not derived (step 3).
- **Web analytics counts devices.** One person on two devices is two customers, and a channel report from web
  analytics does not reconcile line by line with an order system (`metric-definitions`, reconciling across
  systems, step 4). The order system stays the system of record for money.
- **The business wants one number, "the CRM share of revenue."** Give it with total revenue and the attribution
  multiple (`vanity-metrics.md`).
- **Attributed revenue of recommendations, win-back campaigns or in-product displays.** These are attribution
  figures. Publish them on request, and never as the result of the mechanic (`personalization`,
  `lapse-and-winback`, `in-product-messaging`).
- **A global control group excluded from email but not from paid targeting.** The effect it reads is narrower
  than "the program" (`experiments-and-holdouts`), and you say so on the line.

## Failure modes

**Channel claims exceed revenue.** Sign: channel lines add up to more than the deduplicated total, or more than
accounting. The remedy is step 7.

**Credit grows, the effect does not.** Attributed revenue rises, the increment stays flat, the multiple rises.
Causes: the window got longer, the anchor moved to the send, signup codes, more sends to people who buy anyway.
The remedy is steps 3 to 5 and step 10.

**The CRM share rises as acquisition falls.** The share rises while total revenue and the number of new
customers fall. The remedy is the counterweight in `vanity-metrics.md`.

**The model war.** Each team proposes the model that favors its own position. Sign: a proposed model arrives
together with its channel's result under it. The remedy is a model chosen per decision (step 2), and a change of
model handled only as a change of definition.

**Credit falls, the effect holds.** Tracking was lost: consent to analytics dropped, link tagging broke, a
platform release changed counting. Signs: the unidentified share rises and the increment stays flat. The remedy
is step 8; broken tagging is an incident for `program-audit-and-ops`. Watch the multiple to tell this mode from the
previous one: when it rises, credit is inflated; when it falls, credit is being lost.
