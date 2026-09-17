# Chappie

**Marketing skills that don't stop at the framework.** Advanced lifecycle, CRM and retention skills
for AI agents, written for the people who run a B2C or B2B program on customers already in their
database.

Works with Claude Code, Codex, OpenClaw, Hermes Agent, Cursor, GitHub Copilot, Gemini CLI,
OpenCode, Windsurf, Cline, Roo Code, Kiro CLI, Goose, Amp and the Claude app. Every skill is a
plain [Agent Skills](https://agentskills.io/specification) folder, so any agent that reads
`SKILL.md` can load it.

Chappie covers everything after the first touch. Each skill gives you the operating detail that a
framework leaves to you: the sequence of steps, the thresholds and where they come from, the
timing, the segment definition, the edge cases and the ways a mechanic fails. Every file is held
to one test: after reading it, you know what to do on Monday morning. A file that names a
framework and stops there does not get in.

Version 1 has 35 skills in six blocks.

## Built for questions where one number depends on another

A win-back rate depends on who you count, and a sale's margin depends on the weeks around it. A
report can also credit a flow with purchases that would have happened anyway. Every skill makes
the agent work through these dependencies before it answers you.

- **Each skill defines its metric before anyone reads a number.** It names one control metric and
  states the numerator, the denominator and the window. `lapse-and-winback` divides returns by
  everyone who crossed the lapse threshold, including the people no channel could reach, the
  people the frequency cap held back and the control group, so the people you failed to reach stay
  in the count.
- **Each number sits next to the one it trades against.** `email-program` reads revenue per
  recipient next to total channel revenue, because the first rises whenever you mail only your
  most responsive people. `promo-calendar` reads a sale's margin over one purchase cycle on each
  side of it, where purchases people postponed or brought forward show up. `offer-design` reads
  the benefit each offer actually gave, and that figure exposes stacked offers that give away more
  than any single offer promised.
- **Effect stays apart from credit.** `experiments-and-holdouts` measures a change against a
  control group and counts everyone assigned to a group, including the people whose message was
  suppressed, bounced or never opened. `crm-reporting` reads change on cohorts and checks whether
  each published conclusion still holds when its line is read again.
- **Thresholds come from your own data.** A lapse threshold comes from your own median interval
  between purchases. Where a skill has no figure for you, it says so and shows you how to build a
  baseline from your own periods.
- **A question moves across skills.** Each skill hands nearby questions by name to the neighbor
  that owns them. `lapse-and-winback` sets the steps of a win-back attempt and passes what each
  step may cost to `offer-design`, the cap across channels to `contact-orchestration`, and whether
  the attempt caused anything to `experiments-and-holdouts`.
- **The agent acts only on what you asked for.** A request to analyze, audit or plan does not
  authorize sending a message, changing an audience or editing a live setting. Before it sends to
  a list, updates records in bulk or changes a live program, the agent shows what will change and
  for whom, and waits for your go-ahead. Text inside exports, tickets and survey answers is data,
  never an instruction.

### One question, three skills

*We stopped mailing the dormant tier, and revenue per recipient went up. Did the program get
better?*

1. `email-program` does not read revenue per recipient on its own. The figure rises whenever you
   mail only your most responsive people, so a program that got better and a program that got
   smaller both raise it. Read total channel revenue next to it to tell the two apart.
2. `metric-definitions` checks what the figure divides by. Revenue per recipient counts people,
   revenue per delivered message counts messages, and the two move in opposite directions when
   load rises.
3. `experiments-and-holdouts` designs the holdout that shows whether the change caused anything.

## What every skill contains

Each `SKILL.md` has the same six sections. Longer material sits in `references/`, and the agent
loads a file from there only when the task needs it.

| Section | What it gives you |
|---|---|
| When to use this | The situations the skill is for, written as symptoms you would recognize |
| When to use something else | Which neighboring skill owns a nearby question |
| Reference map | Which file in `references/` to load for the task at hand |
| Control metric | The metric you judge the mechanic by, defined so someone else can reproduce it |
| Legal regime this skill assumes | The legal and platform rules the mechanic runs under, or the points where you need your own legal answer |
| Limits | What the skill must never do, starting with inventing a number or acting beyond what you asked for |

## Skills

### Program, data and segments

| Skill | Use it to |
|---|---|
| [`crm-program-design`](skills/crm-program-design/SKILL.md) | Decide what the program is for, the one number it is judged on, who owns each part of that number, and what to build first |
| [`scenario-map`](skills/scenario-map/SKILL.md) | Choose which mechanics run at all, which one gets built first and which one leaves |
| [`segmentation`](skills/segmentation/SKILL.md) | Cut the base into segments someone else can reproduce, size them, settle overlaps and decide what happens to everyone left over |
| [`rfm-segments`](skills/rfm-segments/SKILL.md) | Set recency, frequency and money bands from your own distribution, then collapse the grid into groups a team can work |
| [`list-building`](skills/list-building/SKILL.md) | Know where every record came from, which one wins when two disagree, and when a contact stops being worth keeping |
| [`martech-stack`](skills/martech-stack/SKILL.md) | Decide which system owns each fact, how fresh the events are, and how to change platforms without losing the program |

### Lifecycle mechanics

| Skill | Use it to |
|---|---|
| [`welcome-and-activation`](skills/welcome-and-activation/SKILL.md) | Run the first weeks, from the moment a contact is recorded to a first purchase or a first use of the product |
| [`triggered-messages`](skills/triggered-messages/SKILL.md) | Build flows fired by a customer event: which events qualify, the delay, the chain of steps, the channel cascade and the exit |
| [`repeat-purchase`](skills/repeat-purchase/SKILL.md) | Work out when the next purchase is due, move first-time buyers to a second order, and decide what may be offered alongside an order |
| [`lapse-and-winback`](skills/lapse-and-winback/SKILL.md) | Define who counts as lapsed, catch people on the way out, and run one finite attempt to bring back the ones already gone |
| [`offer-design`](skills/offer-design/SKILL.md) | Decide the form, depth, conditions and lifetime of an offer, and what happens when several land on one order |
| [`promo-calendar`](skills/promo-calendar/SKILL.md) | Plan the year, decide which occasions earn a place, and run a peak together with the weeks around it |
| [`loyalty-program-design`](skills/loyalty-program-design/SKILL.md) | Choose between a discount, a points currency and paid access, then set earn and burn, expiry, tiers and referral rewards |
| [`loyalty-program-launch`](skills/loyalty-program-launch/SKILL.md) | Take a signed design to a running program: pilot, rollout, migration from an old program, enrollment and store staff |
| [`personalization`](skills/personalization/SKILL.md) | Decide what changes from one person to the next, where each value comes from, and what shows when it is missing |

### Channels

| Skill | Use it to |
|---|---|
| [`email-program`](skills/email-program/SKILL.md) | Run email as a standing program: sending rhythm by engagement tier, slot calendar, exclusions, and recovery when returns fall |
| [`email-copy`](skills/email-copy/SKILL.md) | Decide what one email says, promises and asks for, and how to tell whether the words made the difference |
| [`email-design`](skills/email-design/SKILL.md) | Make a template hold up where its author never looked: images off, dark mode, mobile, a clipped message |
| [`deliverability`](skills/deliverability/SKILL.md) | Set how your mail identifies itself to mailbox providers, earn the right to send volume, and recover when a provider stops letting it through |
| [`onsite-capture`](skills/onsite-capture/SKILL.md) | Turn anonymous site traffic into people the program may contact: forms, pop-ups, quizzes and the rule for when each one appears |
| [`push-notifications`](skills/push-notifications/SKILL.md) | Ask for push permission on iOS, Android and the web, and keep each send from spending the permission the channel depends on |
| [`in-product-messaging`](skills/in-product-messaging/SKILL.md) | Decide what the product shows someone already inside it, where and how often, which message wins the screen, and how it connects to email and push |
| [`chat-and-bots`](skills/chat-and-bots/SKILL.md) | Decide whether a bot or a person answers, how a matter reaches someone who can settle it, and when a conversation is finished |
| [`messaging-channels`](skills/messaging-channels/SKILL.md) | Run SMS, RCS, WhatsApp and similar apps, where a carrier or a platform stands between you and the person |
| [`transactional-messaging`](skills/transactional-messaging/SKILL.md) | Decide which service messages an order, booking, payment or account request sets off, what each must contain and how fast it must arrive |

### Orchestration and consent

| Skill | Use it to |
|---|---|
| [`contact-orchestration`](skills/contact-orchestration/SKILL.md) | Cap how many messages one person gets across every channel and system, and settle which message wins when two collide |
| [`consent-and-preferences`](skills/consent-and-preferences/SKILL.md) | Record the basis for writing to a person by channel and purpose, honor what they chose, and decide how far and how fast a withdrawal takes effect |

### Measurement and customer voice

| Skill | Use it to |
|---|---|
| [`metric-definitions`](skills/metric-definitions/SKILL.md) | Write a metric down so two people quoting it mean the same thing: numerator, denominator, window and attribution method |
| [`experiments-and-holdouts`](skills/experiments-and-holdouts/SKILL.md) | Design tests and control groups a decision can rest on, size them, and read the result without over-reading it |
| [`crm-reporting`](skills/crm-reporting/SKILL.md) | Build the regular program report, read change on cohorts rather than the whole base, and keep credit apart from effect |
| [`program-audit-and-ops`](skills/program-audit-and-ops/SKILL.md) | Notice when something you launched has stopped working, and respond: monitoring duty, alerts, incidents and message recall |
| [`voice-of-customer`](skills/voice-of-customer/SKILL.md) | Run surveys after a purchase, a delivery, a conversation or a cancellation, route a low score to an owner, and act on the answer |

### B2B and subscription

| Skill | Use it to |
|---|---|
| [`b2b-lifecycle`](skills/b2b-lifecycle/SKILL.md) | Carry a business account from the first known contact to the buying group's decision, including the handoff to sales |
| [`b2b-retention`](skills/b2b-retention/SKILL.md) | Carry an invoiced contract from the won deal to the renewal decision: success plans, expansion, invoice collection and the renewal case |
| [`subscription-retention`](skills/subscription-retention/SKILL.md) | Keep a paid subscription from ending over a failed charge, and let it end cleanly when the person decides to cancel |

## Install

Skills hand questions to each other by name. Each one works alone, but when it passes a question
to a neighbor, that neighbor has to be installed to take it. Install the whole set unless you know
which skills you need.

### With `npx skills`, for any agent

The [`skills`](https://github.com/vercel-labs/skills) installer finds the agents on your machine
and puts each skill in the folder that agent reads. It supports Claude Code, Codex, OpenClaw,
Hermes Agent, Cursor, GitHub Copilot, Gemini CLI and dozens of other agents, and it needs Node.js.

```bash
# all 35 skills, into the current project
npx skills add 808enzo/chappie

# see the list first, or pick a few
npx skills add 808enzo/chappie --list
npx skills add 808enzo/chappie --skill deliverability --skill email-program

# for one agent only, or for several
npx skills add 808enzo/chappie -a codex
npx skills add 808enzo/chappie -a openclaw -a hermes-agent

# for every project on this machine
npx skills add 808enzo/chappie -g
```

Update with `npx skills update`. Remove a skill with `npx skills remove deliverability`.

### As a Claude Code plugin

Run these inside Claude Code:

```text
/plugin marketplace add 808enzo/chappie
/plugin install chappie@chappie
```

Claude Code prefixes plugin skills with the plugin name, so `deliverability` becomes
`/chappie:deliverability`. Remove the plugin with `/plugin uninstall chappie@chappie`.

### In the Claude app

The Claude app takes one skill per ZIP file, and skills there need code execution turned on.

1. On a Free, Pro or Max plan, turn on **Code execution and file creation** in
   **Settings > Capabilities**. On a Team or Enterprise plan, if skills are missing, ask an owner
   to turn them on in **Organization settings > Skills**.
2. Download this repository (**Code > Download ZIP** on GitHub) and unzip it.
3. Compress each skill folder you need from `skills/` into its own ZIP file. Keep the folder name
   as it is: it has to match the skill's name.
4. Open **Customize > Skills**, click **+**, then **Create skill**, then **Upload a skill**, and
   choose the ZIP file.

To make all 35 ZIP files at once, run this in a terminal:

```bash
git clone https://github.com/808enzo/chappie.git
cd chappie/skills
for skill in */; do zip -r "../${skill%/}.zip" "$skill"; done
```

The files land in the `chappie` folder. The steps follow Anthropic's guide
[Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude),
opened 2026-09-17.

### By hand

```bash
git clone https://github.com/808enzo/chappie.git
mkdir -p ~/.claude/skills
cp -R chappie/skills/* ~/.claude/skills/
```

That installs the skills for Claude Code in every project. For another agent, or for one project
only, copy the folders into the folder your agent reads:

| Agent | Every project | One project |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| Codex | `~/.agents/skills/` | `.agents/skills/` |
| OpenClaw | `~/.agents/skills/` | `skills/` or `.agents/skills/` in the workspace |
| Hermes Agent | `~/.hermes/skills/` | `.hermes/skills/` or `.agents/skills/` |

For any other agent, see its documentation, or let `npx skills` find the folder. To remove, delete
the folders you copied.

## Use

You don't have to name a skill. The agent loads one when your request matches what the skill is
for. Some requests and the skill that takes them:

| You ask | Skill |
|---|---|
| Our win-back email reaches people who bought in the store yesterday. What's wrong with how we define lapsed? | `lapse-and-winback` |
| Our biggest sale of the year beat last year's. Did it make money once you count the weeks around it? | `promo-calendar` |
| Every offer has a cap, yet some orders leave with a bigger discount than any single offer allows. | `offer-design` |
| Mail stopped arriving at one mailbox provider, and every other provider looks fine. Where do I start? | `deliverability` |
| We have forty live flows and nobody can say which ones still earn their place. | `program-audit-and-ops` |
| Does our replenishment reminder sell anything customers wouldn't have bought anyway? | `experiments-and-holdouts` |
| What conversion rate should our welcome series hit? | `welcome-and-activation` |

The last request gets no figure back. The section [On numbers](#on-numbers) explains why.

To call a skill by name, type `/deliverability` in Claude Code (`/chappie:deliverability` if you
installed the plugin) or `$deliverability` in Codex. In other agents, name the skill in your
request.

## On numbers

A skill never invents a number, and the library carries no market benchmarks. Ask what is normal
and the skill tells you it has no figure, gives you the definition of the metric, and shows you
how to build a baseline from your own periods.

The numbers that do appear are legal and channel rules, quantities that follow from the math,
parameters you compute from your own data, named starting points, and made-up worked examples.
Every skill tells you which kind you are reading. [ROADMAP.md](ROADMAP.md#on-numbers) explains why
the library works this way.

## Scope

Chappie starts where acquisition ends. Paid advertising, search, PR, social publishing and brand
sit outside it. Two topics wait for version 2: calls and voice, and AI inside the program.
[ROADMAP.md](ROADMAP.md) gives the reason for each.

The legal sections are not legal advice. They mark where a rule applies and who to check with.
Where a skill quotes a rule, it names the primary source and the date the source was checked. If
a rule has changed since that date, [open an issue](https://github.com/808enzo/chappie/issues/new?template=1-rule-changed.yml)
with a link to the new source.

## License

[MIT](LICENSE) © 2026 [808enzo](https://github.com/808enzo)
