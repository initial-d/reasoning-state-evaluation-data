# Reasoning-state evaluation data

These data record controlled evaluations of numerical drafts. They test
whether model reviews preserve correct answers when intermediate operands
or proposed answers change.

- [Two-task data](data/two-task/) include 24 conditional-count questions and
  24 weighted-ledger questions, reference answers, draft variants, model
  outputs, and scored summaries.
- [Ledger budget data](data/ledger-budgets/) reuse the same ledger questions.
  Review prefixes at 192, 512 and 1,024 tokens share a generation trajectory.
- [Factorial data](data/factorial/) include the 48- and 72-question
  experiments, scored outputs, and an audit of naturally generated drafts.
- [Protocols](protocols/) contain prompts, decoding settings, scoring rules,
  model fingerprints, and paired comparison definitions.

A correct numeric answer and a valid numeric answer are separate fields.
The question is the pairing unit. Draft variants and budget prefixes are
repeated observations. Restart shares one result per question and cap.
File integrity hashes are listed in SHA256SUMS.
