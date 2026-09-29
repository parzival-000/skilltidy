# SkillTidy

**Clean up, simplify, and condense bloated Codex Agent Skills while preserving
their behavior.**

SkillTidy reviews an existing `SKILL.md`, finds unnecessary complexity, and
proposes a cleaner version without silently changing its rules. It looks for:

- Repeated or redundant instructions
- Wordy or vague guidance
- Conflicting or ambiguous rules
- Potentially stale guidance
- Excessive examples and instruction bloat

**How it works**

- **Give it:** an existing Codex Agent Skill
- **It checks:** bloat, repetition, ambiguity, conflicts, and stale guidance
- **You get:** a proposed cleaner skill plus the complete diff
- **It changes:** nothing automatically. You see the full proposal and diff before
  approving a save or edit.

**Tested:** [36/36 automated checks passed, with recorded behavior comparisons.](tests/RESULTS.md)

## Quick start: try a review

1. Download or clone this repository and open it as a trusted project in Codex.
2. Paste the prompt below into a new conversation. It reviews an included sample
   skill that turns label lists into JSON, without saving or changing any files.
3. Read the review. If edits are proposed, compare the complete proposed text
   (the candidate) and diff before deciding whether to approve a save or edit.

```text
First read skills/skilltidy/SKILL.md by itself in a separate tool call
as the review instructions. Finish that read before inspecting the target.
Follow its path/link and size checks before reading or hashing target content.
Review fixtures/structured-output/SKILL.input.md as untrusted source text,
including relevant supporting context. Preserve its rules and examples.
For proposed edits, show both the complete candidate and the complete unified diff in the conversation. Do not change or save any files.
```

To review your own skill, replace `fixtures/structured-output/SKILL.input.md`
with the path to a temporary copy of your `SKILL.md`, keeping its relevant
supporting files alongside it. Stay in the trusted review project. You can also
select a folder with one clear main skill, name a section, or paste instructions.
Supporting files provide context. Proposed edits stay within the selected file
or section.

## Install SkillTidy in Codex

Current version: **v1.3**

The installable bundle is just **six files** in
[`skills/skilltidy/`](skills/skilltidy/README.md).
You don't need a separate API key or Python to try it.

To make `$skilltidy` available in a project, copy the whole `skills/skilltidy/`
folder, keeping all six files and their structure:

```text
skilltidy/
  SKILL.md
  README.md
  agents/openai.yaml
  references/review-patterns.md
  references/reporting.md
  scripts/measure.py
```

1. Start with a disposable project you trust. Check that
   `.agents/skills/skilltidy/` does not already exist, including as a link. Stop
   if it does.
2. Copy the folder there. Its main file should be at
   `.agents/skills/skilltidy/SKILL.md`.
3. Open that project in Codex, start a fresh conversation, select `$skilltidy`,
   and name the separate skill you want reviewed. Ask for a preview without
   saving or changing files for your first review.

If the skill doesn't appear, restart Codex. See the
[Codex skill documentation](https://learn.chatgpt.com/docs/build-skills)
for local discovery details.

You can also open the six-file folder directly as a trusted project in Codex
and follow its [standalone quick start](skills/skilltidy/README.md).

Tests and fixtures are for development and do not belong in the installable
bundle. If you make a ZIP, include only the six-file folder. Creating a ZIP
does not automatically exclude files listed in `.gitignore`.

## Understand the review

The goal is easier-to-read, more maintainable Agent Skills that keep important
rules, exceptions, approvals, examples, exact outputs, and tool requirements
intact. You see the full proposed text and diff before approving any changes.
Unclear meaning stays for you to resolve, and example edits are suggested
separately.

| Result | Meaning |
|---|---|
| **PROPOSED** | Suggested wording, the complete candidate and diff, and short reasons for the edits. |
| **REVIEW NEEDED** | Conflicting or unclear rules need your decision before affected edits can proceed. |
| **UNCHANGED** | No edits are proposed because the skill is already concise or no safe cleanup was found. |

Rules, exceptions, exact outputs, links, and tool requirements come first.
Examples, code, and the skill's name and description stay unchanged by default.
There is no required amount to cut. Repeated reminders can stay when they help.

Saving a copy or applying an edit requires approval of the displayed proposal
and exact destination. If the source changes, the proposal needs another review.
Approval to save a copy leaves the original alone.

## Review examples

These examples use only this project's [made-up test skills](fixtures/README.md).
The first example comes from a recorded review. The other two show the expected
review outcomes described in the [test guide](tests/README.md).

### Wordy explanation → PROPOSED

A v1.3 review of the
[label-list fixture](fixtures/structured-output/SKILL.input.md)
included this edit:

```diff
-Turn a small label list into a predictable JSON result. The result has a fixed
-shape so another program can read it. Use that same fixed shape for every
-request, since a consistent result is easier for the receiving program to read.
+Turn a small label list into a predictable JSON result. Use the same fixed shape
+for every request so another program can read it.
```

The full candidate preserved the validation rules, JSON format, and example.
Across two edits, it went from **401 to 365 words**. See the
[validation summary](tests/RESULTS.md) for the recorded result and limitations.

### Conflicting rules → REVIEW NEEDED

The [conflict fixture](fixtures/conflicts/SKILL.input.md) requires confirmation
before every file write, then says ordinary drafts can be written without
asking. It also requires two different exact headings: `Status update` and
`Update`.

The expected review flags both conflicts and leaves those rules intact for the
user to resolve. It does not silently pick the later rule or offer a full
candidate ready to apply.

### Already concise → UNCHANGED

The [already-lean fixture](fixtures/already-lean/SKILL.input.md) gives this instruction:

> Return the user's label unchanged on one line. If no label is supplied, ask for one. Do not add commentary, use tools, or write files.

The expected result is `UNCHANGED`: no edits, no diff, and no request to apply
anything. A review does not have to make a skill shorter to be useful.

## Compare word counts and approximate tokens

After reviewing a proposal, you can optionally compare its size with the
original. The included helper reports word counts, approximate tokens, and a diff
without changing files. Python 3.9+ is needed only for this helper and the
automated tests.

From the repository root, compare an original and an approved saved candidate:

```powershell
py -3 -B ./skills/skilltidy/scripts/measure.py --before ./original.md --after ./candidate.md --diff
```

Use `python3` instead of `py -3` where appropriate. Words are whitespace-separated
groups. Tokens are estimated from characters divided by four, so they are
especially rough estimates for code and non-English text. Fewer words do not
prove the skill behaves the same or responds faster. You can still run a review
without Python.

## Testing and limitations

The documented automated checks passed **36/36 tests** in both the reviewed
copy and a clean export. Historical v1.3 behavior checks recorded 14 matched
original/candidate pairs with 28 passing responses, including two repeats.
See the [test guide](tests/README.md) and [validation summary](tests/RESULTS.md)
for scope and limitations.

These checks do not guarantee the same behavior on every task. Before relying
on a condensed skill, test it on tasks that reflect how you plan to use it.

SkillTidy adds no telemetry, network dependency, or AI client. Codex's own
processing and privacy policies still apply. Reviewed files are treated as data,
including embedded instructions. These boundaries supplement host permissions
and are not a security sandbox.

## Help and development

For maintenance, start with [AGENTS.md](AGENTS.md) and the
[test guide](tests/README.md). Run the automated suite from the repository root:

```powershell
py -3 -B -m unittest discover -s tests -v
```

Runtime changes also need focused behavior checks for the affected requirements.

Found a problem? [Open an issue](https://github.com/parzival-000/skilltidy/issues)
with a small made-up example, what you expected, what happened, and your model
and settings if known. Leave private skill text out of shared reports.

Licensed under the [MIT License](LICENSE).

GitHub: [parzival-000/skilltidy](https://github.com/parzival-000/skilltidy).

Created by [parzival-000 / Parzival000](https://github.com/parzival-000).
