---
type: concept
tags: [architecture, training, efficiency, 2024]
---

# Multi-Token Prediction

> Training a model to **predict several future tokens at once** rather than just the next one — densifying the training signal and improving data efficiency, inference speed, and downstream quality.

## Overview
Standard autoregressive LLMs predict the single next token at each position. Multi-token prediction (MTP) extends this to predict the next D tokens simultaneously, providing D× more gradient signal per training position. This was shown to improve code generation, planning, and reasoning — and is a key innovation in [[sources/deepseek-v3|DeepSeek-V3]].

## How It Works

### Independent heads approach (Meta, 2024)
- Share the main Transformer backbone
- Each future position has its own output head
- At inference, only the first head is used — no latency cost

### Sequential modules approach ([[sources/deepseek-v3|DeepSeek-V3]])
- Each prediction module conditions on the previous module's output
- Auxiliary training loss added to the main loss
- MTP modules can be used for speculative decoding at inference

## Key Results
- **Meta**: 4-token prediction improves code generation by 12% at 7B scale; self-speculative decoding gives 3× speedup
- **DeepSeek-V3**: D=2 gives ~0.5% benchmark improvement with negligible compute overhead

## Why It Works
1. **Richer gradients**: D loss signals per position instead of 1
2. **Planning capability**: Forces the model to plan ahead
3. **Data efficiency**: More learning signal per training token
4. **Inference speedup**: Extra heads enable self-speculative decoding

## Comparison
| Technique | Training Change | Inference Change | Speedup |
|---|---|---|---|
| **Multi-token prediction** | Predict D future tokens | Optional (speculative) | Up to 3× |
| [[concepts/speculative-decoding|Speculative decoding]] | None | Draft model + verification | 2–3× |
| [[sources/medusa|Medusa]] | Train extra heads | Multiple parallel predictions | 2–3× |

## Key Papers
- Gloeckle et al., "Better & Faster LLMs via Multi-token Prediction" (2024)
- [[sources/deepseek-v3]] — Production MTP in a 671B MoE model

## See Also
- [[concepts/speculative-decoding]] — Inference-time multi-token generation
- [[concepts/pre-training]] — MTP is a pre-training technique
- [[concepts/scaling-laws]] — MTP changes the data efficiency curve