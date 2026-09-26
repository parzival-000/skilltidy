# Validation summary

Current version: **v1.3**

## Automated checks

The local suite passed **36/36 tests** in the proposed documentation update and
in a clean export, with no failures or skips. It checks the measurement helper,
packaging, metadata, fixture layout, documentation links, and helper examples.
See the [test guide](README.md) for the command and coverage details.

## Historical behavior checks

Earlier v1.3 evaluations recorded **14 matched original/candidate pairs with
28 passing responses**, including two repeats. These covered structured output,
multilingual text, code examples, and conditional references. Some responses
were reused only after the original, candidate, and context hashes matched.
These are historical results for specific inputs, not fresh model evaluations
of this documentation update.

The structured-output example linked from the repository README went from
**401 to 365 words** across two edits. Its reviewed candidate preserved the
validation rules, JSON format, and example. Fewer words alone do not establish
equivalent behavior.

### Generated candidates

Whole-file words include metadata and examples; unchanged references are excluded
equally. These are measured historical examples, not reduction targets.

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
- The conditional fixture's common-invalid-input/no-reference branch remains
  a coverage gap. The toy-list explanation's reference-read/tool-ban conflict
  remains unresolved.
- Model evaluations, installation checks, and security scans were not rerun for
  this documentation update. Historical scanner evidence was incomplete and
  is not security certification.

These checks do not guarantee equivalent behavior on every task. Test changes
on representative tasks before relying on them. Detailed development chronology
and machine-specific information are omitted from this public summary.
