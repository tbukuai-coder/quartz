---
type: entity
category: model
tags: [multimodal, vlm, open-source, shanghai-ai-lab, vision-language]
---

# InternVL

> Shanghai AI Lab's family of **vision-language models** — the most downloaded open VLM family on HF Hub, featuring the continuously-trained InternViT-6B vision encoder and achieving the first open MLLM >70% on MMMU.

## Overview
InternVL represents the most systematic effort to close the gap between open and proprietary vision-language models. Built on the "ViT-MLP-LLM" architecture, InternVL's key innovation is a strong, continuously-trained vision encoder (InternViT-6B) that improves with each model generation.

## Model Family

### InternVL 1.5
| Model | Total Params | Vision Encoder | LLM | Key Feature |
|---|---|---|---|---|
| InternVL-Chat-V1-5 | 26B | InternViT-6B | InternLM2-20B | Dynamic high-res, bilingual |

### InternVL 2.5
| Model | Total Params | MMMU | Key Feature |
|---|---|---|---|
| InternVL2.5-1B | 1B | — | Edge deployment |
| InternVL2.5-8B | 8B | — | Efficient VLM |
| InternVL2.5-78B | 78B | **70.1%** | First open >70% MMMU |

## Key Innovations
1. **InternViT-6B continuous learning**: Continuously trained across generations — transfers to new LLM backbones
2. **Dynamic high-resolution**: 1–40 tiles of 448×448 based on aspect ratio
3. **Progressive scaling**: Smaller models bootstrap larger ones via synthetic data
4. **CoT for VLMs**: [[concepts/chain-of-thought|Chain-of-thought]] adds 3.7 points on MMMU

## Related Papers
- [[sources/internvl-1-5]] — InternVL 1.5
- [[sources/internvl-2-5]] — InternVL 2.5: First open >70% MMMU
- [[sources/internvl-3]] — InternVL3: Native multimodal pretraining, 72.2 MMMU (308 upvotes)

## See Also
- [[entities/orgs/shanghai-ai-lab]] — Shanghai AI Lab (creator)
- [[concepts/vision-language-models]] — VLM concept page
- [[concepts/contrastive-learning]] — InternViT training paradigm