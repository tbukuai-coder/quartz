---
type: source
arxiv_id: "2605.04569"
title: "Lightning Unified Video Editing via In-Context Sparse Attention"
authors: ["Shitong Shao", "Zikai Zhou", "Haopeng Li", "Yingwei Song", "Wenliang Zhong", "Lichen Bai", "Zeke Xie"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: null
upvotes: 12
tags: [video-editing, sparse-attention, efficiency, diffusion, in-context-learning]
github: null
---

# Lightning Unified Video Editing via In-Context Sparse Attention (LIVEditor)

> **In-context Sparse Attention (ISA)** — a near-lossless sparse framework for ICL video editing that achieves **~60% reduction in attention-module latency** while surpassing SOTA methods on EditVerseBench, IVE-Bench, and VIE-Bench, trained on a curated 1.7M high-quality video editing dataset.

## Key Contributions

1. **In-context Sparse Attention (ISA)**: First near-lossless empirical sparse framework tailored for in-context learning video editing — theoretically grounded in query sharpness / approximation error correlation
2. **Two key insights**: (a) Context tokens exhibit significantly lower saliency than source tokens; (b) Query sharpness correlates with approximation error (proved and validated)
3. **Dynamic query grouping**: Routes high-error queries to full attention and low-error queries to efficient 0-th order Taylor sparse attention
4. **LIVEditor model**: Lightning video editing model trained with ISA on 1.7M high-quality curated dataset — SOTA across 3 benchmarks
5. **~60% attention-module latency reduction**: Near-lossless acceleration without compromising visual fidelity

## Method

### In-Context Sparse Attention (ISA)
1. **Pre-selection**: Prune redundant context tokens based on saliency scores (context tokens have systematically lower attention weights than source tokens)
2. **Query sharpness estimation**: Compute per-query sharpness as proxy for approximation error (theoretically proven: Theorem 3.1)
3. **Dynamic grouping**: High-sharpness queries (low error) → 0-th order Taylor sparse attention; Low-sharpness queries (high error) → full attention
4. **Block-wise 0-th Taylor attention**: Efficient O(N·S/B) approximation using block-wise first-token expansion

### Theoretical Foundation
- **Theorem**: Approximation error ε_i is upper-bounded by terms involving query sharpness M_i — sharper queries have smaller approximation error under Taylor expansion
- **Empirical validation**: Correlation between predicted error and actual error is consistently high across layers and heads

### Data Pipeline
- 1.7M high-quality video-to-video editing pairs
- Sources: Self-constructed (Gemini 2.5 Flash captions → editing instructions → CogVideoX-1.5 generation) + publicly available datasets (Ditto, LoVoRA)
- 7 editing categories: style transfer, object addition/removal/replacement, background changes, motion modification, attribute editing
- Two-stage training: Stage I (1M synthetic + 0.7M filtered) → Stage II (high-quality subset fine-tuning)

## Results

### Benchmark Comparison
| Method | EditVerseBench (Quality) | IVE-Bench (Total) | VIE-Bench (Avg) |
|---|---|---|---|
| InsV2V | 21.88 | 5.75 | 6.42 |
| Ditto | 22.13 | 6.35 | 7.16 |
| LIVEditor (full-attn) | 23.41 | 6.52 | 8.28 |
| **LIVEditor (ISA)** | **23.63** | **6.58** | **8.84** |

- ISA matches or **exceeds** full attention quality while being ~60% faster
- Surpasses all SOTA methods including Ditto, InsV2V, LucyEdit, VACE

### Efficiency
- ~60% reduction in attention-module latency
- Near-lossless: quality maintained or slightly improved (ISA's pre-selection acts as soft regularization)

## Connections

- [[sources/sparkle-video-bg-replacement|Sparkle]] — Video background replacement; LIVEditor covers all editing types
- [[sources/swifti2v-highres|SwiftI2V]] — Efficient video generation; LIVEditor focuses on efficient editing
- [[concepts/video-generation|Video Generation]] — Extends efficient generation to efficient editing
- [[concepts/diffusion-models|Diffusion Models]] — Built on diffusion backbone with attention optimization
- [[sources/flash-attention-2|Flash Attention 2]] — Hardware-level attention optimization; ISA is algorithm-level for sparse ICL contexts
