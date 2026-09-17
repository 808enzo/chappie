---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-15
---

# Expansion and contraction: the amendment inside a contract term

The unit here is **the amendment**: a change to the entitlement of a live contract inside its term. The customer decides
on the account manager's proposal; a new buying unit is run by the account executive through `b2b-lifecycle`. The price
and the depth of any concession are `offer-design`'s; a message shown at a limit inside the product is
`in-product-messaging`'s.

## Entry conditions

A signal that the entitlement should change: use approaching the contract's entitlement or already past it; a contact
from another team or division of the customer (`b2b-lifecycle`, `qualification-and-handoff.md`, edge cases: a request from
a new contact at an existing customer is expansion through the account manager); a new outcome named at a QBR; the
customer's request to add or to reduce; the part proposed and not bought, from the won-deal record (`b2b-lifecycle`,
`buying-group-and-stalls.md`, step 9: a partial win is a win, and the unsold part is an open opportunity).

## Exit conditions

The amendment closes as signed, with the live contract's end date as its own; as folded into the renewal proposal; as
sent on to `b2b-lifecycle` as a new deal; as declined with a code; or as deferred to a date, with a timer. You update the
contract register and the plan on the day of the signature.

## Steps

**1. Classify the change before any proposal.** An addition inside the buying unit (seats, volume, a module) is an
amendment the account manager runs. A separate buying unit, with a budget and a buying group of its own, is a new account
in `b2b-lifecycle`'s grade and goes to sales; the live contract is a structural signal in that grade. A reduction is step
7. Use past the entitlement is step 6. A missing feature that the account manager or a customer success manager noticed is
a signal for an amendment when the feature exists in another package, and a request to the product team when it does not.

**2. Check readiness against the plan.** No expansion proposal goes out while a milestone of the plan is missed past its
grace, a collection case is open, an issue about a problem is open (`chat-and-bots`), or a renewal case is open; in the
last case the expansion goes into the renewal proposal (`renewal-case.md`, step 5). Expanding an account that is not
keeping its plan adds to the revenue a non-renewal would take.

**3. Align the end date.** An amendment inside the term ends on the live contract's end date, so a buying unit keeps one
decision point. The amendment's first term is shorter than a full one, and its price for the remainder follows the
contract's rule; under daily proration it is the annual price × the days remaining / the days in the term. A change in the
number of seats does not change the end date. Inside a renewal case's window, from its opening date to its decision point,
sign no separate amendment: it folds into the renewal proposal. The exception is use already at a hard limit (step 6): an
amendment the customer asks for there is signed co-termed at once and becomes the baseline of the renewal proposal, since
otherwise the customer waits at the limit for the whole window. Start the conversation about expansion when the
projected date on which use reaches the entitlement (current use carried forward at its own growth over the last period)
is closer than the customer's approval time on the original deal; otherwise the customer reaches the limit before it can
buy.

**4. Put the proposal to the amendment's buying group.** The price list and `offer-design` set the price and the depth;
the account manager writes; the program sends material for a role on request, from the allowed set. An amount above the
champion's authority is the economic buyer's decision, and a signature from a role without authority is a future dispute
over the invoice (the class "disputed", `invoice-collection.md`, step 1).

**5. Record it on the day of the signature.** The entitlement and the invoice schedule go into the contract register, with
the end date unchanged; a new outcome goes into the plan with its milestones (`success-plan-and-qbr.md`, step 3).

**6. Handle use past the entitlement.** On a contract with a true-up clause, notify the customer before the true-up
invoice, at least the customer's approval time on the original deal ahead of the invoice date, with the usage data. A
true-up invoice sent with no prior notice counts as disputed from the day you issue it, and the collection case on it
opens in the class "disputed" (`invoice-collection.md`, step 1). On a contract without such a clause, use past
the entitlement is a conversation about an amendment, not an invoice. At a hard limit in
the product, a message inside the product at the limit (`in-product-messaging`) and a signal to the account manager on the
same day.

**7. Handle contraction.** Inside the term, the entitlement goes down the way the contract says. Where an annual commitment
allows a reduction only at renewal, record the request as two inputs: into the renewal case, as a term of the proposal,
since a renewal with contraction is the decision "renewed with contraction" and not a lost contract; and into the scoring
in `lapse-and-winback`, as an alarming action. Unused seats do not wait silently for the renewal: the milestone of use in
the plan (`success-plan-and-qbr.md`, step 3) comes before the contraction shows up at the signature.

**8. Close with a code.** Signed, with its change of entitlement; folded into the renewal; sent on as a new deal; declined
(budget, no need, timing, price); deferred to a date with a timer. A date without a timer does not get written.

## Thresholds and timings

| Quantity | Where it comes from | Class |
|---|---|---|
| End date of an amendment | the end date of the live contract | 4 |
| Price of an amendment's first term | the contract's rule; under daily proration, the annual price × the days remaining / the days in the term | 3 |
| Window in which an amendment folds into the renewal | from the renewal case's opening date to its decision point; an amendment asked for at a hard limit is signed at once and becomes the proposal's baseline | 4 |
| Start of the conversation about expansion | the projected date of reaching the entitlement is closer than the customer's approval time on the original deal | 4 |
| Notice before a true-up invoice | at least the customer's approval time on the original deal ahead of the invoice date | 4 |
| Contraction inside the term | the contract | 4 |
| Deferred amendment | the date recorded with its code | 4 |

## Edge cases

- **A new division asks for a contract of its own.** A separate buying unit: `b2b-lifecycle`.
- **A merger doubled the users.** An amendment, or a separate contract under the assignment clause; the plan gets rebuilt
  (`success-plan-and-qbr.md`, edge cases).
- **Use past the entitlement forgiven as goodwill.** A concession with an end date, `offer-design`'s; without a date,
  nothing in the register tells it from the contract's entitlement, and at the renewal it is read as the entitlement.
- **The champion signed an expansion without authority.** The economic buyer decides before the invoice goes out.
- **A request to reduce that hides an intent not to renew.** A reason code, and the renewal case opens before its
  opening date.
- **A purchase through a marketplace or a reseller.** The amendment goes through the reseller's offer, and the rules for
  aligning dates are the platform's; where the platform cannot align them, the register carries two end dates and the risk
  of two decision points.

## Failure modes

**Expansion into a burning account.** The sign: amendments signed less than one term before a notice of non-renewal;
expansions on accounts with missed milestones. Remedy: the readiness check (step 2).

**The true-up invoice as a surprise.** The sign: disputes over true-up invoices, and collection cases of class "disputed"
right after them. Remedy: notice before the invoice (step 6).

**Two decision points on one buying unit.** The sign: amendments with end dates of their own; more renewal cases per
account than buying units. Remedy: align the end date (step 3).

**A new unit sold as seats.** The sign: seats added for a division whose buying group never met the account manager; that
division's users inactive; at the first renewal, that part leaves as a contraction. Remedy: classify the change (step 1).

**Unused seats kept until the renewal.** The sign: a contraction at the renewal on seats unused since the term began. A
second cause with the opposite reading: seats reduced inside the term against the contract, as goodwill, so revenue leaves
with no record and no decision. Remedy: the milestone of use in the plan; contraction under the contract and on the record.

This file rests on no statute or platform rule; the regimes it touches are in `SKILL.md`.
