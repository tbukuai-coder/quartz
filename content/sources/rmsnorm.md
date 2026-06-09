---
type: source
arxiv_id: "1910.07467"
title: "Root Mean Square Layer Normalization"
authors: ["Biao Zhang", "Rico Sennrich"]
date: 2019-10-16
org: "University of Edinburgh"
tags: [architecture, normalization, foundational]
upvotes: 2
---

# RMSNorm (Root Mean Square Layer Normalization)

> Proposed **RMSNorm** — a simplified normalization that removes the mean-centering of LayerNorm, keeping only the root mean square rescaling. RMSNorm became the **standard normalization** in virtually all modern LLMs (LLaMA, Mistral, Qwen, DeepSeek, Gemma, OLMo 2), offering equivalent quality with reduced computational cost.

## Key Contributions
- **Simpler normalization**: Only rescales by RMS of activations — removes the mean subtraction step of LayerNorm
- **Equivalent performance**: Matches LayerNorm quality on machine translation and language modeling
- **7–64% faster**: Reduced compute compared to LayerNorm depending on implementation
- **Re-scaling invariance**: Theoretically justified — the re-scaling operation is the key to LayerNorm's success, not re-centering

## Method
### LayerNorm
```
LayerNorm(x) = γ · (x - μ) / √(σ² + ε) + β
```
Where μ = mean(x), σ² = var(x)

### RMSNorm
```
RMSNorm(x) = γ · x / √(mean(x²) + ε)
```
Removes mean subtraction (μ) and variance (σ²), replacing with simpler RMS computation.

### Partial RMSNorm (pRMSNorm)
Uses only first p% of elements to compute the RMS statistic — further computational savings.

## Why It Matters
The paper's theoretical insight — that **re-scaling invariance**, not re-centering invariance, is the key property — proved correct empirically:
- All major LLM families adopted RMSNorm over LayerNorm
- The "LLaMA template" (2023+) standardized: RMSNorm + SwiGLU + RoPE + GQA

## Adoption
- **[[sources/llama|LLaMA]]** (2023): Adopted RMSNorm, establishing the modern standard
- **[[sources/mistral-7b|Mistral]]**, **[[sources/qwen25|Qwen]]**, **[[sources/gemma|Gemma]]**: All use RMSNorm
- **[[sources/deepseek-v3|DeepSeek-V3]]**: RMSNorm throughout
- **[[sources/olmo-2|OLMo 2]]**: Switched from non-parametric LayerNorm to RMSNorm
- **Notable exception**: [[sources/falcon|Falcon]] uses LayerNorm; [[sources/bloom|BLOOM]] uses LayerNorm + embedding LayerNorm

## Connections
- Adopted by: [[sources/llama]], [[sources/mistral-7b]], [[sources/qwen25]], [[sources/deepseek-v3]], [[sources/olmo-2]]
- Related: [[concepts/transformer-architecture]], [[concepts/activation-functions]]

## Citation
> Zhang & Sennrich, "Root Mean Square Layer Normalization," NeurIPS 2019, arXiv:1910.07467.
