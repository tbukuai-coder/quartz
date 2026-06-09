---
type: entity
category: model
tags: [open-models, mistral-ai, efficiency, moe]
---

# Mistral / Mixtral

> Mistral AI's model family — known for exceptional **efficiency** (outperforming larger models) and introducing **Sparse MoE** to open-source LLMs.

## Overview
Mistral AI, founded by ex-Meta and ex-DeepMind researchers, rapidly became a key player with models that punch above their weight class. Mistral 7B outperforms Llama 2 13B; Mixtral 8x7B matches Llama 2 70B while being 6× faster.

## Models

| Model | Year | Params | Active | Key Features |
|---|---|---|---|---|
| Mistral 7B | 2023 | 7B | 7B | GQA + SWA, Apache 2.0 |
| Mixtral 8x7B | 2024 | 47B | 13B | Sparse MoE (8 experts, top-2 routing) |
| Mixtral 8x22B | 2024 | 176B | 44B | Larger MoE variant |
| Mistral Large | 2024 | 123B | 123B | Dense frontier model |
| Mistral Small | 2024 | 24B | 24B | Efficient mid-size model |

## Architectural Innovations
- **Sliding Window Attention (SWA)**: Fixed attention window per layer; information propagates across layers for theoretically unbounded context — [[concepts/swa]]
- **Grouped-Query Attention (GQA)**: Shared KV heads for faster inference — [[concepts/gqa]]
- **Sparse Mixture of Experts**: Token-level expert routing — [[concepts/mixture-of-experts]]
- **Rolling Buffer Cache**: Fixed KV cache size regardless of sequence length

## Related Papers
- [[sources/mistral-7b]] — Mistral 7B paper
- [[sources/mixtral]] — Mixtral 8x7B paper

## See Also
- [[entities/orgs/mistral-ai]]
- [[entities/models/zephyr]] (built on Mistral 7B)
