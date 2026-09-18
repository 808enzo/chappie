## Skill fix

**Skill:** <!-- slug; list every skill you changed -->

**Issue:** <!-- "Closes #123", or "none" -->

## What was wrong

- [ ] A step can't be carried out as written
- [ ] A step is missing
- [ ] Two files contradict each other
- [ ] A question goes to a neighboring skill that doesn't cover it
- [ ] The agent gave a market benchmark or an unexplained number
- [ ] A link is broken
- [ ] Something else:

**Where:** <!-- File and section. -->

**How you found it:**
<!-- By reading the file, or from an agent's answer. For an answer, give your request word for word,
the agent and model, and what came back. Replace customer data with made-up values. -->

## What you changed

<!-- The new wording or step, and why it fixes the problem. If you found the problem through an agent,
run the same request again and say what comes back now. -->

## Checks

- [ ] Every step, threshold, timing, edge case and failure mode outside the fix is still there.
- [ ] If the fix moves a question between skills, I changed both sides, and the neighbor's table doesn't
      hand it back.
- [ ] Every number in the paragraphs I changed belongs to a class under Numbers in `AGENTS.md`.
- [ ] I ran the three passes in `AGENTS.md` on every file I changed.
- [ ] `python scripts/validate <slug>` shows no new errors, and I read every warning.
- [ ] I left `CHANGELOG.md` and the version number to the maintainer.
