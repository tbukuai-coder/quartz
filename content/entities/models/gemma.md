---
type: entity
category: model
tags: [open-models, google, safety]
---

# Gemma

> Google's family of lightweight open models built on Gemini research — emphasizing responsible development and strong performance at small scale (2B–27B).

## Overview
Gemma represents Google DeepMind's push into open-source LLMs. Unlike LLaMA (Meta) or Mistral, Gemma comes with a strong emphasis on safety evaluation and responsible AI practices. The models are distilled from Gemini research but designed for community use.

## Models

| Model | Year | Params | Key Features |
|---|---|---|---|
| Gemma 1 (2B, 7B) | 2024 | 2B, 7B | First release; MQA/MHA variants |
| Gemma 2 (2B, 9B, 27B) | 2024 | 2B–27B | Knowledge distillation, logit soft-capping |
| Gemma 3 | 2025 | 1B–27B | Multimodal (vision + text) |

## Architecture
- Transformer decoder-only
- RoPE embeddings, GeGLU activation, RMSNorm
- Multi-Query Attention (small models) / Multi-Head Attention (larger)
- Extensive safety filtering in training data and post-training

## Related Papers
- [[sources/gemma]] — Gemma 1 paper
- [[sources/gemma-2]] — Gemma 2 paper (distillation, interleaved attention)
- [[sources/gemma-3]] — Gemma 3 paper (multimodal, 128K context)

## Architecture Evolution
| Feature | Gemma 1 | Gemma 2 | Gemma 3 |
|---|---|---|---|
| Attention | MQA/MHA | GQA + interleaved local/global | GQA + high local/global ratio |
| Context | 8K | 8K | 128K |
| Distillation | No | Yes (2B, 9B) | Yes |
| Multimodal | No | No | Yes (vision) |
| Logit soft-capping | No | Yes | Yes |

## See Also
- [[entities/orgs/google]]
- [[concepts/pre-training]]
- [[concepts/distillation]]
