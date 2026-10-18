# Contributing to SkillTidy

Small fixes, clearer examples, and useful problem reports are welcome. Keep each
change focused and explain what it improves.

## Report a problem or suggest an improvement

Use the [issue forms](https://github.com/parzival-000/skilltidy/issues/new/choose)
for problems and suggestions. For questions or general feedback, use
[Discussions](https://github.com/parzival-000/skilltidy/discussions).

For a problem report, include a small made-up input, your prompt, what you
expected, and what happened. Add your Codex version, model, and operating system
if known. Leave private skill text, credentials, and personal information out of
examples, diffs, and screenshots.

## Make a change

Read [AGENTS.md](AGENTS.md) and the [test guide](tests/README.md) before editing.
Keep changes within the issue or pull request's scope. The installable bundle is
the six files under `skills/skilltidy/`, so keep development material outside it.

Preserve rules, exceptions, approval requirements, exact outputs, examples, and
tool requirements when cleaning up instructions. Explain any intended behavior
change separately. A shorter skill is useful only if it still does the job.

## Run the checks

Use Python 3.9 or newer. From the repository root on Windows:

```powershell
py -3 -B -m unittest discover -s tests -v
```

On Linux or macOS, use `python3 -B -m unittest discover -s tests -v`.
The suite needs no extra packages or model access. GitHub Actions runs the same
checks on Windows and Linux with Python 3.9 and the latest stable Python 3.

These checks cover the helper, packaging, and documentation. Changes to skill
instructions also need focused behavior checks for the affected rules, as
described in the test guide. Keep model evaluations separate from automated
checks, and get approval before running model test batches or installation tests.

In your pull request, explain the change and report which checks passed, failed,
or weren't run. Use made-up examples and keep raw local review records out of Git.
