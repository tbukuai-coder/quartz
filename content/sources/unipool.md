---
type: source
arxiv_id: "2605.06665"
title: "UniPool: A Globally Shared Expert Pool for Mixture-of-Experts"
authors: ["Minbin Huang", "Han Shi", "Chuanyang Zheng", "Yimeng Wu", "Guoxuan Chen", "Xintong Yu", "Yichun Yin", "Hong Cheng"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: "Centaurus Alpha"
upvotes: 6
tags: [mixture-of-experts, architecture, efficiency, routing, scaling]
github: "https://github.com/Centaurus-Alpha/UniPool"
---

# UniPool: A Globally Shared Expert Pool for Mixture-of-Experts

> Replaces rigid per-layer expert ownership with a **single globally shared expert pool** accessed by independent per-layer routers — reducing expert-parameter growth from linear to **sublinear with depth** while consistently improving validation loss across 5 model scales (182M–978M).

## Key Contributions

1. **Shared expert pool architecture**: All layers access the same global expert set through independent per-layer routers — eliminates the assumption that every layer needs isolated expert capacity
2. **Motivating observation**: Replacing deep layers' learned routers with uniform random routing drops accuracy by only 1.0–1.6 points in production MoE models — demonstrating substantial expert redundancy
3. **Pool-level auxiliary loss**: Balances expert utilization across the entire pool (not per-layer) — prevents collapse under sharing
4. **NormRouter**: Sparse and scale-stable routing via normalized cosine similarity + ReLU gating — avoids the softmax saturation problem at scale
5. **Sublinear parameter scaling**: Reduced-pool variants using 41.6–66.7% of vanilla expert-parameter budget match or outperform layer-wise MoE

## Method

### Architecture
Standard MoE: Each of L layers owns E separate experts → total E×L expert parameters
UniPool: Single pool of M experts shared across all L layers → M experts total (M < E×L)

```
Standard: Layer 1: [E1_1, E1_2, ..., E1_E]  (private)
          Layer 2: [E2_1, E2_2, ..., E2_E]  (private)
          ...
UniPool:  Shared Pool: [E_1, E_2, ..., E_M]  (global)
          Layer 1: Router_1 → selects from pool
          Layer 2: Router_2 → selects from pool
          ...
```

### Pool-Level Auxiliary Loss
Standard per-layer loss fails under sharing — optimizing balance within each layer doesn't guarantee balance across the pool. Pool-level loss aggregates load fractions and routing probabilities across ALL layers:

```
L_pool = α · M · Σᵢ f̄ᵢ · P̄ᵢ
```

Where f̄ᵢ and P̄ᵢ are pool-averaged load fraction and routing probability for expert i.

### NormRouter
Standard softmax routers saturate at scale. NormRouter computes:
```
s_i = σ(c · ReLU(h/‖h‖₂ · wᵢ/‖wᵢ‖₂))
```
- Cosine similarity: scale-invariant, avoids logit drift
- ReLU gating: natural sparsity without auxiliary sparsity losses
- Calibration factor c: Monte Carlo initialized for unit-magnitude initial scores

## Results

### Main Results (Validation Loss / PPL)
| Scale | Vanilla MoE | UniPool | Δ Loss |
|---|---|---|---|
| 182M | 1.9317 / 6.90 | **1.9029 / 6.71** | −0.0288 |
| 469M | 1.7982 / 6.04 | **1.7636 / 5.83** | −0.0346 |
| 650M | 1.7568 / 5.79 | **1.7182 / 5.57** | −0.0386 |
| 830M | 1.7192 / 5.58 | **1.6857 / 5.39** | −0.0335 |
| 978M | 1.6791 / 5.36 | **1.6559 / 5.24** | −0.0232 |

Consistent improvement across all 5 scales, with improvements composing with finer-grained expert decomposition.

### Sublinear Scaling: Reduced Pool Size
| Pool Size (% of vanilla) | Loss | vs Vanilla MoE |
|---|---|---|
| 100% (full) | 1.9029 | Better |
| 66.7% | 1.9087 | Better |
| 50% | 1.9240 | Better |
| **41.6%** | **1.9290** | **≈ Equal (within 0.003)** |

Key finding: UniPool with only 41.6% of expert parameters matches vanilla MoE — expert parameters need not grow linearly with depth.

### Routing Sensitivity
- Vanilla MoE: Random routing in deep layers drops only 1.3–1.5 points → experts redundant
- **UniPool: Random routing drops 4.1 points** → sharing makes each expert more functionally specialized; routing decisions become more load-bearing

## Connections

- [[concepts/mixture-of-experts|Mixture of Experts]] — Fundamental rethinking of expert allocation in MoE
- [[comparisons/moe-architectures|MoE Architectures]] — Adds UniPool as novel parameter-efficient MoE design
- [[sources/switch-transformer|Switch Transformer]] — Per-layer expert ownership that UniPool challenges
- [[sources/deepseek-v3|DeepSeek-V3]] — Production MoE where UniPool's routing probe was validated
- [[sources/nemotron-3-super|Nemotron 3 Super]] — LatentMoE; UniPool is complementary shared-pool approach
- [[sources/glm-4-5|GLM-4.5]] — 355B MoE; UniPool could reduce its expert parameter count
