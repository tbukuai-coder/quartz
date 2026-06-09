---
type: entity
category: dataset
tags: [pre-training, code, open-source, bigcode]
---

# The Stack

> A massive **open-source code dataset** from the BigCode project (HF × ServiceNow) — permissively licensed GitHub code providing the code component for many open LLMs.

## Versions
| Version | Size | Languages |
|---|---|---|
| v1 | ~3.1 TB, 6.4B files | 358 |
| v2 | ~67 TB | 619 |

## Pipeline
License filtering (Apache/MIT/BSD) → deduplication → PII removal → opt-out mechanism.

## Usage
- [[sources/olmoe|OLMoE]]: StarCoder data (from The Stack) in OLMoE-Mix
- [[entities/models/smollm|SmolLM2]]: Stack-Edu (educational subset)
- **StarCoder/StarCoder2**: Primary training data
- [[entities/datasets/dolma|Dolma]]: Code component

## Significance
Addressed critical gap: code training data with **clear licensing** and opt-out mechanism.

## See Also
- [[entities/models/starcoder]] — StarCoder models (primary consumer)
- [[entities/orgs/huggingface]] — Co-created BigCode
- [[concepts/pre-training]] — Code data for pre-training
- [[comparisons/pretraining-data]] — Data strategies