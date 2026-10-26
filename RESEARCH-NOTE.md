# What the lookup learned, and what it did not

## The question and the baseline

Tokens are a model interface unit, not an editorial word definition. A token-count ratio cannot establish a particular word count for arbitrary text. The prototype asks whether accounting aligned with tokenizer output can be useful when text has a word budget.

A direct local word segmenter is the obvious baseline. It already supplies the count used as the prototype's reference; ordinary counters need not guess. A lookup therefore needs to justify any additional complexity through a defined integration or performance benefit. The inspected evidence does not establish that benefit.

## Count policy and implemented scope

The inspected helper creates `Intl.Segmenter('en', {granularity: 'word'})` and counts segments whose `isWordLike` property is true. All reported reference counts below are under that policy. An editorial service with different rules requires a separate comparison.

At a high level, the prototype builds a calibrated accounting artifact from locally tokenized text and consumes it to estimate counts and identify an estimated budget crossing. Some observed token contributions depend on context; handling unfamiliar surfaces is a known weak point. This is a design overview, not a release of the implementation, token inventory or internal rule set.

The inspected helper processes supplied text. The presence of a running count and an overflow helper does not prove integration into live generation, correct stopping under every input or a safe final sentence.

## Historical results

| Record | Conditions and result | What it does not establish |
| --- | --- | --- |
| June 15 artifact summary | Reports 38/38 exact on the calibrated cases for `gemini-2.0-flash-001` and `gemini-2.5-flash`. The prototype note separately reports 38/38 for the latter. | Held-out accuracy or a newly reproduced result. |
| June 15 generated artifacts | Inspected headers/metadata describe a 43-sample calibration and zero source-reconstruction mismatches for both configured labels. | Zero reconstruction mismatch is not proof of 43 exact estimator counts. This is a different artifact stage from the 38-case note. |
| July 17 technical review | Reports 44/48 exact for each label on the expanded corpus, using the retained generic lookup. | Two independent 48-case studies, tokenizer equivalence, general exactness or live model-generation performance. |
| Separate July 17 probe | Unicode-heavy input: estimated 14, reference 9, error +5. | A 49th corpus case or a general multilingual accuracy rate. |

The two configured labels are `gemini-2.0-flash-001` and `gemini-2.5-flash`. Their overlapping cases must not be added up as 96 independent observations. Exactness on calibration material is not held-out generalization.

### The four reported expanded-corpus errors

Error means estimated count minus reference count. This table reproduces numerical findings from the dated review, not a new run.

| Case description | Estimated | Reference | Error |
| --- | ---: | ---: | ---: |
| Plus-address email | 11 | 8 | +3 |
| Hidden file and extension | 8 | 6 | +2 |
| Model slug and word-budget text | 17 | 15 | +2 |
| Slash-form dates and times | 11 | 15 | -4 |

Both overcount and undercount matter. An overcount may reject usable text; an undercount may miss a real budget violation. Neither an earlier exact calibration nor a reassuring average would erase the latter risk.

The separate Unicode probe matters for a different reason: unfamiliar fragments need not correspond to new words under the reference policy. No raw corpus passages or new examples with invented measured counts are published here.

## Binding and freshness

The estimator accepts a model label but selects one generic lookup. The builder's metadata listing both labels does not prove the lookup is valid for both tokenizers. The inspected generic artifact identifies one model-specific build as its source. Equal aggregate scores are insufficient to settle equivalence.

The currently inspected corpus contains 48 items; generated metadata still describes 43. That discrepancy is directly visible without rerunning the prototype. It does not by itself prove that staleness caused every error, and rebuilding would not automatically establish generalization.

Exact historical tokenizer package, runtime and segmentation-library versions are not established by the reviewed metadata. Model labels alone do not provide a fully pinned reproduction environment.

## What remains a proposal

The July review recommends explicit artifact/version binding, stale-artifact checks, stronger treatment of unknown contexts, held-out comparisons and a separate policy for prose-safe stopping. Those recommendations are not reported here as implemented fixes.

A useful future comparison would evaluate tokenizer-aligned accounting against direct segmentation under the same count policy, including correctness at intermediate boundaries and actual resource cost. No speedup, streaming advantage or inference saving is established now. This documentary edition neither initiates that comparison nor authorizes a prototype repair.
