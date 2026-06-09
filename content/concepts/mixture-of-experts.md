---
type: concept
tags: [architecture, moe]
---

# Mixture of Experts (MoE)

> An architecture where each token is processed by a **subset of "expert" sub-networks** selected by a learned router — enabling models with many more total parameters while keeping inference cost fixed.

## Overview
MoE replaces the dense feed-forward network in each Transformer layer with multiple "expert" FFNs and a routing mechanism. Each token is sent to only the top-k experts (typically k=2), so the model has many parameters (knowledge capacity) but only uses a fraction per token (compute cost). This enables models like [[sources/mixtral|Mixtral 8x7B]] to have 47B total parameters but only 13B active — matching 70B dense models at 13B inference cost.

## How It Works

### Architecture
```
Input → Router(x) → select top-k experts → weighted sum of expert outputs
```

1. **Experts**: N identical FFN blocks (e.g., 8 experts per layer)
2. **Router**: Small linear layer that produces routing scores for each expert
3. **Top-k selection**: Only k experts (typically 2) are activated per token
4. **Weighted combination**: Expert outputs weighted by router softmax scores

### Key Design Choices
| Choice | Options |
|---|---|
| Number of experts | 8 (Mixtral), 64+ (DeepSeek-V3) |
| Top-k | 1 (Switch Transformer), 2 (Mixtral, standard) |
| Routing | Token-level (standard), expert-level |
| Load balancing | Auxiliary loss to prevent expert collapse |
| Expert granularity | Standard, fine-grained (DeepSeek) |

### Trade-offs
| Advantage | Disadvantage |
|---|---|
| More parameters per FLOP | Higher memory (all experts must be loaded) |
| Better quality per inference cost | Training instability (load balancing) |
| Scales well | Complex distributed training |
| Modular knowledge | Some experts may be underutilized |

## Key Models
- [[sources/switch-transformer]] — Switch Transformer (Google's top-1 routing MoE, foundational)
- [[sources/mixtral]] — Mixtral 8x7B (8 experts, top-2, 47B total / 13B active)
- [[sources/olmoe]] — OLMoE (64 fine-grained experts, fully open)
- [[sources/deepseek-v3]] — DeepSeek-V3 (256 experts, auxiliary-loss-free, MLA)

## Key Papers
- [[sources/switch-transformer]] — Switch Transformer (foundational modern MoE)
- [[sources/mixtral]] — Mixtral 8x7B
- [[sources/olmoe]] — OLMoE
- [[sources/deepseek-v3]] — DeepSeek-V3


## Shared Expert Pools: UniPool

[[sources/unipool|UniPool (2026)]] challenges the per-layer expert ownership assumption:
- In production MoEs, random routing in deep layers drops accuracy by only 1.0–1.6 points — experts are largely redundant
- **UniPool**: Single shared expert pool accessed by independent per-layer routers
- Pool-level auxiliary loss ensures balanced utilization across all layers
- NormRouter (cosine similarity + ReLU) provides scale-stable sparse routing
- **Sublinear parameter scaling**: 41.6% of expert parameters matches vanilla MoE
- Expert specialization increases under sharing — routing decisions become more load-bearing

## See Also
- [[comparisons/moe-architectures]] — Detailed MoE architecture comparison
- [[concepts/transformer-architecture]]
- [[entities/models/mistral]]
- [[entities/models/deepseek]]
- [[entities/models/olmo]]
