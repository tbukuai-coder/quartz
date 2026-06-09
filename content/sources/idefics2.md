---
type: source
arxiv_id: "2405.02246"
title: "What matters when building vision-language models?"
authors: ["Hugo Laurençon", "Léo Tronchon", "Matthieu Cord", "Victor Sanh"]
date: 2024-05-03
org: "Hugging Face"
tags: [multimodal, vlm, ablation, architecture, 2024]
upvotes: 104
---

# Idefics2 — What Matters When Building VLMs

> A rigorous ablation study of VLM design choices producing Idefics2, an efficient 8B VLM that matches models 4× its size.

## Key Contributions
- **Comprehensive VLM ablation study**: First systematic comparison of autoregressive vs. cross-attention architectures, visual token reduction strategies, backbone choices, and training procedures
- **Key finding — perceiver resampler hurts**: Full visual token sequences with learned pooling outperform perceiver-based compression
- **Key finding — OCR data is critical**: Adding OCR/document data dramatically improves downstream performance
- **The Cauldron dataset**: A massive collection of 50 vision-language datasets for instruction tuning
- **Idefics2**: 8B VLM achieving SOTA in its size class, often matching 32B+ models

## Method
Starting from SigLIP-SO400M (vision) and Mistral-7B-v0.1 (language), the authors ablate:
1. **Backbone choice**: Mistral-7B significantly outperforms Llama-1-7B as LM backbone (67.6 vs 62.5 avg)
2. **Architecture**: Fully autoregressive (concatenate visual tokens) vs. cross-attention — autoregressive slightly better and simpler
3. **Visual token reduction**: No pooling > perceiver resampler; but learned pooling (pixel shuffle) recovers performance at lower cost
4. **Sub-image splitting**: Splitting images into 4+ sub-images boosts performance without architecture changes
5. **Training**: Unfreezing vision encoder less helps; multi-stage pre-training (interleaved → paired → instruct) works best
6. **Instruction tuning**: Created The Cauldron — 50 diverse VL datasets covering QA, captioning, OCR, charts, documents

## Results
- Idefics2 (8B) achieves SOTA for its size class on VQAv2, TextVQA, DocVQA, MMMU
- Often on par with models 4× its size (LLaVA-NeXT-34B, CogVLM-30B)
- Instruction-tuned and chat variants released alongside base model
- The Cauldron dataset enables community reuse for VLM training

## Datasets Used
- OBELICS (350M images, 115B text tokens) — interleaved pre-training
- PMD (70M image-text pairs) + LAION-COCO — paired pre-training
- **The Cauldron** — 50 VL datasets for instruction tuning (released)

## Models Released
- **Idefics2-8B** (base, instructed, chat)

## Connections
- Builds on: IDEFICS (predecessor), [[sources/mistral-7b|Mistral 7B]] (LM backbone), SigLIP (vision encoder)
- Extended by: [[sources/smolvlm|SmolVLM]] (compact variants), Idefics3
- Related: [[sources/llava|LLaVA]], [[sources/internvl-1-5|InternVL 1.5]]
- Concepts: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|Vision-Language Models]]

## Citation
> Laurençon et al., "What matters when building vision-language models?," arXiv:2405.02246, 2024.
