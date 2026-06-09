---
type: source
arxiv_id: "2408.00118"
title: "Gemma 2: Improving Open Language Models at a Practical Size"
authors: ["Gemma Team", "Morgane Riviere", "et al."]
date: 2024-07-31
org: "Google DeepMind"
tags: [open-models, distillation, architecture, 2024]
upvotes: 78
---

# Gemma 2: Improving Open Language Models at a Practical Size

> Improved Gemma models (2B, 9B, 27B) using **interleaved local-global attention**, **logit soft-capping**, and **knowledge distillation** — the 27B model rivals models twice its size.

## Key Contributions
- Introduced **interleaving local and global attention layers** — reducing KV cache memory while maintaining quality
- Applied **logit soft-capping** in attention to stabilize training
- Trained 2B and 9B models using **knowledge distillation** (from larger models) instead of next-token prediction
- 27B model competitive with models at 2× its size
- Released 2B, 9B, and 27B variants

## Method
### Architecture Changes
- **Interleaved local-global attention**: Alternating between full attention (global) and sliding window attention (local) layers — saves KV cache memory
- **Logit soft-capping**: `tanh(logits/cap) × cap` — prevents extreme attention logit values
- **GQA** for all model sizes
- **Post-norm + pre-norm** combined (RMSNorm both before and after each sublayer)

### Knowledge Distillation
- 2B and 9B models trained by distilling from a larger teacher model
- Uses soft-label training instead of standard next-token prediction
- Enables smaller models to outperform same-size models trained conventionally

## Models Released
| Model | Params | Context | Training |
|---|---|---|---|
| Gemma 2 2B | 2B | 8192 | Distilled |
| Gemma 2 9B | 9B | 8192 | Distilled |
| Gemma 2 27B | 27B | 8192 | Standard |

## Connections
- **Builds on**: [[sources/gemma]] (Gemma 1)
- **Continued by**: [[sources/gemma-3]] (adds multimodal)
- **Key concepts**: [[concepts/distillation]], [[concepts/swa]], [[concepts/gqa]], [[concepts/transformer-architecture]]
- **Models**: [[entities/models/gemma]]
- **Organizations**: [[entities/orgs/google]]

## Citation
> Gemma Team, "Gemma 2: Improving Open Language Models at a Practical Size," arXiv:2408.00118, 2024.
> https://huggingface.co/papers/2408.00118
