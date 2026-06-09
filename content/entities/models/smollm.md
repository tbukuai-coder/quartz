---
type: entity
category: model
tags: [open-models, huggingface, small-model, data-centric, multimodal]
---

# SmolLM (SmolLM2) & SmolVLM

> Hugging Face's family of small language models (135M–1.7B) and vision-language models (256M–2.2B) — demonstrating that **data-centric training** and strategic design can produce surprisingly capable models at tiny scale.

## Overview
SmolLM represents the "small but mighty" philosophy: rather than scaling parameters, scale data quality and training tokens. SmolLM2 1.7B is trained on ~11T tokens — a 6,500:1 token-to-parameter ratio — and outperforms other models in its class. SmolVLM extends this to multimodal, achieving competitive vision-language performance with <1GB VRAM.

## Language Models (SmolLM2)

| Model | Params | Training Tokens | Key Feature |
|---|---|---|---|
| SmolLM2-135M | 135M | ~11T | Ultra-small, edge deployment |
| SmolLM2-360M | 360M | ~11T | Mobile-friendly |
| SmolLM2-1.7B | 1.7B | ~11T | Best-in-class small model |

## Vision-Language Models (SmolVLM)

| Model | Params | VRAM | Key Feature |
|---|---|---|---|
| SmolVLM-256M | 256M | <1GB | Surpasses 80B Idefics |
| SmolVLM-500M | 500M | ~1.5GB | Balanced |
| SmolVLM-2.2B | 2.2B | ~3GB | Rivals 4B+ VLMs |

## Key Datasets Created
- **FineMath**: High-quality math data filtered from web
- **Stack-Edu**: Educational code content
- **SmolTalk**: Curated conversational data
- **FineWeb-Edu**: Educational web content
- **The Cauldron**: 50 VL datasets (from Idefics2, used by SmolVLM)

## Significance
SmolLM is important not just for the models but for the **transparency of the training process**. The paper provides detailed ablations on dataset mixing, making it a practical reference for anyone training small models. SmolVLM further shows that aggressive image tokenization (4× fewer tokens via pixel shuffle) enables competitive multimodal performance at tiny scale.

## Related Papers
- [[sources/smollm2]] — SmolLM2 paper
- [[sources/smolvlm]] — SmolVLM paper
- [[sources/idefics2]] — Idefics2 design principles (SmolVLM's predecessor lineage)
- [[sources/scaling-data-constrained]] — Data repetition insights used

## See Also
- [[entities/orgs/huggingface]]
- [[concepts/pre-training]]
- [[concepts/scaling-laws]]
- [[concepts/vision-language-models]]
