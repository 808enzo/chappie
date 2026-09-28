---
claim_type: definition
source: "internal synthesis"
source_type: internal
checked: 2026-09-12
---

# Control metric: how to read the first-pass share

`SKILL.md` defines the share of identified issues settled on the first pass: the cohort, the population, the
pass, the settle window, the return, the numerator, the denominator and the exclusions; why issues and not
threads, why the first pass and not CSAT, why returns default to the same issue, the blind spot of silence with
the two numbers read beside it, and the numbers not to promote. This file holds how to read it.

## The classes at read

Read every class of the denominator and where it goes: the split tells you which part of the work
failed. Put each issue in the first class that fits, in this order, because an issue nobody answered
is also an issue nobody may close.

| Class at read, in order | In the numerator | What it says | Where it goes |
|---|---|---|---|
| settled on the first pass | yes | answered, closed, and no return inside the settle window | |
| returned | no | the first answer did not settle it: wrong or partial, or closed before the matter was done | `references/bot-first-line.md` step 10 if the bot answered, `references/routing-and-assignees.md` step 8 if a person did |
| left inside the bot | no | never reached a person, and the bot gave no answer: scope, recognition, or an exit nobody could find | `references/bot-first-line.md` steps 2, 5 and 6; a handoff event with no arrival in the queue is a broken handoff route, for `program-audit-and-ops` |
| never claimed | no | reached a person's queue, and no agent claimed it within the longest time to closure: the capacity at that hour, or a group nobody reads | `references/waiting-and-off-hours.md` step 1; `references/routing-and-assignees.md` steps 3 and 11 |
| stuck | no | claimed, and not closed within the longest time to closure: no answer went out, it fell between agents or shifts, it passed its return date, or the closure rule was never applied | `references/routing-and-assignees.md` steps 5 to 8 |

**The wait is not a class here.** A person who left before anyone answered, and got the answer later
where they asked for it, is in the numerator when that answer settled the matter. The wait behind it
shows in the promise-kept number in `SKILL.md`.

## When a cohort's reading closes

- **The read date** of an issue is its first message, plus the longest time to closure you accept,
  plus its topic's settle window. Set the longest time to closure from your own history, as a late
  point of the time from first message to closure, and write it down. The settle window starts at
  closure, and an issue that is never closed never starts one; counting from the first message gives
  every issue a read date. Read the cohort when its last issue reaches its read date.

## Anonymous issues

**Anonymous issues are a separate line**, because a return cannot be observed for someone who was not
tied to a record when they wrote. For them, report the share that ended with an answer, or with a
stated time and place to get one, before the person left. Report the share of anonymous issues among
all issues too: when it grows, the main metric describes a shrinking part of your conversations.
