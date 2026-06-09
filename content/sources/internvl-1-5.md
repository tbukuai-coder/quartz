---
type: source
arxiv_id: "2404.16821"
title: "How Far Are We to GPT-4V? Closing the Gap to Commercial Multimodal Models with Open-Source Suites"
authors: ["Zhe Chen", "Weiyun Wang", "Hao Tian", "Shenglong Ye", "Zhangwei Gao", "Erfei Cui", "Wenwen Tong", "Kongzhi Hu", "Jiapeng Luo", "Zheng Ma"]
date: 2024-04-25
org: "Shanghai AI Lab"
tags: [multimodal, vlm, vision-encoder, high-resolution, bilingual, 2024]
upvotes: 59
---

# InternVL 1.5

> An open-source MLLM that closes the gap to GPT-4V through a strong continuously-trained vision encoder (InternViT-6B), dynamic high-resolution input, and a high-quality bilingual dataset.

## Key Contributions
- **InternViT-6B continuous learning**: Instead of freezing the vision encoder, continuously trains it to improve visual understanding — transferable across different LLMs
- **Dynamic high-resolution**: Divides images into 1–40 tiles of 448×448 pixels based on aspect ratio, supporting up to 4K resolution input
- **High-quality bilingual dataset**: Carefully annotated English/Chinese QA pairs for OCR and document understanding
- **SOTA on 8 of 18 benchmarks** — competitive with GPT-4V and Gemini Pro

## Method
InternVL 1.5 follows the "ViT-MLP-LLM" paradigm:
1. **Vision encoder**: InternViT-6B, continuously pre-trained on diverse vision tasks (not frozen) — can be reused with different LLMs
2. **Dynamic tiles**: Input image is divided into 1–40 tiles of 448×448 based on closest aspect ratio matching. A thumbnail is always included. Total visual tokens scale with image complexity
3. **Language model**: InternLM2-20B connected via 2-layer MLP projection
4. **Bilingual data**: Proprietary + public OCR/document datasets annotated with English and Chinese QA pairs using GPT-4V + human verification
5. **Training**: 2-stage — (1) MLP alignment with frozen ViT+LLM, (2) Full model fine-tuning

## Results
- SOTA on 8 of 18 multimodal benchmarks
- Competitive with GPT-4V on OCR-related tasks (DocVQA, ChartQA, InfoVQA)
- Strong Chinese language understanding alongside English
- Finding: larger LLMs benefit more from larger vision encoders (InternViT-6B >> CLIP-ViT-L with 34B LLMs)
- Spawned InternVL 2.0 and [[sources/internvl-2-5|InternVL 2.5]] — most downloaded open VLM family on HF Hub

## Datasets Used
- Public: LLaVA-mix665K, ShareGPT4V, DocVQA, ChartQA, AI2D, InfoVQA
- Custom bilingual OCR/document QA datasets (English + Chinese)
- Pre-training: LAION-en/zh, COYO, Wukong, CC-3M/12M

## Models Released
- **InternVL-Chat-V1-5** — 26B total (InternViT-6B + InternLM2-20B)
- **InternVL-Chat-V1-5-Int8** — quantized version

## Connections
- Extended by: [[sources/internvl-2-5|InternVL 2.5]] (MMMU >70%, test-time scaling)
- Related: [[sources/llava|LLaVA]], [[sources/idefics2|Idefics2]], [[sources/qwen25-vl|Qwen2.5-VL]]
- Concepts: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|Vision-Language Models]]
- Org: [[entities/orgs/shanghai-ai-lab|Shanghai AI Lab / OpenGVLab]]

## Citation
> Chen et al., "How Far Are We to GPT-4V? Closing the Gap to Commercial Multimodal Models with Open-Source Suites," arXiv:2404.16821, 2024.
