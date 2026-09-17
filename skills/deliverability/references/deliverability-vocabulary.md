---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Vocabulary for deliverability

The terms the three mechanics assume. The last section lists eight words this skill shares with its
neighbors, most of them under different meanings.

## The unit

**Sending identity.** A domain or subdomain, the signatures that prove mail under it is yours, the
Return-Path it answers on, and the IP or pool it leaves through. A provider forms opinions about
identities, not about companies.

**Mailbox provider.** The receiving side that decides whether to accept a message and where to file
it. Called the provider throughout. It decides independently of every other provider.

**The pair.** One sending identity and one provider, read over a period. The unit of this skill:
reputation, thresholds and incidents all live on a pair, which is why a number averaged across
providers hides the thing you are looking for.

## Acceptance and placement

**Acceptance.** The receiving server took the message. Observable, because a refusal comes back
with a code.

**Placement.** Where the provider filed the message after accepting it. Not observable: none of the
providers this skill names reports the folder it chose. Everything you know about placement is
inferred from how people respond.

**Delivered.** Accepted, and nothing more. A message in the spam folder was delivered. Reading
delivered as arrived is the confusion this skill exists to prevent, and it is why the control
metric is built on response rather than on delivery.

**Silent block.** A provider stops accepting or stops showing mail without an error and without a
notification. It leaves no refusals, so any diagnosis built on refusals reports normality.

## Refusals

**Hard bounce, or permanent refusal.** The receiving side states the failure is permanent: the
address does not exist, the domain accepts no mail. `metric-definitions` owns the formula; what to
do about it is here.

**Soft bounce, or temporary refusal.** The failure is stated as temporary: mailbox full, server
unavailable, message too large. It can become permanent through repetition.

**Deferral.** The receiving side asked you to try later. Not a failure yet, and one of the earliest
signs that volume is outrunning your reputation. It is also the reason acceptance is not final at
the moment of sending: a deferred message becomes accepted or refused later, so it enters the
control metric only once the retries have run out.

**Unreachable.** The state this skill sets on an address when delivery is technically impossible.
It has four classes with different clearing rules, and one of them is not about the address at all
(`references/placement-recovery.md`, step 8). The class travels with the state, because
`list-building` decides the fate of the record and the four classes carry opposite decisions.

## Authentication

**SPF.** The record naming which servers may send for a domain. One record per domain, and a limit
on how many lookups it may cost.

**DKIM.** A signature proving the message was not altered in transit and naming the domain that
signed it. Identified by a selector, so several platforms can sign for one domain without
colliding.

**DMARC.** The policy telling a provider what to do when authentication does not line up, and the
mechanism that reports back who is sending under your domain.

**Alignment.** The separate check that the domain in the From header matches the domain that signed
the message or the domain in the Return-Path. Passing SPF and DKIM while failing alignment is
common and is the usual reason a bulk requirement is not met.

**Return-Path.** The technical address failures are returned to. Sending through a platform puts
the platform's domain here by default, which is what breaks alignment.

## Reputation

**Domain reputation and IP reputation.** Held separately by the provider and combined at its
discretion. The domain's survives a change of IP; the IP's does not survive a change of IP, which
is why a platform move looks to a provider like a new sender using an old name.

**Shared IP and dedicated IP.** A shared address carries the behavior of everyone sending from it.
A dedicated one carries only yours, which is an advantage only above the volume at which the
provider sees you regularly.

**Spam complaint rate.** The share of accepted mail that recipients reported as spam. Providers
publish thresholds for it and compute it their own way, one of them on mail delivered to the inbox
rather than on everything accepted, so your figure and theirs will not match.

**Spam trap.** An address that belongs to no person, used to detect senders who did not collect
their list properly. Traps are not published and cannot be found by inspection, so the remedy is
always the intake point or the segment, never the individual address.

**Blocklist.** A published list of IPs or domains that a provider may consult. A listing is not a
legal finding, listing operators set their own removal rules, and removal is always free.

**Postmaster tools.** The provider's own reporting on the mail you send it: reputation, complaint
rate, authentication results, delivery errors. Each covers only that provider's domains, and some
providers offer nothing.

## Volume

**Warmup.** The ladder that earns the right to a volume at one provider. Not a waiting period: each
step is authorized by the signals of the previous one.

**Step.** One increment of the ladder at one provider, together with the audience it goes to and
the signals that will authorize the next.

**Response window.** The period inside which most responses to an ordinary send arrive. Yours to
compute. It sets the warmup audience and the reading window.

**Provider response index.** This provider's response rate on a send divided by the same rate
across the whole send. The control metric. Both halves are computed on messages providers accepted,
never on messages sent. Read per provider against its own median, because the division removes the
quality of the send from the number.

---

## Words this skill shares with its neighbors

**Hygiene.** Here it means the discipline of arriving in the inbox: refusals, reputation, and
validating addresses before a send. In `list-building` it means deciding who stays in the base.
The boundary is one sentence, and both skills state it the same way: **this skill sets the
unreachable state, `list-building` decides the fate of the record.**

**Active.** Here, and to a provider, active means somebody who opened or clicked recently. In
`email-program` it is an engagement tier, and to the business it means somebody who bought.
The populations overlap and do not coincide. A warmup audience assembled on purchases contains
people who never open anything, which is the signal the provider is reading.

**Suppression.** Here it means a hold placed for a technical reason, and its scope is the address
across every program and brand on the platform. `email-program` defines hard and program
suppression and their scopes, and this skill uses those meanings rather than new ones.

**Reputation.** Here it is a provider's assessment of a pair. No neighbor uses the word for
anything else, so nothing here needs disambiguating; it is listed because it sounds like a property
of the company and is not.

**Warm-up.** Here it is the volume ladder. In `promo-calendar` the warm-up is the run-up to a
window, the period in which demand is prepared before a peak. Same word, unrelated objects, and
both calendars can be running at once: a peak arriving during a volume ladder is the case where
they collide.

**Bounce.** Here it is the provider's signal and its class. In `metric-definitions` it is the
formula and the denominator of the bounce rates. Formulas there, thresholds and actions here.

**Complaint.** Here it is a provider signal that moves the reputation of a pair. In
`contact-orchestration` a complaint is a reachability loss event counted per person per period.
Both are correct and the denominators differ, so the two figures will not agree and are not
supposed to.

**Delivered.** Not redefined here, and worth stating: `metric-definitions` defines delivered as
what the receiving server accepted, with a deferred message on neither side until its retries run
out, which is exactly acceptance. Neither definition
includes the folder, and no metric available to you does.
