---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# Issuing an offer, limiting it, and honoring what you sent

The moment an offer is sent it stops being a plan and becomes a promise held by a named person.
Everything after that is about two things: keeping the promise from reaching people it was not
meant for, and keeping it for the people it was.

The two are not written down with equal care. Limits protect a budget, so somebody writes them.
What you owe a person once the thing you promised has run out protects no budget, and it is the
failure that reaches exactly the customers who responded. This file writes both.

## Entry conditions

The offer is specified: form, depth, condition, window, exclusions.

## Exit conditions

Every issued promise has an addressee, a redemption window, a set of limits, and **a named way of
being closed when the thing promised is gone**.

## Steps

**1. Choose the carrier.** Unique per person, or shared by everyone.

| | Shared carrier | Unique carrier |
|---|---|---|
| Cost to set up | one combination | issuing and validation processing |
| Limit on redemptions | not enforceable on the carrier | per person and in total |
| Limit on the window | only in the rule, not on the carrier | on the carrier |
| Leakage | reaches people it was not addressed to, and the intended recipient can no longer be told apart from anyone else | the addressee is always known |
| What you can measure | redemptions, with no participants behind them | participants |

The rule: **a benefit addressed to a named segment is issued on a unique carrier.** A shared
carrier is a public offer, whatever it is called internally. If the offer is public in substance,
construct it as a public one and price it that way, rather than counting it as personal on paper
and discovering the difference in the margin.

**2. Set the six issuing limits.** Total redemptions; redemptions per person; minimum order value;
maximum absolute benefit; excluded items; the window. All six go in before the first send. Each
one added afterwards is a narrowing of a promise somebody is already holding, which is the
withdrawal in step 6 wearing different clothes. Record, for each limit, its own
reason on every redemption attempt it refuses (the control metric in `SKILL.md`): on absolute
counts, a refusal with no recorded reason looks the same as a lost event.

**3. Control what lives outside your system at issuance, not at redemption.** Benefits running in
somebody else's system (an affiliate network, an aggregator, cashback on a payment method, a
rebate service) are invisible to arbitration (`stacking-and-arbitration.md`), and no rule you
write at checkout will see them. The only lever you have is how many such distributions are live
at once. **Run no more than one external distribution at a time, and name its period in advance
rather than closing it when somebody notices.** This is the one place where the cheap fix is
upstream: people who combine four independent benefits are not exploiting a bug, they are using
four things you handed out.

**4. For an earned benefit, limit attempts and raise a flag rather than a block.** Cap the number
of attempts across the whole promotion, or the prize fund goes to whoever repeats one action
instead of to whoever completes the mechanic. Derive the anomaly threshold from the honest
maximum, meaning how many attempts somebody playing seriously can physically make in the period,
and **have it flag an account for manual review, not block it**. A threshold set on behavior sits in
the same tail as your most engaged participants, so an automatic block catches them along with
whoever it was aimed at, and the two errors do not cost the same: a blocked honest player is a
public complaint, a missed cheat is the cost of one prize. Build the flag into the design at the
start; retrofitting review onto a live promotion means reviewing a backlog while the queue grows.

**5. Separate the window from the stock.** The **redemption window** is time: how long the promise
lives in front of the person. The **stock** is a quantity: how much of the promised thing is left,
whether that is codes in the pool, units on the shelf, or money in the fund. They are two
different numbers in two different units, and they run out at different moments. A dashboard can
show you the stock without knowing who was sent what; nothing on that screen shows how many
promises are still outstanding, so you have to hold that number yourself.

**6. Honor the promise past the stock.** The rule: **a promise lives by its redemption window, not
by the state of the stock.** Withdrawal is possible only before sending; after sending, what you
withdraw is issuance to new recipients, not the promise to existing ones. Until the window closes,
every issued promise is closed one of three ways: by the thing itself, by a substitute, or by
refunding what the person already paid toward it. Name which one before the first send rather than
improvising it at the counter, and let the recipient judge equivalence rather than your cost
sheet: a substitute that costs you the same and reads as a downgrade closes the promise on paper
and not with the person.

From this follow two operational consequences.

- **Issuing does not start until the way to close a promise without stock is named.** It is a
  launch condition, not a nicety, and it takes one line in the specification.
- **The level at which issuing stops is not zero**, and you measure it in whatever unit the stock
  drains in. A pool of unique codes drains as you issue codes, so the level is the expected
  issuance over one monitoring interval. Units on a shelf and money in a fund drain as people
  redeem, not as you send, so there the level is the expected redemptions over that interval,
  which is a different number and a larger one wherever redemption lags the send. Either way the
  level covers only what moves between two checks. It does not cover the promises already
  outstanding: the substitute you named above covers those, which is why it has to exist before
  the first send.

**7. Walk the redemption path yourself, end to end, before the send.** From message to redemption:
whether the carrier can be saved, whether it survives dismissing the notification, whether it can
be typed in by hand, whether it works in the sales channel the message points to. Do this before
sending, because fixing the path afterwards means a second message to the same people, which costs
more than the fix and reads as an apology.

**8. Hand the stock to monitoring and name the signal.** Watching a consumable resource belongs to
`program-audit-and-ops`: the level, the alert, the duty slot. What goes there from here is the
object itself and the stopping level from step 6. What comes back is the fact that the level was
reached. **What does not move is the decision about promises already issued**: that stays here,
because it is a decision about what you owe, not about what is running.

## Thresholds and timings

| Quantity | How it is derived |
|---|---|
| Level at which issuing stops | one monitoring interval of whatever drains the stock: expected issuance for a pool of codes, expected redemptions for shelf stock or a fund |
| Anomaly threshold for an earned benefit | the honest maximum number of attempts in the period, from your own funnel |
| Prize fund reserve | a margin on top of the computed fund, held while you have no response data of your own; it applies to a first run of a mechanic and is replaced by your own completion rate after one full promotion |
| External distributions live at once | one |
| Way of closing a promise without stock | the thing, a substitute, or a refund, named before the first send, per offer |

## Edge cases

- **The carrier leaked.** A spike in redemptions is indistinguishable from success by volume. It
  is distinguishable by composition: redemptions arrive from outside the audience and outside the
  channel of issue. You have to be able to take that reading, which means the carrier has to carry
  a mark of where it was issued, decided at step 1 rather than after the spike.
- **One person holds two promises for the same thing.** Resolved by arbitration
  (`stacking-and-arbitration.md`), not here. What stays here is the obligation to record that a
  promise was issued before the second one goes out, so arbitration has something to find.
- **A promise issued to the wrong segment.** A mistake in issuing does not cancel the promise to
  the person: it gets honored, and what narrows is issuance. This is step 6 seen from the other
  side, and it is worth stating separately because the instinct is the opposite.
- **Arbitration delivers less than you promised.** The floor in `stacking-and-arbitration.md`
  recomputes the second benefit on an order, so a promise can arrive smaller than it was sent,
  with the stock full and nothing having run out. Step 6 does not cover this case, and stretching
  it over this one costs you the rule. Decide it where the promise gets written: either the
  message names the condition, so the person holds a promise that can be reduced, or you exempt
  the offer from the floor, or you close the part that got cut like any other promise you did not
  keep. The one answer not available to you is the silent one, because the person reads the number
  you sent.
- **The stock runs out mid-window.** This is the ordinary case, not an incident. It is exactly
  what the named substitute in step 6 exists for, and a promotion that treats it as an emergency
  has skipped the step.
- **An honest participant looks like a cheat.** The ordinary case in an earned benefit, and the
  only defense against it is manual review before a valuable prize is released. This is the reason
  step 4 asks for a flag rather than a block, stated as a case rather than as a rule.

## Failure modes

- **The carrier dies quietly.** It stops working before the window closes: the pool is exhausted,
  a rule was switched off, the item sold out. On the business side this is not an event: the send
  completed, and monitoring sees a resource level rather than a promise. The signature is support
  contacts about an offer that does not work, with nothing at all in the alerting. In your own data
  the sign is a rising share of redemption attempts not applied, with the reason "stock" or "carrier
  no longer works". Realized depth cannot see this failure, because it counts only the orders where
  the benefit went through. This is the
  most expensive failure in the skill, because it lands on precisely the people who responded, and
  it is the failure the whole of step 6 exists to prevent.
- **Issuance exceeded the plan.** Redemptions came in above the size of the audience. That means
  either a leaked carrier or a missing per-person limit, and the two are told apart by the
  composition of redemptions rather than by their number, the same reading as the leak case,
  which is why the mark from step 1 pays for itself twice.
