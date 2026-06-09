---
type: source
arxiv_id: "2601.11659"
title: "The Llama 4 Herd: Architecture, Training, Evaluation, and Deployment Notes"
authors: ["Meta AI"]
date: 2025-01-20
org: "Meta AI"
tags: [open-models, moe, multimodal, 2025]
upvotes: 0
---

# The Llama 4 Herd

> Meta's **fourth-generation** models marking a major architecture shift to **Mixture of Experts (MoE)** with early-fusion multimodality and iRoPE for extreme length generalization.

## Key Contributions
- First Llama models using **MoE architecture** — routed + shared experts
- **Early-fusion multimodality** — natively processes images and text from pre-training (not bolted on)
- **iRoPE** (interleaved RoPE) — novel position encoding for length generalization beyond training context
- Released Scout (smaller) and Maverick variants; previewed Behemoth teacher model
- Multi-stage training: pre-training → mid-training → post-training (SFT + online RL + lightweight DPO)

## Method
### Architecture
- **MoE with routed/shared experts**: Some experts are always active (shared), others are selectively routed
- **Early-fusion multimodality**: Vision tokens processed alongside text from the start (not through adapters)
- **iRoPE**: Interleaved Rotary Position Embeddings for length generalization far beyond training context
- Scout: Long-context specialist; Maverick: General-purpose; Behemoth: Large teacher

### Training Pipeline
1. **Pre-training**: Standard autoregressive on massive corpus
2. **Mid-training**: Domain-specific data emphasis, context extension
3. **Post-training**: Lightweight SFT → online RL → lightweight DPO
4. **Quantization packaging**: Optimized for deployment

## Models Released
| Model | Type | Key Feature |
|---|---|---|
| Llama 4 Scout | MoE | Long context, efficient |
| Llama 4 Maverick | MoE | General purpose |
| Llama 4 Behemoth | MoE | Teacher model (previewed) |

## Connections
- **Builds on**: [[sources/llama-3]], [[sources/mixtral]] (MoE architecture inspiration)
- **Key concepts**: [[concepts/mixture-of-experts]], [[concepts/dpo]], [[concepts/rlhf]]
- **Models**: [[entities/models/llama]]
- **Organizations**: [[entities/orgs/meta]]

## Citation
> Meta AI, "The Llama 4 Herd," arXiv:2601.11659, 2025.
> https://huggingface.co/papers/2601.11659
