---
type: comparison
tags: [moe, architecture, efficiency, synthesis]
---

# Comparison: MoE Architectures — From Switch Transformer to DeepSeek-V3

> A side-by-side analysis of **Mixture of Experts** architectures: how routing strategies, expert granularity, and load balancing have evolved from Google's Switch Transformer (2021) through Mixtral (2024) to DeepSeek-V3's fine-grained MoE (2024) — and the emerging adoption by Llama 4, Qwen3, and OLMoE.

## Overview

[[concepts/mixture-of-experts|Mixture of Experts (MoE)]] is the dominant approach for scaling language model capacity without proportionally scaling inference cost. The core idea: replace dense feed-forward layers with multiple "expert" sub-networks, routing each token to only a subset. This enables models with many total parameters but fixed active parameters per token. The design space has expanded dramatically — from simple top-1 routing to auxiliary-loss-free balancing with 256 fine-grained experts.

## Architecture Comparison

| Feature | Switch Transformer | Mixtral 8x7B | OLMoE-1B-7B | DeepSeek-V3 | Llama 4 | Qwen3-MoE |
|---|---|---|---|---|---|---|
| **Year** | 2021 | 2024 | 2024 | 2024 | 2025 | 2025 |
| **Org** | Google | Mistral AI | AllenAI | DeepSeek | Meta | Alibaba |
| **Total params** | Up to 1.6T | 47B | 6.9B | 671B | Unknown | 235B |
| **Active params** | Varies | 13B | 1.3B | 37B | Unknown | 22B |
| **Num experts** | 128 | 8 | 64 | 256 (+1 shared) | Unknown | 128 |
| **Top-k** | 1 | 2 | 8 | 8 | Unknown | 8 |
| **Load balancing** | Auxiliary loss | Auxiliary loss | Auxiliary loss + QK-Norm | **Aux-loss-free** (bias term) | Unknown | Auxiliary loss |
| **Expert granularity** | Standard | Standard | Fine-grained | **Fine-grained** | Unknown | Fine-grained |
| **Attention** | Standard MHA | GQA + SWA | GQA + QK-Norm | **MLA** | GQA | GQA |
| **Context** | Varies | 32K | 4K | 128K | Unknown | 32K+ |
| **Open** | ✅ | ✅ | ✅ (fully) | ✅ | ✅ | ✅ |

## Key Design Dimensions

### 1. Routing Strategy

| Strategy | Used By | Pros | Cons |
|---|---|---|---|
| **Top-1** | Switch Transformer | Simplest, cheapest | Less capacity per token |
| **Top-2** | Mixtral | Good quality/cost balance | 2× expert compute vs top-1 |
| **Top-8** | DeepSeek-V3, OLMoE, Qwen3 | Maximum capacity utilization | Higher routing overhead |

**Trend**: The field has moved toward higher top-k with more experts. DeepSeek-V3 uses top-8 of 256, giving each token access to 8/256 = 3.1% of experts — extreme sparsity with high capacity.

### 2. Expert Granularity

| Approach | Description | Used By |
|---|---|---|
| **Standard** | 8–16 large experts per layer | Switch Transformer, Mixtral |
| **Fine-grained** | 64–256 small experts per layer | DeepSeek-V3, OLMoE, Qwen3 |

Fine-grained experts (many small experts, higher top-k) allow more flexible token-to-expert assignment and better load distribution. DeepSeek-V2 introduced this approach; DeepSeek-V3 validated it at frontier scale.

### 3. Load Balancing

Preventing "expert collapse" (where router sends all tokens to a few experts) is a fundamental MoE challenge:

| Method | Description | Used By |
|---|---|---|
| **Auxiliary loss** | Add α · Σ(f_i · P_i) to training loss | Switch, Mixtral, OLMoE |
| **Capacity factor** | Hard limit on tokens per expert; overflow dropped | Switch Transformer |
| **QK-Norm** | Normalize query/key vectors for routing stability | OLMoE |
| **Auxiliary-loss-free** | Learnable bias adjusted by load statistics | DeepSeek-V3 |

DeepSeek-V3's auxiliary-loss-free approach is a significant innovation: it adds a bias term to routing scores, updated based on which experts are overloaded/underloaded. This avoids the tension between main training objective and load-balancing loss, leading to better expert specialization.

### 4. Shared Experts

| Model | Shared Experts | Purpose |
|---|---|---|
| DeepSeek-V3 | 1 per layer | Always activated, captures common knowledge |
| Others | 0 | All experts specialized |

Shared experts ensure that common patterns (frequent tokens, basic syntax) are always available, reducing redundancy across routed experts.

## Performance Comparison

### Quality per Active Parameter
| Model | Active Params | MMLU | vs. Dense Equivalent |
|---|---|---|---|
| Switch-Base (128E) | ~Comparable to T5-Base | — | 7× pretraining speedup |
| Mixtral 8x7B | 13B | 70.6 | Matches LLaMA 2 70B (5× active) |
| OLMoE-1B-7B | 1.3B | 52.2 | Matches OLMo-7B (5× active) |
| DeepSeek-V3 | 37B | 88.5 | Near GPT-4o level |

**Key insight**: Across all generations, MoE models consistently match dense models with **4–6× more active parameters** — roughly constant scaling efficiency.

### Inference Efficiency
| Model | Total Params | Active Params | Ratio | Memory Impact |
|---|---|---|---|---|
| Mixtral 8x7B | 47B | 13B | 3.6× | All experts loaded |
| OLMoE-1B-7B | 6.9B | 1.3B | 5.3× | Modest memory |
| DeepSeek-V3 | 671B | 37B | 18.1× | Extreme: 671B in VRAM |

**Trade-off**: MoE saves compute per token but not memory — all expert weights must be loaded. This creates deployment challenges, especially for DeepSeek-V3 (671B total). Expert offloading and expert parallelism partially address this.

## The MoE vs. Dense Debate

### Arguments for MoE
- **Better quality per FLOP**: Consistently demonstrated across all model families
- **Scalable**: Can grow total parameters without proportional inference cost
- **Modular**: Experts naturally specialize; can prune or add experts post-training
- **Proven at frontier**: DeepSeek-V3 ($5.5M training cost) demonstrates extreme cost efficiency

### Arguments for Dense
- **Simpler deployment**: No routing overhead, standard parallelism strategies
- **Lower total memory**: Only active parameters stored
- **Training stability**: No load-balancing concerns
- **Predictable**: No dropped tokens, no routing variability

### The Verdict (2025)
MoE has won at the frontier: DeepSeek-V3/R1, Llama 4, and Qwen3's largest models all use MoE. Dense models remain dominant at small scale (<7B) where MoE overhead isn't justified, and for deployment-constrained scenarios.

## Timeline
| Year | Milestone | Significance |
|---|---|---|
| 2017 | Shazeer et al. (original MoE) | MoE for LSTM language models |
| 2021 | [[sources/switch-transformer\|Switch Transformer]] | Simplified to top-1, scaled to 1T+ |
| 2024 | [[sources/mixtral\|Mixtral 8x7B]] | MoE goes mainstream in open source |
| 2024 | [[sources/olmoe\|OLMoE]] | First fully open MoE (data + code + logs) |
| 2024 | [[sources/deepseek-v3\|DeepSeek-V3]] | Fine-grained MoE + aux-loss-free + MLA |
| 2025 | [[sources/llama-4\|Llama 4]] | MoE adopted by Meta for Llama |
| 2025 | [[sources/qwen3\|Qwen3]] | 128-expert MoE with thinking mode |

## Key Papers
- [[sources/switch-transformer]] — Switch Transformer (foundational modern MoE)
- [[sources/mixtral]] — Mixtral 8x7B (MoE goes open-source mainstream)
- [[sources/olmoe]] — OLMoE (fully open MoE, 64 experts)
- [[sources/deepseek-v3]] — DeepSeek-V3 (frontier MoE with MLA)
- [[sources/llama-4]] — Llama 4 (Meta adopts MoE)
- [[sources/qwen3]] — Qwen3 (unified thinking MoE)
- [[sources/jamba]] — Jamba (hybrid Transformer-Mamba-MoE)


## Shared Expert Pool: UniPool

[[sources/unipool|UniPool (2026)]] challenges the fundamental assumption that each MoE layer needs isolated expert capacity:

### Key Insight: Deep-Layer Expert Redundancy
- Replacing deep layers' learned top-k routers with **uniform random routing** drops accuracy by only 1.0–1.6 points in production MoE models (Qwen, DeepSeek)
- This means deep-layer experts are largely redundant — they could be shared

### Architecture: Global Shared Pool
| Aspect | Vanilla MoE | UniPool |
|---|---|---|
| Expert ownership | Per-layer (L×E total) | Global pool (M total, M < L×E) |
| Parameter growth with depth | Linear | **Sublinear** |
| Routing | Per-layer router → layer's experts | Per-layer router → shared pool |
| Expert specialization | Low in deep layers | Higher (sharing forces specialization) |

### Results
- Consistent loss improvement across 5 scales (182M–978M): up to −0.0386 validation loss
- **41.6% of expert parameters** matches vanilla MoE performance — parameters need not grow linearly with depth
- NormRouter (cosine similarity + ReLU) provides scale-stable routing

### Implications for Large-Scale MoE
- GLM-4.5 (355B), DeepSeek-V3 (671B) could reduce expert parameter counts substantially
- Pool size becomes an explicit depth-scaling hyperparameter
- Expert decomposition (finer-grained experts) composes with sharing benefits

## See Also
- [[concepts/mixture-of-experts]] — MoE concept page
- [[concepts/transformer-architecture]] — Transformer fundamentals
- [[concepts/scaling-laws]] — Scaling laws and compute efficiency
- [[entities/models/deepseek]] — DeepSeek model family
- [[entities/models/mistral]] — Mistral / Mixtral family
- [[entities/models/olmo]] — OLMo / OLMoE family
- [[comparisons/open-model-families]] — Open model family comparison
