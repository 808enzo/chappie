---
claim_type: mechanic
source: "internal synthesis"
checked: 2026-09-05
---

# The policy: classes, precedence, the cap, quiet hours

The policy is the written rule: how much one person may receive, in what order messages yield to
each other, when they may not arrive at all, and what is exempt. It is short. Deriving the cap is
the part that takes the time, because the number has to come out of your own base.

## Entry conditions

The inventory is done: you have the distribution of load per person per period, and you can read
every sending system in one place.

## Exit conditions

A written policy that names: the cap per person per period in total and by channel, the message
classes and their precedence, quiet hours, what is exempt from the cap and where the exemption
ends, the owner of the policy, and how an exception is granted.

## Steps

**1. Sort messages into classes.** Precedence runs top to bottom:

1. **Service.** A direct consequence of the person's own action, which they are waiting for: order
   confirmation, delivery status, a login code. Never suppressed.
2. **Mandatory notice.** What you are obliged to tell them by contract or by law: points about to
   expire, terms changing, a product recall. Never suppressed. It is not exempt, because the person
   is not waiting for it: it counts toward load and the cap, and when it lands on a person already at
   the cap it still goes, and the next message below it in this order yields.
3. **Perishable and personal.** Available to this person and only now: a slot for tomorrow, the
   last item in their size, a price drop on what sits in their cart.
4. **Automated flow.** A reaction to an event. It has a shelf life, but a longer one.
5. **Campaign.** Addressed to many, and it will run again.

The rule underneath the order: **whatever perishes faster and is addressed more precisely wins.**
Not business importance, which sorts everything into the top tier within one meeting. A recurring
promotion yields to a personal occasion because the person will hear about the promotion next time
around. A reminder about the item someone viewed outranks a roundup of the category they browsed,
because the signal is more specific.

**2. Derive the cap from your own data.** Do not adopt someone else's number: whoever
measured it did so on another category, another purchase frequency and another base composition.

- Take the load distribution from the inventory.
- For each load bucket, read reachability loss and revenue per person over the window, both under
  their own denominators: people addressed for the loss, every person in the bucket for the
  revenue.
- Find the knee: the bucket from which loss grows faster than revenue.
- **Set the first cap at the 90th percentile of current load**, computed on messaged people as the
  inventory builds it. It breaks nothing that already works and trims the tail down to that level:
  the people above the 90th percentile keep receiving, only no more than it. Their share is at most a
  tenth of messaged people and can be much less, because load is counted in whole messages and many
  people sit exactly on the percentile; read the count above the cap before you announce what it
  cuts.
- Then move it down one message per period at a time, confirming each step with a randomized
  group.
- **Set the cap per engagement tier, not one number for everyone.** An active buyer absorbs more
  than a dormant one, and a single number for both hits the dormant group at the exact point where
  they are still recoverable. A tier belongs to a channel: `email-program` computes email's, and
  someone dormant in email can be active on push. So the email cap follows email's tier, and the
  total cap needs a tier on the person, which no neighbor holds: compute it by the same rule, from
  recency of response in any channel, and keep someone whose history is shorter than one window on
  the base cap until the window passes.

**3. Set a separate cap per channel.** An expensive, intrusive channel gets a tighter ceiling than
a cheap, mild one. The total cap survives alongside it: three messages in three channels is three
messages, not one in each.

**4. Set quiet hours.** In the recipient's local time, not yours. Exclude the night for every
channel that puts a sound on a device. Apply the window by class. A service message the person can
act on now (a login code, access, an exception whose deadline falls inside the night) and a
mandatory notice whose deadline falls inside the night go at once; which service rows those are is
`transactional-messaging`'s register. Everything else waits for morning, and a perishable message
whose shelf life ends before morning is dropped rather than held (`collisions-and-enforcement.md`,
step 2). For phone channels in the US a federal window runs from
8:00 to 21:00 local to the recipient, and it covers cold solicitation: a call or message sent with
prior express permission, or inside an established business relationship, falls outside the
definition the rule uses, and the rule does not reach email or push at all (the legal section of
`SKILL.md` carries the citation). Treat the window as the outer edge for whatever you cannot place
inside those exclusions. It is not a floor under everything you send. For every other channel,
derive the window from your own activity data. Work out the recipient's time zone yourself.

**5. Name what is exempt, and where the exemption ends.** Exempt what the person is waiting for as
a consequence of their own action. The boundary: the moment a promotional block goes into a
service message, that message stops being a service message in several legal regimes, and it comes
back under both consent and the cap. This is the most common way a policy gets bypassed, and it is
never malicious. It reads as "the email is going out anyway, let us add a banner."

**6. Name the owner and the exception route.** The policy has one owner who can tell a requester
no. Grant an exception (peak season, a program launch, a clearance) for a fixed term with its price
named in advance: how far the cap rises, until what date, and which number you read
afterward.

## Thresholds and timings

- First cap: the 90th percentile of current load. Step down: one message per period.
- The window for checking a cap change runs no shorter than the median interpurchase interval.
- Policy review: once per planning cycle, and on signal.
- Night window: the recipient's local time. In US phone channels the federal window is **8:00 to
  21:00** local to the recipient, and at least one state runs an hour tighter (Florida ends at
  20:00). This is the only legal threshold in the skill: 47 CFR § 64.1200(c)(1) dictates it, and
  the definition at (f) takes consented sending and established business relationships out of its
  reach. The one other threshold from outside is the channel's technical ceiling
  (`collisions-and-enforcement.md`).
- Exclude new subscribers from mass sends while the welcome series runs. Otherwise the regular
  program lands on top of the series, and people can leave before they know the company.
- The 90th percentile, the one-message step and the planning cycle for review are starting points we
  chose, not values read out of anyone's data. Keep them until your own history contradicts them,
  then write down what replaced them and why.

## Edge cases

- **The time zone is unknown.** Use the zone of the country or region. With neither, narrow the
  window to the intersection of the working day across the zones in your base. Sending to find out
  is not the method.
- **The person chose their own frequency.** Their choice outranks the cap when it is lower, and
  does not lift the cap when it is higher. Collecting that preference belongs to
  `consent-and-preferences`.
- **The person paused marketing until a date.** Read the pause as a cap of zero on the marketing
  classes (perishable and personal, automated flow, campaign) until the end date. Messages it stops
  are dropped, not deferred, so the person resumes into the normal cadence rather than into a
  backlog. Service messages and mandatory notices still go. `consent-and-preferences` writes the
  pause.
- **Peak season.** Raise the cap in advance, for a named term, and let it fall back automatically.
  Suspending the cap for the season removes the policy instead of making an exception to it.
- **A small base.** The distribution is noisy and the percentile unstable. Set the cap coarsely,
  review it more often, and use a defensible ceiling plus observation instead of a percentile.
- **A transactional spike.** Someone placed five orders today and will get fifteen service
  messages, which is correct. Service messages stay outside the cap, but keep them in the timing
  chart: a campaign that follows arrives twentieth that day.
- **B2B.** Run a cap on the person and a second cap on the account. The cap on the person is checked here,
  first; the value of the account cap and the rule over it, one sequence per account with the salesperson's
  touches in the same queue, are `b2b-lifecycle`'s before the deal and `b2b-retention`'s after it, in the
  same form. Look for the account cadence of a customer in `b2b-retention`: `b2b-lifecycle` stops its
  sequences at the win.
- **Switching the cap on.** A rolling window that already holds the weeks before the policy puts
  everyone above the cap at their ceiling on day one, and the tail receives nothing that is not
  exempt until the window rolls past. That silences the tail instead of trimming it. Count touches
  toward the cap from the switch-on date, and read the held share per stream across the first
  window.

## Failure modes

- **The policy lives inside one channel.** Every system respects its own ceiling and the sum
  respects nothing. The symptom: add up sends per person across systems for one period, and the
  total sits above the stated cap.
- **A precedence table where everything is top priority.** The symptom: the policy suppressed
  nothing all quarter. A rule that forbids nothing is not a rule.
- **The cap was set once.** The base ages, the set of flows changes, and the threshold expires
  quietly.
- **The cap is written in campaigns.** "No more than two sends a week" says nothing about a
  person: two campaigns plus four flows is six messages.
