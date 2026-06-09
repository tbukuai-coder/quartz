---
type: source
arxiv_id: "2503.19786"
title: "Gemma 3 Technical Report"
authors: ["Gemma Team", "Aishwarya Kamath", "et al."]
date: 2025-03-25
org: "Google DeepMind"
tags: [open-models, multimodal, vision, 2025]
upvotes: 55
---

# Gemma 3 Technical Report

> Google's first **multimodal open model** family (1B–27B) supporting vision + text with **128K context**, optimized KV-cache memory via increased local-to-global attention ratio.

## Key Contributions
- Added **vision understanding** capabilities — first multimodal Gemma
- Extended context to **128K tokens** (from 8K in Gemma 2)
- Reduced KV-cache memory by increasing the **local-to-global attention ratio** (most layers use local/SWA)
- Strong multilingual coverage
- Enhanced post-training recipe improving math, chat, and instruction-following
- Released 1B, 4B, 12B, and 27B variants

## Method
### Architecture
- Increased ratio of **local attention layers** (sliding window) to global attention layers
- This dramatically reduces KV-cache memory for long contexts
- Vision encoder processes images into tokens that interleave with text tokens
- Standard Transformer decoder core with GQA, RoPE, GeGLU

### Post-training
- Improved SFT + RLHF pipeline
- Enhanced math ability through targeted training
- Better instruction-following through curated datasets

## Models Released
| Model | Params | Context | Vision |
|---|---|---|---|
| Gemma 3 1B | 1B | 32K | ❌ |
| Gemma 3 4B | 4B | 128K | ✅ |
| Gemma 3 12B | 12B | 128K | ✅ |
| Gemma 3 27B | 27B | 128K | ✅ |

## Connections
- **Builds on**: [[sources/gemma-2]] (architecture), [[sources/gemma]] (first generation)
- **Key concepts**: [[concepts/swa]], [[concepts/gqa]], [[concepts/transformer-architecture]]
- **Related**: [[sources/llava]] (multimodal LLMs)
- **Models**: [[entities/models/gemma]]
- **Organizations**: [[entities/orgs/google]]

## Citation
> Gemma Team, "Gemma 3 Technical Report," arXiv:2503.19786, 2025.
> https://huggingface.co/papers/2503.19786
