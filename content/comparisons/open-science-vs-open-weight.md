---
type: comparison
tags: [open-science, open-source, reproducibility, synthesis]
---

# Comparison: Open-Science vs Open-Weight LLMs

> A systematic analysis of what "open" really means in the LLM ecosystem — from fully open science (AllenAI, Apertus) to open-weight (Meta) to proprietary (OpenAI) — and why the distinction matters.

## The Openness Spectrum

| Level | Weights | Code | Data | Logs | Checkpoints | Eval | Example |
|---|---|---|---|---|---|---|---|
| **Fully Open** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | [[entities/orgs/allenai|OLMo]], [[sources/apertus|Apertus]] |
| **Open-Weight+** | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ | [[entities/orgs/deepseek|DeepSeek-V3]] |
| **Open-Weight** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | [[entities/models/llama|Llama]], [[entities/models/mistral|Mistral]] |
| **Gated Open** | ✅* | ❌ | ❌ | ❌ | ❌ | ❌ | Llama 2 |
| **API-only** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | GPT-4, Claude |

## What Each Artifact Enables

| Artifact | What It Enables | Who Benefits |
|---|---|---|
| **Model weights** | Inference, fine-tuning, deployment | Everyone |
| **Training code** | Reproduce training, modify architecture | ML engineers |
| **Training data** | Study data → model relationship | Data scientists |
| **Training logs** | Study training dynamics | Researchers |
| **Intermediate checkpoints** | Analyze learning trajectory | Researchers |
| **Evaluation framework** | Standardized comparison | Community |

## Detailed Comparison

### [[entities/orgs/allenai|AllenAI]] (OLMo) — Fully Open
- **Weights**: Apache 2.0, all sizes
- **Data**: [[entities/datasets/dolma|Dolma]] (3T tokens), documented curation
- **Code**: Training code on GitHub
- **Logs**: W&B training logs public
- **Checkpoints**: All intermediates released
- **Impact**: DCLM, training dynamics research, independent reproductions

### [[sources/apertus|Apertus (Swiss AI)]] — Fully Open
- **Weights**: Apache 2.0, 8B and 70B
- **Data**: 15T tokens, openly available, robots.txt compliant, 1800+ languages
- **Code**: Training code, data preparation scripts released
- **Checkpoints**: Released
- **Evaluation**: Evaluation suites released
- **Goldfish objective**: Novel memorization suppression technique
- **Impact**: Data compliance + multilingual open pretraining at scale

### [[entities/orgs/deepseek|DeepSeek]] — Open-Weight+
- **Weights**: MIT license (most permissive)
- **Code**: Training framework released
- **Data**: Not released
- **Impact**: GRPO adopted widely, MLA studied, distilled models widely used

### Meta (Llama) — Open-Weight
- **Weights**: Custom license (increasingly permissive)
- **Code**: Inference code only
- **Impact**: Catalyzed entire open-source LLM ecosystem

## License Comparison

| Model Family | License | Commercial Use |
|---|---|---|
| OLMo | Apache 2.0 | ✅ |
| Apertus | Apache 2.0 | ✅ |
| DeepSeek-R1 | MIT | ✅ |
| Qwen3 | Apache 2.0 | ✅ |
| Mistral 7B | Apache 2.0 | ✅ |
| Llama 3 | Llama 3 Community | ✅ (with conditions) |
| Gemma | Google Gemma License | ✅ (with conditions) |

## Ethical/Open Data Landscape

A growing movement emphasizes **data compliance** as a prerequisite for truly open models:

| Initiative | Tokens | Key Feature | License |
|---|---|---|---|
| [[entities/datasets/dolma|DOLMA]] | 3T | Fully documented curation | Open |
| [[sources/common-pile|Common Pile]] | 8TB | Openly licensed pretraining | Permissive |
| [[sources/common-corpus|Common Corpus]] | 1.99T | Public domain majority, provenance tracked | Open |
| Apertus data | 15T | Robots.txt compliant, 1800+ languages | Permissive |

## The Trend
The field is moving toward greater openness:
- 2023: LLaMA released weights only → revolutionary at the time
- 2024: OLMo set fully-open standard; DeepSeek released training code
- 2025: More organizations adopting Apache 2.0/MIT; OLMo won best paper at ACL 2024
- 2025: Apertus and Common Corpus raise the bar for **data compliance** — open models must also be ethically sourced

## See Also
- [[entities/orgs/allenai]] — Pioneer of fully open LLMs
- [[sources/apertus]] — Apertus: Data-compliant multilingual open models
- [[sources/common-corpus]] — Common Corpus: Largest ethical pretraining dataset
- [[entities/models/olmo]] — The most open LLM
- [[entities/datasets/dolma]] — The open training dataset
- [[comparisons/open-model-families]] — Model family comparison
