---
type: source
arxiv_id: "2504.05299"
title: "SmolVLM: Redefining small and efficient multimodal models"
authors: ["Andrés Marafioti", "Orr Zohar", "Miquel Farré", "Merve Noyan", "Elie Bakouch", "Pedro Cuenca", "Cyril Zakka", "Loubna Ben Allal", "Anton Lozhkov", "Nouamane Tazi"]
date: 2025-04-07
org: "Hugging Face"
tags: [multimodal, vlm, small-model, efficiency, vision, video, 2025]
upvotes: 207
---

# SmolVLM

> A family of compact vision-language models (256M–2.2B) that achieve competitive multimodal performance with minimal GPU memory, enabling deployment on mobile and edge devices.

## Key Contributions
- **Aggressive image tokenization**: 4× fewer visual tokens than Idefics2 with no quality loss, via pixel shuffle pooling
- **Systematic VLM design exploration**: Rigorous ablations on compute allocation between vision and language towers, image encoding strategies, and video handling
- **Three model variants**: SmolVLM-256M (<1GB VRAM), SmolVLM-500M, SmolVLM-2.2B — each optimized for different deployment scenarios
- **SmolVLM-256M surpasses Idefics-80B** (a 300× larger model from 18 months earlier)

## Method
SmolVLM combines a SigLIP vision encoder with [[entities/models/smollm|SmolLM2]] as the language backbone. Key design decisions validated through ablation:
1. **Compute allocation**: Smaller vision encoders (SigLIP-B/16 at 93M) complement compact LMs better than larger encoders
2. **Pixel shuffle pooling**: Reduces visual token count by 4× while preserving spatial information — outperforms perceiver resampler approaches
3. **Learned positional tokens**: Special tokens for sub-image positions prevent "OCR loss plague" that occurs with string-based position encoding
4. **Structured prompts**: System prompts and media intro/outro prefixes improve performance
5. **Video via frame sampling**: Shared encoding with images; 2-minute optimal video duration during training

## Results
- SmolVLM-256M: <1GB GPU memory, outperforms Idefics-80B across benchmarks
- SmolVLM-2.2B: Rivals models consuming 2× more GPU memory
- Strong performance on DocVQA, TextVQA, ChartQA, MMMU, and video benchmarks
- Real-time inference on NVIDIA L4 GPUs; practical for mobile deployment
- Robust video comprehension capabilities alongside static image understanding

## Datasets Used
- The Cauldron (50+ VL datasets) — from [[sources/idefics2|Idefics2]]
- MathWriting (added for formula recognition)
- Video datasets with 2-minute average duration
- Chain-of-thought data (proportion carefully tuned — too much hurts small models)

## Models Released
- **SmolVLM-256M** — 256M params, <1GB VRAM
- **SmolVLM-500M** — 500M params
- **SmolVLM-2.2B** — 2.2B params, flagship

## Connections
- Builds on: [[sources/idefics2|Idefics2]] (design framework), [[sources/smollm2|SmolLM2]] (language backbone)
- Lineage: Flamingo → IDEFICS → [[sources/idefics2|Idefics2]] → Idefics3 → SmolVLM
- Related: [[sources/llava|LLaVA]], [[sources/internvl-1-5|InternVL 1.5]], [[sources/qwen25-vl|Qwen2.5-VL]]
- Concepts: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|Vision-Language Models]]

## Citation
> Marafioti et al., "SmolVLM: Redefining small and efficient multimodal models," arXiv:2504.05299, 2025.
