---
type: source
arxiv_id: "2502.13923"
title: "Qwen2.5-VL Technical Report"
authors: ["Shuai Bai", "Keqin Chen", "Xuejing Liu", "Jialin Wang", "Wenbin Ge", "Sibo Song", "Kai Dang", "Peng Wang", "Shijie Wang", "Jun Tang"]
date: 2025-02-19
org: "Alibaba"
tags: [multimodal, vlm, video, document, agent, 2025]
upvotes: 218
---

# Qwen2.5-VL

> The flagship Qwen vision-language model with dynamic resolution ViT, native video comprehension up to hours, and visual agent capabilities — matching GPT-4o on document/diagram understanding.

## Key Contributions
- **Native dynamic-resolution ViT**: Trained from scratch with Window Attention, processes any image resolution without normalization — perceives true spatial scales
- **Multimodal RoPE (M-RoPE)**: Extends [[concepts/self-attention|RoPE]] to encode temporal (video timestamps) and spatial (image positions) information jointly
- **Absolute time encoding**: Second-level video event localization across hours of video content
- **Visual agent capability**: Can operate computers and mobile devices through reasoning and tool use
- **Three sizes**: 3B, 7B, 72B — covering edge to high-performance computing

## Method
1. **Vision encoder**: ViT trained from scratch with dynamic resolution — Window Attention reduces computation while maintaining native resolution processing. No fixed tile grid; resolution adapts to input
2. **M-RoPE**: Decomposes positional encoding into temporal, height, and width components — enables natural understanding of spatial layout in documents and temporal ordering in videos
3. **Absolute time encoding**: Video frames tagged with real timestamps (not frame indices), enabling temporal reasoning ("what happened at 1:23?")
4. **Training**: Multi-stage with image, document, video, and agent tasks; builds on [[sources/qwen25|Qwen2.5]] language backbone
5. **Agent training**: Includes GUI grounding, computer use, and mobile device interaction data

## Results
- **72B model matches GPT-4o and Claude 3.5 Sonnet** on DocVQA, ChartQA, diagram understanding
- Excels at structured data extraction from invoices, forms, tables
- Native video comprehension up to hours with second-level event localization
- Visual agent: operates computers/phones through visual reasoning
- Maintains core language competencies of [[sources/qwen25|Qwen2.5]] LLM
- 218 HF upvotes — one of the highest for any VLM paper

## Datasets Used
- Multi-stage training on image, video, document, OCR, chart, agent, and code data
- Proprietary + public datasets covering diverse visual understanding tasks

## Models Released
- **Qwen2.5-VL-3B** — edge/mobile deployment
- **Qwen2.5-VL-7B** — balanced performance/efficiency
- **Qwen2.5-VL-72B** — flagship, GPT-4o competitive

## Connections
- Builds on: [[sources/qwen25|Qwen2.5]] (language model), Qwen2-VL (predecessor)
- Competes with: [[sources/internvl-2-5|InternVL 2.5]], GPT-4o, Claude 3.5 Sonnet
- Related: [[sources/llava|LLaVA]], [[sources/smolvlm|SmolVLM]], [[sources/idefics2|Idefics2]]
- Org: [[entities/orgs/alibaba|Alibaba / Qwen]]
- Concepts: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|Vision-Language Models]], [[concepts/agents|Agents]]

## Citation
> Bai et al., "Qwen2.5-VL Technical Report," arXiv:2502.13923, 2025.
