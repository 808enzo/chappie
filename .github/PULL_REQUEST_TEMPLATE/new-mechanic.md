## New mechanic

**Skill:** <!-- slug -->

**Issue:** <!-- "Closes #123", or "none" -->

**What you're adding:**

- [ ] A section in an existing file
- [ ] A new file in `references/`

## The situation it serves

<!-- What a practitioner is trying to run, and where the skill stopped telling them what to do. -->

## Where each part of the mechanic lives

<!-- A new section may complete a mechanic that already exists. Then name the existing heading for
the parts you didn't change. -->

| Part | File and heading |
|---|---|
| Entry and exit conditions | |
| Steps | |
| Thresholds and timings | |
| Edge cases | |
| Failure modes | |

## Sources

<!-- For every legal or channel rule: the body, the document, the section, the URL and the date you
opened it. For a mechanic you know from one market only: two independent sources showing that the
practice exists elsewhere. Write "none" if the mechanic quotes no rule. -->

## Checks

- [ ] A new file in `references/` has its frontmatter, and the Reference map in `SKILL.md` lists it.
- [ ] Every metric the mechanic relies on has a numerator, a denominator and a window, in a definition
      file.
- [ ] If the mechanic touches a neighboring skill, the `When to use something else` tables on both
      sides name the boundary.
- [ ] The mechanic names a vendor or a sum of money only where a cited rule does, and counts time from an
      event, not as a fixed number of days.
- [ ] Every number belongs to a class under Numbers in `AGENTS.md`.
- [ ] I ran the three passes in `AGENTS.md` on every file I added or changed.
- [ ] `python scripts/validate <slug>` shows no new errors, and I read every warning.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
