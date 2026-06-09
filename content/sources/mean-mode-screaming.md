---
type: source
arxiv_id: "2605.06169"
title: "Mean Mode Screaming: Mean-Variance Split Residuals for 1000-Layer Diffusion Transformers"
authors: ["Pengqi Lu"]
date: 2026-05-11
org: "Independent"
tags: [diffusion, architecture, training-stability, deep-networks, 2026]
upvotes: 231
---

# Mean Mode Screaming: Mean-Variance Split Residuals for 1000-Layer Diffusion Transformers

> Identifies Mean Mode Screaming (MMS) as the trigger for silent mean-dominated collapse in deep DiTs, and proposes mean-variance split residuals enabling stable training of 1000-layer Diffusion Transformers.

## Key Contributions
- **Mean Mode Screaming (MMS)**: identifies the mechanistic trigger for deep DiT collapse — a mean-coherent backward shock on residual writers that opens deep branches and drives mean-dominated homogenization
- **Mean-variance split residuals**: decouples residual updates into mean and variance components, preventing collapse while preserving expressivity
- **1000-layer DiTs**: enables training DiTs at extreme depths previously impossible due to silent collapse
- **Mechanistic auditing**: rigorous gradient decomposition analysis revealing how softmax Jacobian structure enables MMS propagation
- Fundamental architecture insight for the diffusion-architectures comparison

## Method
Through mechanistic auditing of deep DiTs, the paper isolates a structural vulnerability: Mean Mode Screaming occurs when residual updates become mean-coherent across tokens, triggering a cascade that homogenizes representations and suppresses centered variation. The fix is elegantly simple: split each residual branch into separate mean and variance pathways, applying different scaling to each. This preserves the information-carrying variance while preventing the mean mode from dominating.

## Results
- Stable training of 1000-layer DiTs (previously collapsed at ~100+ layers)
- Maintained generation quality at extreme depths
- Silent collapse detected and prevented even when loss curves appear normal

## Connections
- Builds on: [[sources/dit]], [[sources/sd3]], [[concepts/diffusion-models]], [[concepts/transformer-architecture]]
- Related: [[sources/cola-dlm]], [[comparisons/diffusion-architectures]], [[concepts/activation-functions]]
- Fundamental to: scaling diffusion architectures beyond current limits

## Citation
> Lu, "Mean Mode Screaming: Mean-Variance Split Residuals for 1000-Layer Diffusion Transformers," arXiv:2605.06169, 2026.
