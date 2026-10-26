# Tokenizer-Native Word-Count Index

## A token is not a word

What does a calibrated lookup get right, and where does it break?

This Sheila Studios research prototype explores local word-budget accounting for text tokenized under two Gemini model labels. Instead of asking a language model to estimate its own word count, it compares tokenizer-aligned estimates with a declared local word-segmentation policy.

The interesting result is not universal exactness. A July 17, 2026 technical review reports **44 of 48 exact counts for each configured model label**, with four recurring errors and a separate Unicode-heavy failure. The expanded corpus exposed limits that the earlier calibration result did not.

This repository is a **retrospective documentary edition**, not a software release, a hosted counter or a new evaluation. The implementation, calibration text and generated lookup tables are not distributed here.

### What you can inspect

- [Research note](RESEARCH-NOTE.md): count policy, historical results, failures and the direct-segmentation comparison that remains necessary.
- [Evidence ledger](EVIDENCE.md): inspected source, dated reported results and unresolved version/binding questions.
- [Rights and exclusions](RIGHTS.md): provenance and what this edition does not publish.

The reference count is English-locale JavaScript `Intl.Segmenter`, counting segments marked `isWordLike`. That is a specific policy, not a universal editorial definition or demonstrated agreement with every publishing platform.

### Maturity

Source inspection supports a local builder and estimator prototype, including an estimated overflow-position helper. Historical results show both calibrated success and generalization failures. Current live-generation integration, reliable hard-cap enforcement, faster counting and reduced inference cost are not established by this edition. An estimated token boundary is not necessarily a safe place to end prose.

This is a distinct tooling project within the studio's writing-tool research, not a release of an associated manuscript or SCCN tokenizer research. James and Sheila guide the work; Arden prepared this edition for Sheila's review. See the [studio portfolio](https://github.com/sheilastudios).
