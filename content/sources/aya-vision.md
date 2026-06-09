---
type: source
arxiv_id: "2505.08751"
title: "Aya Vision: Advancing the Frontier of Multilingual Multimodality"
authors: ["Saurabh Dash", "Yiyang Nan", "John Dang", "Arash Ahmadian", "Shivalika Singh", "Madeline Smith", "Bharat Venkitesh", "Vlad Shmyhlo", "Viraat Aryabumi", "Walter Beller-Morales"]
date: 2025-05-14
org: "Cohere / Cohere For AI"
tags: [multimodal, vlm, multilingual, cohere, synthetic-data, model-merging, 2025]
upvotes: 13
---

# Aya Vision: Advancing the Frontier of Multilingual Multimodality

> Cohere's multilingual multimodal model family that uses a synthetic annotation framework and cross-modal model merging to achieve best-in-class performance across many languages — Aya-Vision-8B rivals much larger models like Llama-3.2-90B-Vision.

## Key Contributions
- **Synthetic annotation framework**: Curates high-quality, diverse multilingual multimodal instruction data, enabling natural human-preferred responses across many languages
- **Cross-modal model merging**: A novel technique that mitigates catastrophic forgetting, preserving text-only capabilities while enhancing multimodal generative performance
- **Best-in-class at 8B**: Aya-Vision-8B outperforms Qwen-2.5-VL-7B, Pixtral-12B, and Llama-3.2-90B-Vision
- **Scalable to 32B**: Aya-Vision-32B outperforms models more than twice its size (Molmo-72B, LLaMA-3.2-90B-Vision)
- **Multilingual-first**: Extends the Aya project's multilingual mission to the multimodal frontier

## Method

### Synthetic Annotation Framework
Aya Vision develops a data generation pipeline that:
1. Starts with multilingual text instructions from the Aya project
2. Generates corresponding visual content and image-text pairs
3. Curates for diversity, quality, and multilingual coverage
4. Produces natural, human-preferred responses across languages

This addresses the fundamental data scarcity problem for multilingual multimodal data — machine translation often distorts meaning in visual contexts.

### Cross-Modal Model Merging
A novel technique to combine:
- **Text-only model**: Retains strong text capabilities (prevents catastrophic forgetting)
- **Multimodal model**: Adds vision capabilities

The merging operates in weight space to preserve text-only performance while enhancing multimodal output quality. This is particularly important for multilingual models where vision introduction often degrades existing text capabilities.

### Training
- Base model: Aya text foundation
- Vision encoder: Standard vision transformer
- Connector: MLP projection layers
- Training data: Synthetic multilingual multimodal instruction data
- Post-training: SFT + RLHF for response quality

## Results

### Performance Comparison

| Model | Size | Relative Performance |
|---|---|---|
| Aya-Vision-8B | 8B | Best-in-class vs Qwen2.5-VL-7B, Pixtral-12B, Llama-3.2-90B |
| Aya-Vision-32B | 32B | Outperforms Molmo-72B, Llama-3.2-90B-Vision |

Key design insight: The cross-modal merging technique effectively "bends the need for compute" — delivering extremely high performance with smaller parameter counts by preserving and enhancing complementary capabilities.

## Connections
- Builds on: [[sources/aya|Aya]] (multilingual text model), [[sources/llava|LLaVA]] (VLM architecture), [[sources/qwen25-vl|Qwen2.5-VL]] (competing multilingual VLM)
- Cited by / Influenced: Extends Aya coverage into multimodal domain; demonstrates synthetic data + model merging as a powerful combination
- Related concepts: [[concepts/multilingual-models|Multilingual Models]], [[concepts/vision-language-models|Vision-Language Models]], [[concepts/model-merging|Model Merging]]
- Related orgs: [[entities/orgs/cohere|Cohere / Cohere For AI]] (creators)
- Related papers: [[sources/cambrian|Cambrian-1]] (vision-centric MLLM), [[sources/aya|Aya]] (multilingual text foundation)

## Citation
> Dash et al., "Aya Vision: Advancing the Frontier of Multilingual Multimodality," arXiv:2505.08751, 2025.
