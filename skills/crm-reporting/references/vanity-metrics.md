---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-13
---

# The register of vanity metrics

A vanity metric here is **a number that improves, or holds, while the work it is quoted for gets worse, because
of how its numerator or denominator is built.** None of them is a wrong number. Each is correct and answers a
narrower question than the one it gets quoted for. You apply this register in `regular-report.md`, step 5:
every metric below stands in the same report row as its counterweight, or it does not stand in the report.

**One rule covers every rate computed on sends.** It improves when you stop sending to the people least likely
to respond. Beside it, put the absolute count of what the business wants (orders, people, margin) and the number
of people reached.

## The register

| Metric | How it improves while the work gets worse | Counterweight in the same row | Named by |
|---|---|---|---|
| Share of the base enrolled in the loyalty program | its denominator carries the flow of new customers; slow that flow and the accumulated base dominates, so the share climbs with no change in behavior, hardest once acquisition stops | redemption share; new customers in the period | `loyalty-program-design` |
| Share of all customers who purchase again | the same construction: it climbs when acquisition stops | second purchase rate of first purchase cohorts at equal age; new customers in the period | `loyalty-program-design`, `repeat-purchase` |
| Share of revenue from your own channels (the CRM share) | its denominator is total revenue, so it rises when acquisition falls and when another channel took the credit; it also depends on an attribution model the program does not choose | total revenue; the attribution multiple | `crm-program-design`, `metric-definitions` |
| Revenue attributed to win-back campaigns | it counts people who were coming back anyway | return rate of the attempt cohort per threshold step; the return rate inside the control group | `lapse-and-winback` |
| Share of revenue attributed to recommendations | it counts a click from somebody who would have bought anyway; it is an attribution figure, not a health measure | resolved share; the increment against a control group | `personalization` |
| Revenue credited to in-product displays on a view window | it credits the display with everyone who was about to act anyway | a control group of eligible people who reached the slot | `in-product-messaging` |
| Click rate of in-product messages | it counts taps, accidental ones included, rewards loud formats, and says nothing about the people who closed the display or never saw it | wasted interruption share | `in-product-messaging` |
| Push click rate on delivered pushes | people who switch notifications off leave the denominator, so the rate holds or improves while the channel shrinks | displayable share of the install cohort at the check age | `push-notifications` |
| Revenue per recipient read alone | it rises when the program mails only its most responsive people and falls when it extends reach, so a shrinking channel and an improving one look the same | total revenue from the channel, in the same row; the count of people who received at least one send in the cycle | `email-program` |
| Reachability loss per addressed person read alone | it falls when the program narrows sends to its most responsive people or stops sending, so a program going quiet looks like one getting healthier | revenue per reachable person over the same period, in the same row; the counts of people addressed and messaged | `contact-orchestration` |
| Open rate | it rises with machine opens nobody made, and with a subject line that promises more than the message delivers | on-job click share; people who clicked | `email-copy` |
| Click-to-open rate | it inherits every distortion of open counting through its denominator | as for open rate | `email-copy` |
| Delivered share | it improves when a sender stops mailing everybody doubtful | reach: people who received a message against the people the program is meant to reach | `deliverability` |
| Number of email clients passed in a preview tool | it grows with the tool's list rather than with your base, and an emulated preview predicts a client rather than observing one | the share of accepted recipients whose reading environment, from your own environment list, was checked in a live mailbox | `email-design` |
| Share of conversations handled without a human | it rises when the exit to a human is hidden | share of identified issues settled on the first pass; policy match of bot answers | `chat-and-bots` |
| First response time | it falls when an automated greeting counts as a reply | promise kept: first human replies that arrived by the time the chat promised | `chat-and-bots` |
| CSAT from a survey sent on closure | it never reaches the people who left before an answer or got stuck in a bot | share of identified issues settled on the first pass | `chat-and-bots` |
| Conversations started by a proactive opener | it measures the interruption, not the help | share of those issues settled on the first pass | `chat-and-bots` |
| Open rate and click rate of service emails | they are high by construction, because the person is waiting for the message | chase share by path; on-time share per row | `transactional-messaging` |
| Revenue "from confirmations" | a message the person is owed does not have to earn anything | do not publish it; chase share by path | `transactional-messaging` |
| Widget conversion on impressions | narrowing a point to the hottest visitors improves the ratio while the base receives fewer contacts | usable contacts per thousand sessions of the fixed population; the absolute count of new usable contacts | `onsite-capture` |
| Revenue of the promotional days | every purchase borrowed from the weeks around the sale counts as a gain; the shoulders, where the borrowing shows, are not read | margin over the extended window per person in the active base; the pair of periods | `promo-calendar` |
| Welcome series conversion on entries into the series | it cannot see the people who arrived and entered no series | first-action rate of the arrival cohort; silent loss | `welcome-and-activation` |
| Base size | it grows on any intake at all and says nothing about whether you can do anything with the records | the reachable base | `list-building` |
| A survey score reported alone (NPS, CSAT) | it rises when the population asked narrows to the satisfied, and the people who already answer answer again; the narrowing is invisible in the score | the response share and the population asked, as asks over experiences; complaints per order through other channels | `voice-of-customer` |
| The score of a part of the experience whose owner chooses whom to ask | the owner selects the respondents, so the score improves with the selection and not with the work | asks over experiences for that part; complaints per order through other channels; sampling and sending held centrally | `voice-of-customer` |
| Handoff conversion (MQL to SQL, the share of handed accounts that sales accepted) | it rises when the program hands over only the obvious accounts and sales starves | the count of accounts handed over; the won share by grade cell at the time of handoff, read a cycle later | `b2b-lifecycle` |
| Sales cycle length | it falls when stalled deals are closed "no decision" earlier | the count of closes by code and the share of "no decision" closes without a recorded re-qualification; the share of a handoff cohort that reached a decision, at its settling age | `b2b-lifecycle` |
| Renewal rate | it rises with contracts renewed by default and with holdovers counted as retained, so it cannot tell "decided to renew" from "missed the chance to refuse" | the share of renewal cases decided by their decision point; contracts renewed by default, with what became of each in the next term | `b2b-retention` |
| Net revenue retention | it rises with price increases and with expansion into accounts that will not renew next term, and it hides contraction inside expansion | gross revenue retention; contraction at renewal; expansion signed less than one term before a notice of non-renewal | `b2b-retention` |
| Average order value | it rises while the number of orders falls | order count; total revenue | this skill |
| Retention rate, or activity of the base | retention can rise while revenue from new customers falls; activity counted on opens and clicks can rise with no revenue behind it | revenue from new and from returning customers, separately; total revenue | this skill |

## How to add a row

A number enters the register when you can name the construction that makes it improve while the work gets worse,
and a counterweight that does not share that construction. Check the second condition by substitution: apply the
failure to both numbers and confirm the counterweight moves the other way or stays put. Average order value
passes: revenue equals the number of orders times the average order value, so orders falling while the average
rises leaves the average improving and revenue free to fall, and the order count shows it.

A number with no counterweight that survives the substitution is not a vanity metric. It is a line that answers
the wrong question, and it leaves the report (`regular-report.md`, step 12).
