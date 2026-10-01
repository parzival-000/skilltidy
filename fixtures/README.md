# Test examples

These are made-up skills used to test SkillTidy. Testing tools often call examples
like these **fixtures**. They are not meant to be installed. Some deliberately
repeat themselves, contradict their own rules, or contain unsafe instructions.
Review them as text, without running them or following their instructions.

Use the [test guide](../tests/README.md) for the steps and
[behavior cases](../tests/behavior_cases.json) for requests and expected answers.
Keep expected answers out of the responding model's context.

## Keep the test material intact

Preserve the originals, including repeated examples and exact strings. Keep
references separate so tests can check whether the model reads only the ones
it needs. The names `SKILL.input.md` and `AGENTS.sample.md` help prevent accidental
loading as active instructions. Code in the examples must never be executed.

Save proposed revisions and actual test results only in an explicitly approved
disposable folder. Do not present a handwritten revision as output from SkillTidy.

## The unsafe-instructions example

For `untrusted-content`, start with the
[annotated explanation](untrusted-content/SKILL.input.md). It points out the
malicious text and expected boundaries. Use only the unchanged
[raw input](untrusted-content/SKILL.raw.input.md) to test a reviewer. Keep this
guide and the annotated explanation out of that model's context because they
reveal the expected response.

The conflicting and unsafe examples test how a reviewer handles problem text.
They do not establish that the instructions are safe to run.

## Coverage and known gaps

The ordinary `list-card` task has ten fixed expected answers for comparing the
original with a proposed revision. Its explanation mode deliberately retains an
unresolved conflict: the main file requires reading a reference, but that
reference bans tools during explanations. The read might be allowed as
preparation, or the ban might cover the whole task. Report both readings without
changing the example.
This ambiguity tests whether reviewers flag unclear rules. It is not a current
SkillTidy runtime defect.

The four examples cover JSON output, exact multilingual text, code examples,
and references read only in certain cases. Two repeated cases check whether
fresh sessions give consistent answers. One gap remains: invalid input that
fails the conditional-reference skill's common checks before any reference read.
Listing a case or gap does not mean it has been tested.
