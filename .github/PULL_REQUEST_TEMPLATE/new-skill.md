## New skill

**Skill:** <!-- slug, the name agreed in the issue -->

**Issue:** <!-- "Closes #123". Required: the maintainer accepts a new skill in an issue before work
starts. A pull request for a skill without an accepted request gets closed. -->

## What the skill covers

<!-- The work it serves, in two or three sentences, and the requests from the issue it answers. -->

## Boundaries

<!-- The neighboring skills closest to this one, and which questions stay with each of them. -->

## Mechanics

<!-- One row per mechanic file. -->

| File | Entry and exit conditions | Steps | Thresholds and timings | Edge cases | Failure modes |
|---|---|---|---|---|---|
| | | | | | |

## Sources

<!-- For every legal or channel rule: the body, the document, the section, the URL and the date you
opened it. For a mechanic you know from one market only: two independent sources showing that the
practice exists elsewhere. -->

## Checks

- [ ] `SKILL.md` has the frontmatter and the six sections from `AGENTS.md`, in order, with both Limits
      blocks copied character for character.
- [ ] The skill has at least two mechanic files and one definition file, or `SKILL.md` says why a single
      mechanic file is enough.
- [ ] The control metric has a numerator, a denominator and a window, and says what to do when someone
      asks what is normal.
- [ ] Every neighbor in `When to use something else` hands the matching question back to this skill in its
      own table.
- [ ] The skill names a vendor or a sum of money only where a cited rule does, and counts time from an
      event, not as a fixed number of days.
- [ ] Every number belongs to a class under Numbers in `AGENTS.md`.
- [ ] I ran the three passes in `AGENTS.md` on every file I added or changed.
- [ ] I added the skill to the README table and to the skill lists in the issue forms, and updated the
      skill counts in the root files and manifests.
- [ ] `python scripts/validate` shows no new errors, and I read every warning.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
