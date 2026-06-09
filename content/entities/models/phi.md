---
type: entity
category: model
tags: [open-models, microsoft, synthetic-data, reasoning]
---

# Phi (Phi-1 → Phi-3 → Phi-4)

> Microsoft Research's model series that pioneered the **"data quality over quantity"** paradigm — proving that small models trained on carefully curated synthetic data can match or exceed models 10× their size. Phi-4 (14B) surpasses its GPT-4 teacher on STEM reasoning.

## Overview
The Phi series is the most compelling demonstration that synthetic data quality can substitute for parameter scale. Starting with the insight that "textbooks are all you need" (Phi-1, 2023), the series has systematically shown that a 14B model can compete with 70B+ models when trained on strategically designed data.

## Models

| Model | Year | Params | Key Innovation | Benchmark Highlight |
|---|---|---|---|---|
| Phi-1 | 2023 | 1.3B | "Textbook quality" synthetic data | 50.6% HumanEval (beat 10× larger models) |
| Phi-1.5 | 2023 | 1.3B | Extended synthetic data to NL reasoning | — |
| Phi-2 | 2023 | 2.7B | Scaled data quality approach | Matched Llama-2-70B on some tasks |
| Phi-3-mini | 2024 | 3.8B | Heavily filtered web + synthetic | 69% MMLU (matched Mixtral 8x7B) |
| Phi-3-small | 2024 | 7B | Extended architecture | — |
| Phi-3-medium | 2024 | 14B | Baseline for Phi-4 | — |
| **Phi-4** | **2024** | **14B** | **50 synthetic dataset types, Pivotal Token Search** | **80.4% MATH, beat GPT-4o on GPQA** |

## Key Themes
1. **Synthetic data throughout**: Unlike models that use synthetic data only for fine-tuning, Phi uses it extensively during pretraining
2. **Data diversity**: 50+ synthetic dataset types with different seeds, prompting strategies, and domains
3. **Surpassing the teacher**: Phi-4 outperforms GPT-4 on STEM despite being distilled from it — evidence that curation > imitation
4. **Edge deployment**: Phi-3-mini was designed to run on phones; the series prioritizes capability per parameter

## Architecture
- Decoder-only Transformer (close to standard LLaMA template)
- RoPE, SwiGLU, GQA (from Phi-3 onward)
- tiktoken tokenizer (100K vocab)
- 4K → 16K context (with midtraining extension)

## Related Papers
- [[sources/phi-4]] — Phi-4 Technical Report
- Related: Phi-1 "Textbooks Are All You Need" (2306.11644), Phi-3 (2404.14219)

## See Also
- [[entities/orgs/microsoft]]
- [[concepts/synthetic-data]]
- [[concepts/distillation]]
