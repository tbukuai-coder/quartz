---
type: concept
tags: [training, foundational]
---

# Pre-training

> Training a model on a large corpus of unlabeled data to learn general-purpose representations — the foundation stage that gives LLMs their knowledge and capabilities before any task-specific training.

## Overview
Pre-training is the first and most compute-intensive stage of LLM development. A model processes trillions of tokens of text, learning language, world knowledge, reasoning patterns, and code. The resulting "base model" can then be adapted for specific tasks via [[concepts/fine-tuning]], [[concepts/instruction-tuning]], and [[concepts/rlhf|alignment]].

## How It Works

### Objectives
| Objective | Description | Used By |
|---|---|---|
| **Autoregressive LM** | Predict next token given previous tokens | GPT, [[entities/models/llama|LLaMA]], all decoder models |
| **Masked Language Modeling** | Predict masked tokens from bidirectional context | [[entities/models/bert-model|BERT]] |
| **Denoising** | Reconstruct corrupted input | T5, BART |

### Key Ingredients
1. **Tokenization**: Text must first be converted to token IDs — see [[concepts/tokenization]]. Tokenizer quality directly impacts data efficiency and multilingual coverage
2. **Data**: Trillions of tokens from web, books, code, papers — quality matters more than quantity ([[sources/refinedweb]], [[sources/scaling-data-constrained]])
3. **Scale**: Modern models train for weeks on thousands of GPUs
4. **Architecture**: [[concepts/transformer-architecture|Transformer]] with modern enhancements
5. **Optimization**: AdamW optimizer, learning rate warmup + cosine decay, gradient clipping

### Data Scale Evolution
| Model | Year | Training Tokens | Dataset |
|---|---|---|---|
| BERT | 2018 | ~3.3B | BooksCorpus + Wikipedia |
| GPT-3 | 2020 | 300B | Proprietary |
| LLaMA 1 | 2023 | 1–1.4T | Curated public data |
| Llama 2 | 2023 | 2T | Proprietary |
| [[entities/models/olmo\|OLMo]] | 2024 | 2.46T | [[entities/datasets/dolma\|Dolma]] (fully open) |
| SmolLM2 | 2025 | ~11T | FineWeb-Edu, FineMath, Stack-Edu |
| Qwen2.5 | 2024 | 18T | Proprietary |

## Key Papers
- [[sources/bert]] — Established pre-train + fine-tune paradigm
- [[sources/llama]] — Modern pre-training recipe on public data
- [[sources/olmo]] — First fully open pre-training pipeline (data + code + logs)
- [[sources/scaling-data-constrained]] — Data repetition scaling laws
- [[sources/refinedweb]] — Web-only pre-training data
- [[sources/fineweb]] — 15T token curated web data
- [[sources/smollm2]] — Multi-stage pre-training with data mixing

## See Also
- [[concepts/tokenization]] — Text → tokens (prerequisite step)
- [[concepts/fine-tuning]]
- [[concepts/scaling-laws]]
- [[concepts/instruction-tuning]]
- [[entities/datasets/dolma]] — Fully open pretraining dataset