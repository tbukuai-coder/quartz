---
type: concept
tags: [architecture, foundational, activation-function, efficiency]
---

# Activation Functions (SwiGLU, GeGLU)

> The nonlinear functions applied in Transformer feed-forward layers — **SwiGLU** has become the universal choice in modern LLMs, replacing ReLU with a gated mechanism that improves quality at marginal extra cost.

## Overview
Every Transformer layer contains a feed-forward network (FFN) with a nonlinear activation function. The field converged on **gated linear units** (GLUs) — specifically SwiGLU — after Noam Shazeer's 2020 paper showed consistent improvements over ReLU/GELU.

## Evolution

| Activation | Year | Formula | Used By |
|---|---|---|---|
| **ReLU** | 2010 | `max(0, x)` | Original Transformer, early GPTs |
| **GELU** | 2016 | `x · Φ(x)` | [[entities/models/bert-model\|BERT]], GPT-2/3 |
| **SwiGLU** | 2020 | `Swish(xW₁) ⊙ (xV)` | [[entities/models/llama\|LLaMA]], [[entities/models/mistral\|Mistral]], [[entities/models/qwen\|Qwen]] |
| **GeGLU** | 2020 | `GELU(xW₁) ⊙ (xV)` | [[entities/models/gemma\|Gemma 2]] |

## How Gated Linear Units Work
Standard FFN: `FFN(x) = σ(xW₁)W₂` — two weight matrices.
Gated FFN: `FFN(x) = [σ(xW₁) ⊙ (xV)]W₂` — three weight matrices, gating mechanism.

The gate `σ(xW₁)` learns to selectively pass or block information from the value `xV`.

## The "LLaMA Architecture Template"
SwiGLU is one of four key choices defining modern decoder-only LLMs:
1. **[[concepts/positional-encodings|RoPE]]** — Rotary positional embeddings
2. **RMSNorm** — Simplified layer normalization
3. **SwiGLU** — Gated activation function
4. **[[concepts/gqa|GQA]]** — Grouped-query attention

Nearly every major open model since LLaMA (2023) follows this template.

## Key Papers
- Shazeer, "GLU Variants Improve Transformer" (2020)
- [[sources/llama]] — Popularized SwiGLU in open-source

## See Also
- [[concepts/transformer-architecture]] — SwiGLU is a core component
- [[concepts/positional-encodings]] — RoPE (another template choice)
- [[concepts/gqa]] — GQA (another template choice)