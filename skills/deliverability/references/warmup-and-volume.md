---
claim_type: mechanic
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Warmup: earning the right to volume, one provider at a time

The unit here is **a step of the ladder at one provider**. Reputation belongs to the pair of a
sending identity and a provider, so a single ladder does not exist: you run as many as you have
providers worth reading, and the strictest of them sets its own pace.

A warmup is not a waiting period. It is a sequence in which each step is authorized by what the
previous step produced.

## Entry conditions

The identity is configured (`sending-identity.md`) and at least one of these holds: the domain or
subdomain is new; the IP or the sending platform is new; sending has been paused for longer than
subscribers remember signing up; or the sender name has changed enough that recipients may not
recognize it.

## Exit conditions

A working volume at which provider signals hold steady across two consecutive reading windows. The
step you stopped on is written down, along with the signals that would authorize the next one.
**Stopping below the planned volume is a legitimate exit**: a smaller program that arrives beats a
larger one that does not.

## Steps

**1. Choose the audience before the volume.** The first step goes to people who responded recently,
measured by your own shortest response window, which is the period inside which most responses to
an ordinary send arrive. The volume of the first step is the size of that audience. It is not a
number you pick.

**Recently responded means recently responded to mail.** To a provider, an active person opens and
clicks. To the business, an active person buys. Those populations overlap and do not coincide, and
a warmup audience built from the business definition contains people who never open anything, which
is what the provider is measuring. Get it backwards and every step is authorized by signals from
people who were never going to respond, so the ladder runs and the reputation does not move.

**Each later step is one widening of that window, and the ladder has no other move.** The first
step takes the people inside your shortest response window; the second takes the window one notch
wider, and so on out to the whole base you are entitled to mail. Volume is not set separately: it
follows from the audience, which is why a step never carries a number of its own. The people each
notch adds have responded less recently than the people already in, which is exactly the gradient
the provider is reading. Write the notches down before you start, so a step is a decision you
already made rather than one you take under pressure.

**2. Warm each provider on its own ladder.** Their thresholds and their tolerance for new senders
differ, and a single ladder across the whole base means either the strictest provider sets the pace
for everyone or the pace of the others breaks it. In practice: give the strictest
provider with real weight in your base a slower ladder of its own, and let the rest run together.

**3. Switch off everything dragging the numbers down, for the duration.** Flows with the lowest
response, sends to people who have been silent a long time, and content that has drawn complaints
before. **Count automated flows in the total.** They run at their own times, their volume looks
trivial one message at a time, and on the days several of them fire they add a spike on top of your
planned step that nobody planned and nobody sees.

**4. Spread each step out in time.** Rate limiting is a required setting, not a refinement. The
same thousand messages sent over an hour and sent in one minute read differently to the receiving
side, and the second one can trip volume limits that the first never approaches.

**5. Authorize the next step by signal, not by schedule.** Four signals, all read on the pair
rather than averaged across the send: the refusal share has not risen, the complaint share sits
inside the provider's published threshold, the reputation shown in that provider's postmaster tool
has not fallen, and response has held. A calendar cannot authorize a step, because the calendar
does not know what the provider saw.

**6. Know the shape of the step.** Google states the rule directly: the more mail you send, the
more slowly you should increase the volume, and the more frequently you send, the faster you can.
It also names the move to avoid, doubling a previous volume suddenly, and notes that sending at a
consistent rate beats sending in bursts. Those are Google's statements about mail to Gmail, opened
on the date in `SKILL.md`; other providers publish less, and the shape generalizes better than any
number would.

**7. Step back at the first adverse signal.** Rising refusals, messages being deferred, a
postmaster reputation moving down a level. Google describes the response to its own volume error in
detail: on error `4.7.28` you stop sending for at least ten minutes, resume on a single connection,
and add connections one at a time; and where messages start bouncing or being deferred, you reduce
volume until the error rate falls and then increase again slowly. Stepping back costs one step.
Pressing on costs the warmup.

**8. Record the working point.** The volume reached, the notch the window sits on, and the step you
stopped on. Stopping records where you are, and it is not clearance to mail the rest of the base:
reopening the ladder later means running the next notch as a step like any other, with its own
signals.

## Thresholds and timings

- **First-step audience:** your own shortest response window, computed from your own sends. It is a
  parameter of your data, not a figure to copy.
- **Step size:** not a number. The rule from the provider is proportional, larger volume means
  slower increase, more frequent sending allows faster increase.
- **Reaction to a volume error:** the provider's own instruction, quoted at step 7, and it belongs
  to the provider that issued the error rather than to sending in general.
- **Reading window for a step:** the longer of 48 hours after the send and your platform's retry
  ceiling. The 48 hours are a starting point: they hold for email, where responses keep arriving
  for days, and they are wrong for you as soon as you can plot your own curve of when responses
  arrive, so replace them with the point by which most of your responses have landed. The retry
  ceiling is the other half of the rule, because deferrals resolve inside it and a step read before
  they do is read on a denominator that is still moving.
- **Stability for exit:** two consecutive reading windows with no signal moving the wrong way.
- **One change per step, and the widening is that change.** The audience and the volume move
  together by construction, because the volume is the size of the audience. Everything else holds
  still for the length of a step: the sending rhythm, the mix of what you send, the rate limit, the
  identity, the template. Move any of those in the same step and no signal tells you what the
  provider reacted to.

## Edge cases

- **Service mail during a warmup.** It cannot be switched off and it goes to whoever triggered it
  rather than to the chosen audience. Separate identities (`sending-identity.md`, step 2) are what
  make a warmup possible without stopping the business; where they do not exist, move the service
  stream to another identity for the duration.
- **The business wants the volume now.** Do not argue for patience, state the price: every attempt
  to accelerate that fails sets the ladder back and lengthens the whole warmup, so the fast route
  is the slow one. A number of failed attempts named in advance moves the conversation better than
  a request to wait.
- **Same domain, new IPs, after a platform move.** The provider sees a new sender even though the
  domain is old, because domain reputation and IP reputation are held separately. Plan the warmup
  as if the identity were new, and expect the domain's history to help rather than to substitute.
- **A dedicated IP proposed as a fresh start.** A blank record is the absence of reputation, not a
  good reputation, and warming a new dedicated IP takes longer than repairing a shared one that
  still works. If the reason for wanting it is a placement failure, the answer is
  `placement-recovery.md`, not a new address.
- **The domain has sent before, but rarely.** Warm it anyway. The provider reads the history of the
  flow, and an old domain with almost no sending history is a new sender with an old registration
  date.
- **The base is too small for the steps to differ.** Skip the ladder: send to the whole audience
  and read the signals. Steps only mean something when a step is large enough for the provider to
  notice the difference.
- **Two brands warming at once on one platform.** They are two identities and two ladders. Warming
  them as one means a signal from either can stop both and neither can be diagnosed.

## Failure modes

**Repeated warmups produce nothing.** The sign: response at one provider never rises above
where it started while the others behave normally. The ladder is not the problem. Look for a flow
that was never switched off, an audience picked on business activity rather than response, or a
cause that belongs to `placement-recovery.md` and was never a warmup problem at all.

**Every step is authorized and the volume stops growing.** The sign: the signals stay green and the
next step cannot be filled with people. Check the notches first. A ladder that stopped widening
has not run out of people; it stopped. Where the window really has opened out to the whole
mailable base, the people beyond it are not an intake problem but a lapsed one, and bringing them
back is `lapse-and-winback` running after the warmup rather than inside it. Only once that is done
too is the ceiling a question about intake for `onsite-capture` and `list-building`.

**The warmup finished, the signals hold, and revenue did not come back.** The expected outcome when
the audience was narrowed. Do not widen it again in one move. Record that the channel
now runs at a smaller volume, and let `email-program` decide whether to rebuild reach from the
intake side.

**Automated flows kept running and nobody counted them.** The sign: the ladder looks orderly on
paper and the provider reacts to volumes you never planned, landing on the same days each month.
Add every automated send to the step it lands in before you plan the next one.
