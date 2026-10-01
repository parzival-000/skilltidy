# Validation summary

## Automated checks

Recorded automated runs passed **36/36 tests**
in both the reviewed copy and a clean export, with no failures or skips. It checks
the measurement helper, packaging, metadata, fixture layout, documentation links,
and helper examples.
The [test guide](README.md) has the command and coverage details.

## Historical behavior checks

Earlier evaluations recorded **14 matched original/candidate pairs with
28 passing responses**, including two repeats, covering structured output,
multilingual text, code examples, and conditional references. Some responses
were reused only after the original, candidate, and context hashes matched.
These results apply to those specific historical inputs. Model evaluations
were not rerun during the later documentation updates.

The structured-output example linked from the repository README went from
**401 to 365 words** across two edits, and its reviewed candidate preserved the
validation rules, JSON format, and example. Fewer words alone do not establish
equivalent behavior.

### Generated candidates

Word counts cover the whole file, including metadata and examples, and exclude
unchanged references from both the original and candidate. The table records
historical measurements, not reduction targets.

| Fixture | Original | Candidate | Fewer words |
|---|---:|---:|---:|
| Structured output | 401 | 365 | 9.0% |
| Multilingual | 397 | 371 | 6.5% |
| Code examples | 337 | 320 | 5.0% |
| Conditional reference | 693 | 670 | 3.3% |

## Limitations

- Earlier reviews produced incorrect diffs, altered escape characters, and
  missed ambiguous rules. Later focused checks addressed specific failures,
  but did not retest every workflow after every revision.
- Cross-platform behavior, real missing-Python and unreadable-file conditions,
  automatic skill selection, and every conditional branch remain unverified.
- The conditional fixture's common-invalid-input/no-reference branch is still
  a coverage gap.
- The list-card fixture deliberately retains the explanation's unresolved
  reference-read/tool-ban ambiguity. It tests how reviewers report unclear
  rules. It is not a current SkillTidy runtime defect.
- Later documentation updates did not rerun model evaluations, installation
  checks, or security scans. Historical scanner evidence was incomplete and
  does not establish security certification.

These checks do not guarantee equivalent behavior on every task, so test changes
on representative tasks before relying on them. This public summary omits
detailed development chronology and machine-specific information.
