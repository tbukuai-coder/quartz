---
type: source
arxiv_id: "2401.04081"
title: "MoE-Mamba: Efficient Selective State Space Models with Mixture of Experts"
authors: ["Maciej Pióro", "Kamil Ciebiera", "Krystian Król", "et al."]
date: 2024-01-08
org: "IDEAS NCBR / University of Warsaw"
tags: [architecture, moe, ssm, hybrid, 2024]
upvotes: 74
---

# MoE-Mamba: Combining MoE with State Space Models

> Showed that **Mixture of Experts** can be combined with **Mamba** (SSMs) — achieving the scaling efficiency of MoE while retaining Mamba's constant-memory inference. MoE-Mamba reaches Transformer quality **2.2× faster** in training steps, combining the best of three architecture paradigms.

## Key Contributions
- **MoE + Mamba hybrid**: Replace Mamba's feed-forward layers with MoE layers — each token routed to top-k experts
- **2.2× faster convergence**: Matches Transformer quality in 2.2× fewer training steps
- **Outperforms both**: Better than Mamba alone (quality) and Transformer-MoE alone (efficiency)
- **Interleaving pattern**: Alternating Mamba and MoE-Mamba layers provides best results
- **74 upvotes**: High community interest in the MoE+SSM combination

## Method
```
Token → Mamba layer (selective SSM)
      → MoE-Mamba layer (SSM + expert routing)
      → Mamba layer
      → MoE-Mamba layer → ...
```

Key design: Every other Mamba layer replaced with MoE-Mamba (feedforward becomes MoE).

## Results
| Model | Training Steps to Match Quality | Inference Speed |
|---|---|---|
| Transformer | 1× (baseline) | Slowest |
| Mamba | ~1× | Fast (constant memory) |
| MoE-Transformer | ~0.5× | Medium |
| **MoE-Mamba** | **~0.45×** | **Fast** |

MoE-Mamba combines MoE's training efficiency with Mamba's inference efficiency.

## Impact
- Validated the MoE+SSM combination that was later adopted by:
  - [[sources/jamba|Jamba]] (AI21 Labs): Transformer + Mamba + MoE at 52B scale
  - [[sources/nemotron-h|Nemotron-H]] (NVIDIA): Mamba-2 + attention + MoE potential
- Established that the three architecture paradigms (attention, SSM, MoE) are complementary, not competing

## Connections
- Combines: [[sources/mamba|Mamba]] + [[concepts/mixture-of-experts|MoE]]
- Related: [[sources/jamba|Jamba]], [[sources/nemotron-h|Nemotron-H]]
- Concepts: [[concepts/state-space-models]], [[concepts/mixture-of-experts]]
- Comparisons: [[comparisons/moe-architectures]]

## Citation
> Pióro et al., "MoE-Mamba: Efficient Selective State Space Models with Mixture of Experts," arXiv:2401.04081, 2024.
