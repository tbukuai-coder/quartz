---
type: concept
tags: [architecture, ssm, mamba, alternative]
---

# State Space Models (SSMs)

> A family of sequence models based on continuous-time state spaces that process sequences in linear time — the primary alternative to Transformer attention, pioneered by [[sources/mamba|Mamba]].

## Overview
While Transformers process all tokens simultaneously via attention (O(n²)), State Space Models process tokens sequentially through a hidden state (O(n)), analogous to RNNs but with structured dynamics that enable parallelization during training. The breakthrough came with **Mamba** (2023), which added input-dependent selectivity to SSMs, enabling content-based reasoning that prior SSMs lacked.

## How It Works
A continuous-time SSM maps input u(t) to output y(t) through hidden state h(t):
```
h'(t) = A·h(t) + B·u(t)    (state evolution)
y(t) = C·h(t)                (output)
```

**Discretization** converts to discrete steps for sequence processing. The key matrices (A, B, C) define how information flows. **Selective SSMs (Mamba)** make B, C, and the step size Δ functions of the input — enabling content-dependent reasoning.

## Key Advantage: Linear Scaling
- **Attention**: O(n²) — quadratic in sequence length
- **SSM**: O(n) — linear in sequence length
- Mamba achieves **5× inference throughput** over Transformers
- Scales to **1M+ tokens** at linear cost

## Key Papers
- [[sources/mamba|Mamba]] — selective SSMs with hardware-aware implementation
- S4 (2021) — foundational structured SSM
- Mamba-2 (2024) — connection between SSMs and attention (SSD framework)

## Models Using SSMs
- **Mamba-{130M–2.8B}**: Original models from Gu & Dao
- **Jamba** (AI21): Hybrid SSM + Attention layers
- **Zamba** (Zyphra): SSM-based efficient model
- **FalconMamba** (TII): First large-scale pure Mamba model
- All available on HF Hub with `transformers` integration

## See Also
- [[concepts/transformer-architecture|Transformer Architecture]]
- [[concepts/self-attention|Self-Attention]]
- [[concepts/long-context|Long Context]]
