---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# When mail stops arriving: diagnosis and the way back

The unit here is **an incident on one pair of a sending identity and a provider**. The order of the
steps is the mechanic: worked out of order, you will rewrite copy for a problem that turns out to
be an authentication record, or move platforms for a problem that moves with you.

## Entry conditions

One of three signals:

- the provider response index for one provider has fallen across two consecutive reading windows
  while the others hold;
- the refusal share or the complaint share has crossed a threshold the provider publishes;
- an explicit refusal arrived: an error code you have not seen before, a postmaster notification,
  or a listing on a public blocklist.

The third signal opens the mechanic immediately. Waiting for a volume of refusals to accumulate is
how a silent block gets a month's head start. One weak send does not open the mechanic.

## Exit conditions

The cause is named, fixed, and the provider's index holds across two consecutive reading windows.
Volume returns on the ladder in `warmup-and-volume.md` rather than in one move.

## Sequence, and the order is the mechanic

**1. Separate acceptance from placement.** Two failures that look identical from the report and
have nothing in common underneath. The provider **did not accept** the message, in which case there
is a code, a refusal and something to read; or it **accepted the message and filed it out of
sight**, in which case nothing comes back at all. The first is fixed through records and list
quality, the second through reputation and behavior. Until they are separated, every fix is a
guess.

**Before you read an accepted-but-silent fall as placement, rule out rendering.** A template that
broke in the environment where most of a provider's readers open their mail lowers that provider's
clicks exactly as filing to spam does, and the provider response index cannot tell the two apart.
`email-design` splits the same provider by reading environment with its environment click index,
and the question that separates the cases is written on both sides: is the fall in this
provider's index spread across its environments, or concentrated in one? Concentrated in one, with
the provider's other environments up, is rendering: open the seed mailbox in that environment and
hand the case to `email-design` before you touch volume. Spread across, with the environment
indices where they were, is placement, and you continue here. **Where nearly all of a provider's
readers open mail in one environment, the numbers cannot answer the question.** That
environment's index sits at 1 by construction and barely moves when it breaks, so a rendering
defect there shows only as this index falling, which is the picture placement gives. Open the seed
mailbox in that environment first, and touch volume only after it.

**2. Confirm the message was handed over at all.** A flow that never gave the message to the
channel is `program-audit-and-ops`, not deliverability. The check takes a minute, and it decides
whether the incident belongs to you at all.

**3. Name the provider and the date.** The problem almost always sits at one provider and almost
always has a start date. Find both before changing anything: without the date you cannot line the
fall up against the event that caused it, and the event is what you are looking for.

**4. Line the date up against your own side.** A platform or IP change, a DNS edit, a volume spike,
a large contact import, a new flow, a changed sender name, a seasonal peak. Look here before you
look at the provider.

**5. Check four causes, cheapest check first.** The order is by what the check costs you, which is
the reverse of how often each turns out to be the cause.

1. **Authentication.** Open the authentication result of a message you received: SPF, DKIM, DMARC,
   and alignment. A lookup, not an investigation.
2. **Blocklists.** Look the domain and the sending IP up in the public lists. Also a lookup.
3. **The list.** The refusal share at this provider, the complaint share, and the proportion of
   addresses that have never responded. A query against your own data.
4. **Behavior.** Volume and its spikes, the mix of what you send, and how much of the audience has
   been silent. The dearest check to run and the likeliest cause.

**6. If a domain or IP is listed, fix the cause before requesting removal.** The order is strict:
find out what the listing is for, fix it permanently, then ask. A request without a fix is refused,
and repeated refused requests make the position worse. Who may ask depends on the list: the IP
lists take a request only from the network or hosting company that controls the address, so an
ordinary sender goes through their platform or provider, while a domain listing is handled through
the operator's own checker. Details and the sources are in `SKILL.md`. Do not move to a new domain
or a new IP to escape a listing: it reads as evasion rather than remediation.

**7. Narrow the audience to recent responders and switch off the low-response flows.** This is the
same action as the first step of a warmup, and here it is the main one: the provider needs to see a
flow that people react to. Keep service mail flowing, on a separate identity where you have one.

**8. Repair the list in the same pass, using the four classes of unreachable.** The state comes in
classes because they clear differently, and treating them as one is how a base loses healthy
addresses or keeps dead ones.

| Class | Set by | Cleared by |
|---|---|---|
| Permanent refusal | the provider answered with a permanent failure: no such address, the domain accepts no mail | **Never by a retest.** Only by the person's own act: a confirmed opt-in given again, or a transaction against that address |
| Temporary refusal | the provider answered with a temporary error: mailbox full, server unavailable | One accepted delivery in a controlled retest on rising intervals; past the ceiling of those intervals it becomes permanent |
| Complaint | the person reported the message as spam | **Never, by anything** except a new and explicit consent. This is the person's refusal, not a property of the address |
| Provider block | the refusal is about your reputation, not about the address | Cleared with the incident, at once and for every address at that provider, because it is a property of the pair |

**Two of the classes arrive as the same event, so read the class on the pair rather than on the
address.** A temporary refusal and a provider block both come back as a refusal, and the refusal
itself does not separate them. The number of addresses does: a full mailbox or an unavailable
server hits one address at a time, while a block raises the refusal share at one provider inside a
single send, and at that provider only. So before you classify anything, group the send's refusals
by provider and compare each provider's refusal share against its own recent sends. A provider
whose share jumped is an incident and its addresses take no class at all until the incident
closes; the rest are ordinary temporary refusals and go to retest. Skip this and the ceiling on
the retest intervals converts an incident into permanent refusals, the one state neither you nor
`list-building` can undo.

**Testing whether an address works by sending to it is the behavior that damages reputation.** So a
retest is allowed only for the temporary class, only on rising intervals, and only inside ordinary
sending. Never assemble a verification campaign addressed to everybody currently unreachable.

**The fourth class is the one that surprises people.** When a provider blocks a flow, every address
at that provider goes unreachable at once, including perfectly live ones. Clearing that state
address by address is meaningless, and deleting records on the strength of it removes a healthy
part of the base for an incident that had nothing to do with them. `list-building` needs the class
before it decides anything.

**9. Where the intake was the cause, close it there.** A batch of contacts that arrived through one
point and brought refusals with it is a question for that point: add confirmed opt-in, or stop
sending to the batch as a whole. Spam traps cannot be found by inspection, because nobody publishes
them, so the remedy is always the segment rather than the address.

**10. Contact the provider once your own side is clean.** Include the domain, the date, a sample
message with full headers, and what you changed. Some providers answer, some never do, so an answer
cannot be a step in the plan.

**11. Return the volume on the ladder.** `warmup-and-volume.md`, with the same stop rule. The
return is always slower than the fall.

## Thresholds and timings

- **Entry:** two consecutive reading windows of a falling index at one provider, or a single
  explicit refusal, which opens the mechanic at once.
- **Reading window:** no shorter than 48 hours after a send, and never shorter than your
  platform's retry ceiling. Forty-eight hours is a starting point for email, where responses arrive
  over days; replace it with the point by which most of your own responses have landed. The retry
  ceiling is the second half of the rule because the denominator moves too: deferrals resolve into
  acceptances or refusals over the retry window, and an incident produces both faster than an
  ordinary week does.
- **One change per reading window.** Otherwise the cause stays unknown even when the numbers
  recover, and you will not know what to avoid next time.
- **Retest of a temporary refusal:** rising intervals tied to your own sending rhythm, with a
  ceiling after which the address moves to the permanent class. Take rising intervals as a starting
  construction; where a large share of held addresses turns out to accept mail again, lengthen the
  ceiling, and replace the schedule entirely once you can measure that share across two cycles.
- **Delisting time:** set by the list, not by you. An approved domain removal is processed within
  minutes while local systems can lag up to a day; an IP listing goes through your provider and
  takes as long as that takes.

## Edge cases

- **Everything fell at every provider at once.** This is not placement. Look at your own side,
  broken authentication, a platform failure, a DNS edit, or at content and offer, which is
  `email-program` and `email-copy` rather than this file.
- **A silent block.** The provider stopped accepting without an error code and without a
  notification. Only the index and the postmaster tool show it; a diagnosis driven by refusals
  reports everything as normal, because the refusals never arrive.
- **The mail went to a promotions tab rather than to spam.** Not an incident. A promotional message
  sitting in the tab for promotional messages is where it belongs, and chasing the main tab with
  promotional mail is effort spent against the provider's own sorting. It is an incident only when
  a service message lands there, and the fix is separate identities.
- **Few complaints as a share, many as a count.** A small share of a large send is still a large
  absolute number, and providers read both. Report the share and the count together.
- **Trouble began after a large contact import.** A spam trap inside the batch is the likely cause
  and it cannot be located by hand. Stop sending to the segment, add confirmed opt-in at that
  intake point, and do not try to clean the batch address by address.
- **Somebody is sending as you.** The fall is caused by mail you did not send. DMARC reports show
  it as sources you do not recognize authenticating against your domain. From that point it is a
  security incident with a different route out, and tightening your policy is the containment step
  rather than the diagnosis.
- **The provider offers no postmaster tool.** Some do not. You are left with the index and the
  refusals, which is enough to detect and not always enough to explain. Say so in the report rather
  than treating an absence of data as a healthy reading.
- **The incident coincides with a seasonal peak.** Volume rose for a reason everybody knows, which
  makes it tempting to wait. Peaks are exactly when a spike breaks a ladder, so read the index per
  provider through the peak rather than after it.

## Failure modes

**The content gets rewritten while the authentication is broken.** The sign: weeks of edits, an
index that does not move, and nobody has opened the headers of a received message. The order in
step 5 exists against precisely this.

**A platform move is proposed as the cure.** The sign: the plan is to start clean somewhere else.
Domain reputation travels with the domain and new IPs need a new warmup, so the state after the
move is worse than before it. A move that was already planned should wait until the incident is
closed.

**The audience was narrowed, the numbers recovered, and the volume never came back.** The sign: the
index has been healthy for two quarters while the share of the base receiving anything keeps
falling. The recovery finished and the warmup was never started. Two numbers on one page catch it:
the index and the share of the base held back.

**Nothing recovers and all four causes came back clean.** The cause is outside the channel: the
offer, the assortment, the price. Say so, hand it to whoever owns the channel, and name which of
the four you cleared so the next person does not repeat them.
