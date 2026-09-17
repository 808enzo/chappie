# Contributing to Chappie

There are two ways to contribute. Report a problem as an issue, and the maintainer makes the change.
Or make the change yourself and open a pull request.

To ask which skill fits your case or how to read a step, use
[Discussions](https://github.com/808enzo/chappie/discussions) instead. Issues are for changes to
the library. [SUPPORT.md](SUPPORT.md) lists where each kind of question goes.

Everyone who posts in issues, pull requests and Discussions follows the
[code of conduct](CODE_OF_CONDUCT.md).

Every file goes through the same review before it ships. The review checks that each step can be
carried out as written, that every legal or channel rule names its primary source and the date the
source was opened, and that every number says which kind it is. [AGENTS.md](AGENTS.md) spells out
those rules and the checks that go with them. Read it before you open a pull request.

## What to report

[Open an issue](https://github.com/808enzo/chappie/issues/new/choose) and pick one of five forms.
They are listed in order of how much each report is worth to the library.

### 1. A legal or channel rule has changed

Laws get amended, regulators publish new guidance, and mailbox providers, carriers, app stores and
messaging platforms change their requirements on their own schedule. When a rule quoted in a skill
no longer matches its source, report it with this form.

Bring:

- the skill, the file, and the sentence as it reads now;
- what the rule says today;
- a link to the primary source: the law itself, the regulator's page, or the platform's own
  documentation;
- the date you opened that source.

A blog post, a vendor summary or a news item tells you the rule may have moved. Add it as context
if it helped, and link the primary source it points to.

You don't need to be a lawyer to file this. The legal sections are not legal advice, and a source
that moved to a new address is worth reporting too.

### 2. A skill gets something wrong

Use this form for:

- a step you can't carry out as written, or a step that is missing;
- two files that contradict each other;
- a question handed to a neighboring skill that doesn't cover it;
- a broken link;
- an agent that gave you a market benchmark, or a figure with no rule, math or recipe behind it.

The last one counts as a defect. The library promises that a skill never invents a number, and
[ROADMAP.md](ROADMAP.md#on-numbers) lists the five kinds of number a skill may use.

Bring the request you gave the agent, the agent and model you ran it on, what came back, and what
you expected instead.

### 3. Installation fails

Name the method (`npx skills`, the Claude Code plugin, a ZIP upload in the Claude app, or copying
by hand), the agent and its version, and your operating system. Then give the exact commands you ran
with their full output, or, in the Claude app, the steps you took and the message the app showed.

### 4. A mechanic is missing

Use this form when a skill covers your area but stops short of your case: a step, an edge case, a
failure mode, a threshold or a variant of the mechanic is missing. Name the skill, say what you are
trying to run, and point to the place where the skill stops telling you what to do. "Our
replenishment reminder reaches people who already reordered in the store" gives the maintainer
something to work with. "Improve `repeat-purchase`" doesn't.

A request can end as a new section in the skill, a new file in its `references/`, or a refusal with
the reason.

### 5. A new skill

Use this form when no skill covers the work at all. Describe the work rather than the skill: what you
run, who it reaches, and which decisions you make along the way. Add two or three requests you would
give the agent, and the skills you read first with the reason none of them fits. A name is
optional, and the maintainer picks the final one.

A request can end as a new skill, a section in an existing skill, a line in
[ROADMAP.md](ROADMAP.md), or a refusal with the reason.

## What the library won't take

- **Market benchmarks.** A request for a typical open rate, a normal churn rate or an industry
  conversion figure gets closed. [ROADMAP.md](ROADMAP.md#on-numbers) explains why. To judge your
  own results, `metric-definitions` shows you how to build a baseline from your own periods.
- **Topics outside the territory.** Chappie starts where acquisition ends, so paid advertising and
  ad platforms, search, PR, social publishing and brand stay out.
- **Calls and voice, and AI inside the program.** Both are planned for version 2, and
  [ROADMAP.md](ROADMAP.md#not-in-version-1) gives the reason each one waits. Skip the issue.
- **Setup guides for one platform.** A skill describes the mechanic, and you run it on the stack
  you have. How to configure a specific email platform, CDP or CRM belongs in that vendor's
  documentation.

## Before you post

Issues and pull requests are public. Remove everything that identifies a customer or an employee:
email addresses, phone numbers, names, order and account IDs, rows from a CRM export. Replace them
with made-up values that keep the shape of the problem. Leave out your company's figures unless you
are free to publish them.

## After you post

An accepted report becomes a change in the library and an entry in [CHANGELOG.md](CHANGELOG.md).
The changelog also says how each change moves the version number: a rule updated to match its
current source ships as a patch, and a new skill, reference file or mechanic ships as a minor
release.

Suggested wording helps show what you mean. The maintainer writes the fix in the library's style
and runs it through the same review as every other file, so the text that ships may read
differently from your suggestion.

## Propose a change

### Start with an issue when the change is large

A new skill needs a request, filed with the new skill form, that the maintainer has accepted before
you start writing. Renaming,
merging or removing a skill is the maintainer's decision, so don't open a pull request for one. A
rule update, a fix, or a new mechanic in an existing skill may go straight to a pull request. If an
issue already describes the problem, say in it that you are working on a fix, so two people don't
write the same one.

### Make the change

1. Fork the repository and create a branch for one change. If a pull request fixes one skill
   and adds a mechanic to another, the maintainer asks you to split it.
2. Edit the files by the rules in [AGENTS.md](AGENTS.md), and run its three passes (market
   neutrality, evidence, style) on every file you add or change. If you work with an AI agent, point
   it to `AGENTS.md`. Claude Code reads it through `CLAUDE.md`.
3. Run the checks from the repository root:

   ```bash
   pip install pyyaml
   python scripts/validate <slug>
   ```

   Fix every error, and read every warning. A warning marks a sentence for you to check. Then run
   the searches listed under Checks in `AGENTS.md`.
4. Leave `CHANGELOG.md` and the version number alone. The maintainer writes both when the change
   ships.

### Open the pull request

Push the branch and open a pull request. The page opens with a short general form. For the form
that fits your change, add `?template=` and a file name to the end of the page's address, then
press Enter. If the address already contains a `?`, add `&template=` instead. For a fix from the
branch `fix-deliverability` in your fork, the address ends like this:

```text
compare/main...your-username:chappie:fix-deliverability?expand=1&template=skill-fix.md
```

The templates:

| Your change | Template |
|---|---|
| A legal or channel rule no longer matches its source | `rule-update.md` |
| A skill gets something wrong | `skill-fix.md` |
| Installation, the root files, the validator or the workflow | `install-and-docs.md` |
| A new section or a new file in `references/` in an existing skill | `new-mechanic.md` |
| A new skill, after the maintainer accepts the request | `new-skill.md` |

Fill in every field. The checklist at the end repeats the review in short form: check a box only
after you've done the step, and say why when one doesn't apply.

### Review

- The validator runs on every pull request. On your first pull request, the run waits for the
  maintainer to approve it.
- Keep "Allow edits by maintainers" switched on. The maintainer may adjust wording in your branch
  to fit the library's style, rather than send the pull request back for a small change.
- A pull request ends one of three ways: merged, returned with requested changes, or closed with the
  reason.
- The maintainer credits a merged pull request in `CHANGELOG.md` with your GitHub username.

### License

Chappie ships under the MIT license. By opening a pull request, you release your contribution under
the same license.
