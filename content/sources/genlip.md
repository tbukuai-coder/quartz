---
type: source
arxiv_id: "2605.00809"
title: "Let ViT Speak: Generative Language-Image Pre-training"
authors: ["Unknown"]
date: 2026-05-03
org: "Unknown"
tags: [vision-transformers, multimodal-pretraining, generative-modeling, vision-language-models, 2026]
upvotes: 2
---

# GenLIP: Generative Language-Image Pre-training for Vision Transformers

> A minimalist generative pretraining framework that trains Vision Transformers to directly predict language tokens from visual tokens using only a standard autoregressive language modeling objective — no contrastive losses, no additional text modules.

## Key Contributions

- **Minimalist design**: Single ViT backbone + standard autoregressive objective; removes contrastive losses, dual-encoder architectures, and additional text decoders/modules
- **Direct alignment with MLLMs**: Vision encoder optimized directly for next-token prediction — the same objective downstream MLLMs use — eliminating objective mismatch
- **Strong scalability**: Consistent gains with both data and model size
- **Competitive performance**: Matches or outperforms strong baselines (CLIP, SigLIP, CapPa, AIMv2) pretrained on much larger corpora, using only **8B pretraining samples**
- **Superior OCR**: Particularly strong on optical character recognition tasks

## Method

Problem with prior VLP approaches:
- **Contrastive methods** (CLIP, SigLIP): Discriminative alignment mismatches with generative MLLM objective
- **Generative methods** (CapPa, AIMv2): Couple vision encoder with text decoder, optimizing vision encoder indirectly
- **Hybrid methods** (CoCa, SigLIP2): Redundant architecture, indirect optimization, complicated training

GenLIP's solution: Let the Vision Transformer "speak" directly — predict language tokens that describe visual content using standard autoregressive LM objective.

Second-stage native-aspect-ratio adaptation further improves downstream performance.

## Results

- Matches/outperforms baselines pretrained on much larger corpora with only 8B samples
- Particularly strong OCR performance
- Scales effectively with data and model size

## Connections
- Builds on: [[sources/clip]], [[sources/siglip]], [[sources/cappa]], [[sources/aimv2]]
- Related concepts: [[concepts/vision-language-models]], [[concepts/multimodal-models]]
- Related papers: [[sources/llava]], [[sources/internvl-3]], [[sources/qwen2-vl]]
- Cited by / Influenced: Vision encoder pretraining for MLLMs, generative VLP

## Citation
> "Let ViT Speak: Generative Language-Image Pre-training," arXiv:2605.00809, 2026.
