---
type: entity
category: model
tags: [open-models, tii, pre-training, web-data, uae]
---

# Falcon

> TII's family of open language models — the first to demonstrate that **web-only pretraining data** ([[entities/datasets/refinedweb|RefinedWeb]]) can produce frontier-competitive models. Falcon-180B was briefly the **largest open model** and one of the top three language models in the world at release.

## Overview
The Falcon series, developed by the Technology Innovation Institute (TII) in Abu Dhabi, proved a powerful thesis: well-filtered web data alone can match or exceed curated multi-source corpora for LLM pretraining. Falcon-40B briefly topped the Hugging Face Open LLM Leaderboard in mid-2023, and Falcon-180B — trained on 3.5T tokens across up to 4,096 A100 GPUs on AWS — neared the performance of PaLM-2-Large at a fraction of the cost. TII has continued the Falcon line with multimodal (Falcon-2), state-space (Falcon Mamba), and hybrid architectures (Falcon-H1).

## Model Family

| Model | Year | Params | Training Tokens | Key Features |
|---|---|---|---|---|
| Falcon-7B | 2023 | 7B | 1.5T | Multi-query attention, competitive with LLaMA-7B |
| Falcon-40B | 2023 | 40B | 1T | Briefly #1 on HF Open LLM Leaderboard |
| Falcon-180B | 2023 | 180B | 3.5T | Largest open model at release; near PaLM-2-Large |
| Falcon-2 11B | 2024 | 11B | 5.5T | Multimodal (vision-to-text) capabilities |
| Falcon Mamba 7B | 2024 | 7B | 5.8T | Pure Mamba (SSM) architecture; attention-free |
| Falcon-H1 | 2025 | 0.5B–34B | Various | Hybrid Transformer-SSM; SOTA efficiency |

## Architecture
The original Falcon models follow a **decoder-only Transformer** design with key efficiency choices validated through extensive ablations:
- **Multi-query attention** (Falcon-7B) / **Multi-group attention** (Falcon-40B/180B) — GQA variant optimized for tensor-parallel inference (8 KV heads for Falcon-40B/180B)
- **RoPE** positional embeddings (replacing ALiBi from internal experiments)
- **LayerNorm** (not RMSNorm — one of the few deviations from the "LLaMA template")
- **Parallel attention and MLP** computation (GPT-J style) for throughput
- **No biases** in linear layers
- Custom distributed training via **Gigatron** on cloud AWS infrastructure (up to 4,096 A100s)

## Training Data
- **~85% [[entities/datasets/refinedweb|RefinedWeb]]** (web-only, English + European multilingual)
- **~13% curated sources**: Books (Project Gutenberg), conversations (Reddit, StackOverflow, HackerNews), technical (arXiv, Wikipedia), code (GitHub)
- **No data upsampling** — all sources used at natural frequency
- Key insight: extreme-scale filtering + deduplication of web data can replace hand-curated corpora

## Benchmarks

### Falcon-180B vs. Peers (at release, 2023)
| Model | MMLU (5-shot) | HellaSwag (0-shot) | ARC-C (25-shot) |
|---|---|---|---|
| Falcon-180B | 70.4 | 88.0 | 69.4 |
| LLaMA 2 70B | 68.9 | 85.3 | 64.6 |
| PaLM-2 Large | 78.3 | — | — |

Falcon-180B significantly outperforms LLaMA 2 70B and approaches PaLM-2-Large on NLP tasks.

## Evolution
1. **Falcon (2023)**: Web-data thesis validated at scale; open weights under permissive license
2. **Falcon-2 (2024)**: Added multimodal capabilities; 11B model with 5.5T tokens and VLM variant
3. **Falcon Mamba (2024)**: Pure state-space model; first competitive attention-free 7B model
4. **Falcon-H1 (2025)**: Hybrid Transformer + SSM architecture; redefining efficiency-performance tradeoffs across 0.5B–34B sizes

## Related Papers
- [[sources/falcon]] — The Falcon Series of Open Language Models (main paper)
- [[sources/refinedweb]] — RefinedWeb dataset (Falcon's data foundation)

## See Also
- [[entities/orgs/tii]] — Technology Innovation Institute (creator)
- [[entities/datasets/refinedweb]] — RefinedWeb dataset
- [[entities/models/llama]] — LLaMA (primary competitor in 2023)
- [[concepts/pre-training]] — Pre-training methodology
- [[concepts/state-space-models]] — SSMs (Falcon Mamba, Falcon-H1)
- [[comparisons/open-model-families]] — Model family comparison
