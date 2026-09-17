---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-04
---

# Send selection and suppression

"Send it to the list" is the absence of a decision. You assemble the audience for a send by
subtracting from a tier, and you store the resulting composition with the send. Without the
record, you cannot reproduce the result and you cannot read the reporting.

## Entry conditions

- The program plan exists: tiers, rhythms and suppression rules are written down
  (`program-plan-and-cadence.md`).
- This send has a slot and a stated purpose. A send with no purpose has no audience rule either,
  and it defaults to everybody.

## Exit conditions

The recipient list is assembled, its composition is recorded alongside the send, and the send
either goes out or gets dropped under the rule in step 5. Dropping the send is a normal outcome
of the mechanic.

## Sequence

**1. Start from the slot's tier, not from the list.** The tier is your ceiling. Every step after
this one removes people.

**2. Apply hard suppression by scope.** Non-negotiable, and enforced by the platform rather than
by whoever builds the send. Start with the basis: in a regime that requires consent before the
first message, no valid basis means there is no audience to assemble and nothing below applies.
**Who this does not bind:** an opt-out regime, which changes the basis question rather than
removing it (the paragraph at the end of this step), and any message that is not marketing.

Everything after that is a prohibition, and a prohibition carries two properties: the reason it
exists and the scope it covers. Read the scope to know how far the prohibition travels. Teams get
it wrong first when one platform carries more than one brand.

The scopes below turn on who the sender is, and the sender is the identity the message went out
under: the From identity named in the header, not the business unit that commissioned the send. A
brand sending under its own identity is its own sender; two brands sharing one identity are one
sender, whatever the platform's list structure says.

| Scope | Typical reason | Where the prohibition applies |
|---|---|---|
| Address or channel | Hard bounce; an address that does not exist; a channel identifier that cannot receive | Every send to that address, in every program and every brand on the platform |
| Global | Do not contact; an erasure request; an unsubscribe whose wording covered the sender as a whole | All marketing sending inside the perimeter that request named |
| Controller or brand | An opt-out from one brand, where the brands are separate senders holding separate permissions | That brand only |
| Message type | A type-level opt-out set in a preference center: the newsletter off, order updates still on | That type, across the brand holding the preference |
| Program | The tunable subtractions in step 3: frequency, recency, flow priority | That program only |

Two rules hold the table together.

- **The widest matching prohibition wins.** A global opt-out closes every brand under it. A hard
  bounce closes the address whatever permission sits on it, because that constraint is technical
  and no consent repairs it.
- **The absence of a prohibition is not a permission.** Someone not suppressed in one brand's
  program has not agreed to another brand's mail. Scopes remove people; none of them widens
  consent.

Neither rule runs on a suppression row that carries no reason and no scope. Write both when you
create the row, not the week somebody asks.

**A pause is a prohibition that ends.** Somebody who asked for silence until a date is suppressed
until that date and then released by the date rather than by anybody remembering: the row carries
its end, and the resume puts the person back on their tier's cadence, not in front of everything
that queued up while they were away. `consent-and-preferences` records the instruction, this step
applies it, and a pause whose basis expired before it ended does not resume at all.

**A mandatory notice is not subject to any of this.** What you owe somebody by law or by contract,
a recall, a change of terms, points about to expire, goes out to the people it concerns including
the suppressed tier, and neither the scopes above nor the program rules below hold it back. The one
question it raises is whether its content is mandatory throughout: a notice carrying a promotion is
a promotion.

Under an opt-out regime the basis changes shape: you may send, but you must already have honored
the opt-out, and the law sets the honoring window, not your platform's refresh schedule.
`consent-and-preferences` owns which basis makes a send lawful and how far a withdrawal reaches.
Applying the resulting scopes to an audience is this step.

**3. Apply program suppression.** These are the tunable rules, and they prevent most of the
damage:

- received a touch inside the tier's minimum gap, counted on the person rather than the row where
  two records of one person are linked;
- bought recently, inside the window where a repeat purchase is unlikely for this category;
- currently inside an automated flow with higher priority;
- has an open order incident or support ticket. A promotion landing on top of a delivery problem
  is the cheapest complaint a program can avoid;
- belongs to an account whose contract stage is owned by somebody else: under `b2b-retention`'s
  ownership classes the account manager's stages admit only the set that skill allows, and a stage
  with no class admits nothing.

**4. Apply relevance.** The thing you promote has to be available to this person: in stock, sold
in their market, in the language you addressed them in before. A send offering something the
recipient cannot buy costs the same as one they can, and it teaches them to ignore you.

**5. Check the size that survived.** When the remaining audience is smaller than what has
produced a readable response in your own history, take one of two roads: merge the slot into the
next send, or send it and record in advance that you will draw no conclusion from the result. Do
not widen the audience back out to make the number readable. That reverses steps 1 to 4 for the
sake of the report.

**6. Reserve a holdout when the send tests something.** Only when you have a hypothesis. A
holdout on every send costs reach and returns no information. Sizing and design belong to
`experiments-and-holdouts`.

**7. Record the composition.** Tier, rules applied, counts before and after each subtraction.
Teams skip this step, and it is the one that makes the next cycle's diagnosis possible.

## Thresholds and timings

- **Minimum gap between touches:** per tier, inherited from the program plan. Never set it per
  send.
- **"Bought recently" window:** a fraction of the median interval between purchases for the
  category, not a calendar period. In a weekly-purchase category that is days, in an annual one
  it is months, and the same rule produces both.
- **Priority when two messages collide on the same person on the same day:** the five classes of
  `contact-orchestration`, in its order, service message, mandatory notice, perishable and personal,
  automated flow, campaign. The campaign always yields. This skill's own split into campaign,
  automated and service says who assembles a send rather than which of them yields; read it as a
  short version of the precedence list and you lose the two classes in the middle, which carry what
  you owe somebody and what expires today.
- **Opt-out honoring window:** set by the applicable law, not by the program. In the United States
  CAN-SPAM gives you ten business days for commercial email, and the unsubscribe mechanism has to
  keep working for at least thirty days after the message went out. Neither one matches what the
  EU, the UK or Canada asks for. Run your platform's suppression refresh faster than the shortest
  window that applies to you, or you break the rule while looking compliant.
  **Who this does not bind:** a message whose primary purpose is one of the five categories of
  transactional and relationship message; the regimes outside the United States, which set their
  own windows (`SKILL.md`, and the mechanics of `consent-and-preferences`).
- **Cancellation window:** how late you can pull a send is a property of the sending platform.
  Find it before the first send you need to pull, not during it.

## Edge cases

- **A campaign and a triggered message land on the same person the same day.** The trigger goes,
  the campaign waits. The trigger answers something the person did.
- **The segment is empty after suppression.** Skip the slot. Do not widen it back to the tier.
- **Suppression removed more than half the tier.** The rhythm exceeds what this audience carries.
  Do not fix it here, take it back to `program-plan-and-cadence.md`.
- **Resend to non-openers.** Allowed inside the same tier only, respecting the minimum gap, and
  never to anyone who already clicked. Count the resend as a second touch in the load, because
  that is what it is.
- **An external event:** an outage, a public crisis, an incident affecting orders. Pause
  campaigns, keep service messages flowing. Write the pause rule before you need it, because you
  will need it on a day when nobody has time to design one.
- **Multi-brand or multi-market lists on one platform.** Read the scope column in step 2 before
  you decide anything, and settle first which of them is a sender: two brands that mail from one
  From identity are one sender, so an unsubscribe worded against the sender closes both, and
  treating them as two because the platform holds two lists leaves you mailing somebody who
  stopped you. Frequency and recency rules run per program, so someone rested in one
  brand's program is not rested in the other's, and that is how a person receives the same offer
  twice. A hard-bounced address does not come back through the second brand: the address is
  unreachable in both. A brand-only opt-out leaves an independent permission for the other brand
  standing and does not create one where none existed. Both simplifications break. Treat the
  brands as one list and you spread narrow prohibitions over permissions nobody withdrew; treat
  them as unrelated lists and you ignore the wide ones.
- **A recipient sits in different tiers across channels**, active in one and dormant on email.
  The email tier governs this send. The cross-channel view belongs to `contact-orchestration`.

## Failure modes

- **The "received a touch recently" rule keeps removing more than half a tier.** The rhythm does
  not hold. The plan is wrong, not the rule.
- **Complaints concentrate in the segments receiving the most touches.** Someone applies
  suppression on paper and bypasses it in practice. Look for a manual send that skipped the
  rules, and find the bypass before you change any threshold.
- **Nobody records the composition.** The mechanic fails whatever the results say: you have
  nothing to compare, and the next diagnosis starts from zero.
- **Every send goes to the same audience.** Suppression has collapsed into a static list. Check
  that you recalculate tiers each cycle, because a frozen tier assignment looks exactly like this.
- **Exceptions keep getting granted for important campaigns.** Every send is important to whoever
  asked for it. When the rules bend for a launch, they are not rules, and the load you counted in
  the plan is fiction. Either write the exception into the plan as an anchor, or hold the line.
