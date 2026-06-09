---
type: entity
category: org
tags: [ai21-labs, architecture, ssm, hybrid, long-context, 2024]
---

# AI21 Labs

> An Israeli AI company that built the first production-scale **hybrid Transformer-Mamba-MoE architecture** (Jamba) — demonstrating that combining attention, state space models, and sparse experts yields superior efficiency and long-context performance.

## Overview
AI21 Labs was founded in 2017 in Tel Aviv and initially focused on language models for enterprise applications (Jurassic-1/2 series). Their most significant research contribution is [[sources/jamba|Jamba]], the first production model combining Transformer attention, [[sources/mamba|Mamba]] SSM layers, and [[concepts/mixture-of-experts|Mixture of Experts]] — proving that the three approaches are complementary rather than competing.

## Key Contributions

### Jamba Architecture
- [[sources/jamba|Jamba]] (2024) — 52B total parameters, 12B active:
  - **Hybrid design**: 1:7 ratio of attention to Mamba layers, MoE on alternating layers
  - **256K effective context**: 100% needle-in-a-haystack retrieval
  - **Memory efficiency**: 10× smaller KV cache than equivalent Transformer at 256K context
  - **Single GPU deployment**: Fits on a single 80GB GPU despite 52B total params
  - **2× throughput** vs. Mixtral 8×7B on long sequences

### Jamba 1.5
- Extended to 12B active / 98B total parameters
- Instruction-tuned variants for production deployment

### Key Architecture Insights
- SSMs and Attention are **complementary**: Mamba handles long-range dependencies; Attention handles recall-intensive tasks
- Positional embeddings are **optional** in hybrid models — Mamba provides implicit position information
- MoE integration with Mamba requires careful stabilization (RMSNorm in Mamba layers essential at 7B+ scale)

## Models
| Model | Total Params | Active Params | Context | Year |
|---|---|---|---|---|
| Jamba-v0.1 | 52B | 12B | 256K | 2024 |
| Jamba-1.5-Mini | 12B | — | 256K | 2024 |
| Jamba-1.5-Large | 98B | — | 256K | 2024 |

## Papers in This Wiki
- [[sources/jamba]] — Jamba: A Hybrid Transformer-Mamba Language Model

## See Also
- [[concepts/state-space-models]] — Mamba SSM component
- [[concepts/mixture-of-experts]] — MoE component
- [[concepts/long-context]] — 256K context capability
- [[concepts/transformer-architecture]] — Attention component