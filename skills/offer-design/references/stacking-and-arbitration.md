---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-07
---

# When several offers land on one order

Offers are designed one at a time and redeemed all at once. A person who qualifies for a seasonal
promotion, a personal offer, and a loyalty accrual meets all three at checkout, and something has
to decide what applies, in what order, and where it stops.

That something is arbitration, and the unit it works on is **the order**. Not the person and not
the message: the frequency cap in `contact-orchestration` counts a person over a period, and this
counts one order at the moment it is placed. Skipping the decision does not avoid it: it delegates
it to whichever system happens to run first.

## Entry conditions

More than one offer is live at the same time, and at least one person can qualify for several.

## Exit conditions

Relations between groups of offers; the order in which forms apply; a floor on total benefit; and
the whole thing written down so that a new offer joins an existing group instead of starting a new
rule.

## Steps

**1. Build the register of live offers.** Public and personal, yours and external, running inside
your system and outside it. This is not the register of mechanics that `scenario-map` keeps: a row
there lives for quarters and describes a mechanic, a row here lives for days and describes one
promise that is currently redeemable.

**2. Create groups and set relations on groups, not on individual offers.** Offers reach dozens;
groups stay in single figures. A relation set once for a group survives every new offer added to
it, and adding an offer becomes filing rather than rule-writing. Three relations are enough:
compatible, incompatible, and one outranks the other.

**3. Personal outranks public.** The reason is structural rather than a matter of taste. A personal
offer buys a decision that would not otherwise be made; a public one also goes to everyone who
would have bought anyway. Under the reverse order the personal offer applies only on the orders
the public one happens not to reach, which is not where it was aimed, and the cost of selecting
the segment stops being visible in the data, because on the orders it was built for, it never
appears.

This ranking assumes you can tell both systems to stand down. A public promotion loaded onto a
till that keeps selling when the connection drops is not one of those: it applies what it holds,
and your ranking covers only the hours when the link is up. Where that is how it runs, set the
relation between the two groups in advance so they cannot sum (step 2), and set the depth of the
personal offer so that the till's promotion applying on its own still leaves you an order you
want. An outage is not the moment to find out that the two were designed to be applied together.

**4. Fix the order in which forms apply.** An accrual is computed **after** a price reduction.
Otherwise points are earned on a price nobody paid, and the cost of the obligation is higher than
the one you designed by exactly the depth of the discount. This is the one ordering rule that is
not a preference: it follows from what the two forms are computed on.

**5. Set a floor and recompute the remainder.** The floor is either a cap on total benefit per
order or a minimum margin per order. When the floor is reached, the second benefit is **not**
discarded: it is recomputed against what is left of the allowance. As an illustration of the
arithmetic: if a general reduction has already consumed part of the permitted benefit, payment in
points is allowed only against the remaining part, not against its own full share. The floor is
the only place in this skill where a mistake in an individual offer is caught automatically, which
is why it is worth setting before the offers that will test it exist.

What gets recomputed may be something you already promised a person by name in a message. The
floor still holds, and the promise does not stop existing because it did: you decide which of the
two gives way when you build the offer, not at the checkout. `issuing-and-honoring.md` carries
that case under its edge cases.

**6. Decide what happens between two compatible benefits.** "Whichever is better for the customer"
reads easily and costs money: a percentage benefit and a fixed one win in different price bands,
so which is better depends on the value of the particular order. The rule therefore has to be
evaluated per order rather than chosen once. The alternative is to declare the two forms
incompatible and give no choice at all, which is a legitimate answer, and cheaper, as long as
somebody decides it deliberately.

**7. Match the wording of the promise to the order of application.** Two benefits applied in
sequence do not add up, and a person reads a sum. A message that promised the sum, and a checkout
that applied the sequence, produce a complaint about honesty while the arbitration is working
exactly as designed. Check the wording against the order of application before the send;
`email-copy` writes the sentence, and this is the constraint it needs.

**8. Compute arbitration at checkout.** Not when the message is sent and not when the segment is
built: between the send and the order the set of live offers changes, and a decision made at send
time is a decision about a different set. One case moves it, and only one: an offer whose value
you quote to the person as a final figure has to be computed at send and then held, because the
figure was the promise. Step 7 is the cheaper answer to that one, and where you take it,
arbitration stays at checkout.

What separates arbitration from the frequency cap in `contact-orchestration` is the unit, not the
moment: one counts a person over a period, the other counts one order. The moments differ because
the units do. Keep track of which of the two carries the split: the unit is a property of the
problem, the moment is a decision you are making here.

## Thresholds and timings

| Quantity | How it is derived |
|---|---|
| Margin floor per order | a share of order value that arbitration does not take the order's margin below, from your own unit economics; arbitration recomputes the benefit past it (step 5) and does not refuse the order |
| Cap on total benefit | a share of order value, set against the same margin |
| Moment of computation | checkout, except an offer quoted to the person as a final figure, which is computed at send and held |
| Number of relations needed | three: compatible, incompatible, outranks |

## Edge cases

- **An offer that lives outside your system.** Two unlike things get filed here, and they take
  opposite fixes. A benefit computed by somebody else, such as cashback on a payment method, an
  affiliate network, or a rebate service, is invisible to arbitration and always will be; the only
  lever is limiting issuance (`issuing-and-honoring.md`, step 3). A promotion of your own that is
  applied somewhere you do not control at that moment, such as a till running without a
  connection, is a different case: you know it exists, you can put it in a group, and the fix is
  to set the relation in advance rather than to compute anything at checkout. Record both in the
  register as their own rows, so that nobody spends a week looking for the cause of a margin gap
  in rules that had nothing to do with it.
- **A return on an order that carried several benefits.** What goes back to the person and what
  goes back to the fund is a decision made once and written down; left undecided, it gets made by
  whoever is on the phone, differently each time.
- **There are only three offers.** Write the rule anyway. The fourth arrives next week, and a rule
  derived after the fact has to be checked against all three that preceded it.
- **A threshold inside a stack.** Whether the minimum order value is measured before or after
  somebody else's reduction is a decision, not a detail: it decides whether the order qualifies
  for the second offer at all. Both answers are defensible; only one of them is what your system
  currently does, and it is worth finding out which.

## Failure modes

- **Stacking below the floor.** The signature is direct: orders exist with a margin below the
  floor. It means the floor is either absent or set on a group rather than on the order, which is
  the common version: a cap per promotion caps nothing when three promotions apply.
- **The personal offer is devalued.** Personal offers do not apply, because the public one
  outranks them. The signature is the share of orders where a personal offer applied sitting near
  zero while issuance is healthy, with the unapplied attempts on personal offers carrying the
  reason "outranked". The cost is not the discount, it is that every segment decision
  upstream becomes unmeasurable.
