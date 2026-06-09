---
type: source
arxiv_id: "2409.02060"
title: "OLMoE: Open Mixture-of-Experts Language Models"
authors: ["Niklas Muennighoff", "Luca Soldaini", "Dirk Groeneveld", "Kyle Lo", "Jacob Morrison", "Sewon Min", "Weijia Shi", "Pete Walsh", "Oyvind Tafjord", "Nathan Lambert", "Yuling Gu", "Shane Arora", "Akshita Bhagia", "Dustin Schwenk", "David Wadden", "Alexander Wettig", "Binyuan Hui", "Tim Dettmers", "Douwe Kiela", "Ali Farhadi", "Noah A. Smith", "Pang Wei Koh", "Amanpreet Singh", "Hannaneh Hajishirzi"]
date: 2024-09-03
org: "AllenAI"
tags: [moe, open-science, pre-training, efficiency, 2024]
upvotes: 81
---

# OLMoE: Open Mixture-of-Experts Language Models

> A fully open sparse Mixture-of-Experts model — 1B active / 7B total parameters, trained on 5T tokens — that outperforms Llama2-13B-Chat and DeepSeekMoE-16B while being completely open (data, code, weights, logs).

## Key Contributions
- Released OLMoE-1B-7B: a fully open sparse MoE model with 7B total but only 1.3B active parameters per token
- Trained on 5 trillion tokens (OLMoE-Mix dataset), surpassing models with far more active parameters
- Provided comprehensive MoE design experiments: routing strategies, load balancing, expert count, granularity
- Deep analysis of MoE internals: router saturation, expert co-activation, domain specialization, vocabulary specialization
- Fully open: model weights, training data (OLMoE-Mix), training code, intermediate checkpoints, W&B training logs

## Method
**Architecture**:
- Decoder-only Transformer with sparse MoE layers
- 1.3B active parameters, 6.9B total parameters
- 16 layers, each with 64 experts, top-8 routing (k=8)
- SwiGLU activation, RoPE, RMSNorm, QK-Norm (for stability)
- Dropless MoE with load balancing loss (α=0.01)

**Key MoE Design Choices** (validated through ablations):
- **Fine-grained experts**: 64 small experts with k=8 outperform 8 large experts with k=2 (at same active params)
- **Router initialization**: Random initialization works well
- **Load balancing**: Critical for preventing expert collapse; α=0.01 balances quality and utilization
- **QK-Norm**: Required for stable training at scale (prevents loss spikes)
- **No positional information needed**: Jamba-style finding confirmed — explicit position embeddings optional in hybrid/MoE settings

**Training**:
- OLMoE-Mix: curated from DCLM, Dolma, StarCoder, peS2o, Wikipedia, Fandom
- 5T tokens, batch size 4M tokens, learning rate 3e-4 with cosine decay
- 128 H100 GPUs, ~3 weeks

**Adaptation**:
- SFT on Tülu 3 dataset (no Preference subset)
- DPO with UltraFeedback
- Creates OLMoE-1B-7B-Instruct

## Results
| Model | Active Params | MMLU | ARC-C | HellaSwag | WinoGrande |
|---|---|---|---|---|---|
| OLMoE-1B-7B | 1.3B | 52.2 | 52.1 | 79.6 | 71.7 |
| OLMo-7B | 7B | 52.0 | 48.5 | 78.2 | 72.1 |
| Llama2-13B | 13B | 55.7 | 49.4 | 80.5 | 72.2 |
| DeepSeekMoE-16B | 2.8B | 45.0 | 39.8 | 73.0 | 71.7 |
| Mixtral-8x7B | 12.9B | 70.6 | 55.4 | 84.4 | 77.2 |

OLMoE-1B-7B matches OLMo-7B (7× more active params) and outperforms DeepSeekMoE-16B with 2× fewer active params.

**MoE Analysis Findings**:
- **Router saturation**: Routing converges early (~20% of training), suggesting routers could be initialized better
- **Domain specialization**: Experts develop domain preferences (code, math, natural language) — more so than Mixtral
- **Vocabulary specialization**: Token-level routing patterns emerge, with specific experts handling specific token types

## Datasets Used
- OLMoE-Mix (5T tokens, fully open): DCLM, [[entities/datasets/dolma|Dolma]], StarCoder, peS2o, Wikipedia, Fandom
- Tülu 3 SFT data
- [[entities/datasets/ultrafeedback|UltraFeedback]] (DPO)

## Models Released
- OLMoE-1B-7B (base)
- OLMoE-1B-7B-SFT
- OLMoE-1B-7B-Instruct (SFT + DPO)
- All on HF Hub with intermediate checkpoints

## Connections
- Builds on: [[sources/olmo|OLMo]] (open-science framework), [[sources/switch-transformer|Switch Transformers]] (MoE foundations), [[sources/mixtral|Mixtral]] (sparse MoE for LLMs)
- Part of: AllenAI open-science ecosystem (OLMo, Dolma, Tülu, Paloma)
- Updated: OLMoE-1B-7B-0125 (Jan 2025) with DCLM data and improved performance
- Related concepts: [[concepts/mixture-of-experts|Mixture of Experts]], [[concepts/pre-training|Pre-training]]
- Related: [[sources/deepseek-v3|DeepSeek-V3]] (much larger MoE, proprietary training data)

## Citation
> Muennighoff et al., "OLMoE: Open Mixture-of-Experts Language Models," arXiv:2409.02060, 2024.
