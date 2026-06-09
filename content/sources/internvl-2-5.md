---
type: source
arxiv_id: "2412.05271"
title: "Expanding Performance Boundaries of Open-Source Multimodal Models with Model, Data, and Test-Time Scaling"
authors: ["Zhe Chen", "Weiyun Wang", "Yue Cao", "Yangzhou Liu", "Zhangwei Gao", "Erfei Cui", "Jinguo Zhu", "Shenglong Ye", "Hao Tian", "Zhaoyang Liu"]
date: 2024-12-06
org: "Shanghai AI Lab"
tags: [multimodal, vlm, scaling, test-time-scaling, mmmu, 2024]
upvotes: 161
---

# InternVL 2.5

> First open-source MLLM to surpass 70% on MMMU, with systematic study of model, data, and test-time scaling for multimodal understanding — rivals GPT-4o and Claude 3.5 Sonnet.

## Key Contributions
- **First open MLLM >70% on MMMU** — achieved through Chain-of-Thought reasoning (3.7-point improvement from CoT alone)
- **Triple scaling study**: Systematically explores vision encoder scaling, LLM scaling, dataset scaling, and test-time scaling together
- **Progressive scaling strategy**: Train smaller models first, use them to improve larger ones — efficient training pipeline
- **Comprehensive evaluation**: 29+ benchmarks covering reasoning, OCR, video, grounding, multilingual, hallucination

## Method
1. **Architecture**: Same "ViT-MLP-LLM" as InternVL 1.5 — InternViT (300M or 6B) + MLP + various LLMs (1.8B to 78B)
2. **Progressive scaling**: Train InternViT-300M + small LLM first → generate synthetic data → train larger model. Each size bootstraps the next
3. **Training pipeline**: 3-stage — (1) MLP warmup (frozen ViT+LLM), (1.5) optional ViT incremental learning, (2) full model instruction tuning
4. **Data improvements**: 16.3M fine-tuning samples (2× over InternVL 2.0), with emphasis on:
   - Random JPEG compression augmentation (prevents overfitting to clean images)
   - Loss reweighting for response-only tokens
   - Multimodal data packing (concatenate samples to maximize GPU utilization)
   - Data filtering pipeline to remove anomalous samples
5. **Test-time scaling**: CoT prompting provides 3.7-point improvement on MMMU

## Results
- **MMMU val: 70.1%** (first open MLLM >70%)
- Competitive with GPT-4o across 29 benchmarks
- Strong on: multi-discipline reasoning, document understanding, video understanding, visual grounding
- Model sizes: 1B to 78B total parameters
- InternViT-6B continuously trained shows steady improvement with each iteration
- Video understanding: competitive on Video-MME, MVBench, MLVU

## Datasets Used
- 16.3M fine-tuning samples across diverse tasks
- Pre-training: public captioning, OCR, document, chart, and grounding datasets
- Progressive scaling: synthetic data from smaller models in the family

## Models Released
- **InternVL2.5-{1B, 2B, 4B, 8B, 26B, 38B, 78B}** — full model family
- Available on Hugging Face Hub (most downloaded open VLM family)

## Connections
- Builds on: [[sources/internvl-1-5|InternVL 1.5]] (architecture + InternViT)
- Related: [[sources/qwen25-vl|Qwen2.5-VL]], [[sources/smolvlm|SmolVLM]], [[sources/idefics2|Idefics2]]
- Concepts: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|Vision-Language Models]], [[concepts/test-time-compute|Test-Time Compute Scaling]]
- Org: [[entities/orgs/shanghai-ai-lab|Shanghai AI Lab / OpenGVLab]]

## Citation
> Chen et al., "Expanding Performance Boundaries of Open-Source Multimodal Models with Model, Data, and Test-Time Scaling," arXiv:2412.05271, 2024.
