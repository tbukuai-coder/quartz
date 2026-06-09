---
type: source
arxiv_id: "2304.08485"
title: "Visual Instruction Tuning"
authors: ["Haotian Liu", "Chunyuan Li", "Qingyang Wu", "Yong Jae Lee"]
date: 2023-04-17
org: "University of Wisconsin / Microsoft"
tags: [multimodal, vision-language, instruction-tuning, foundational, 2023]
upvotes: 21
---

# LLaVA: Visual Instruction Tuning

> Introduced **Large Language and Vision Assistant (LLaVA)** — the first major open-source multimodal model connecting a vision encoder to an LLM via instruction tuning, establishing the template for open multimodal models.

## Key Contributions
- First attempt to use **language-only GPT-4** to generate multimodal instruction-following data
- Connected a **CLIP vision encoder** to a language model (Vicuna/LLaMA) via a simple projection layer
- Demonstrated strong multimodal chat capabilities with relatively simple architecture
- Established the **LLaVA paradigm**: vision encoder + projection + LLM, widely adopted since
- Released model, data, and code fully open-source

## Method
### Architecture
```
Image → CLIP ViT-L/14 → Linear Projection → LLM (Vicuna 13B) → Response
```

1. **Vision Encoder**: Pre-trained CLIP ViT-L/14 (frozen or fine-tuned)
2. **Projection Layer**: Simple linear or MLP layer mapping visual tokens into the LLM's embedding space
3. **LLM Backbone**: Vicuna 13B (LLaMA fine-tuned on ShareGPT)

### Training
1. **Stage 1 — Feature Alignment**: Train only the projection layer on image-caption pairs
2. **Stage 2 — Visual Instruction Tuning**: Fine-tune end-to-end on GPT-4-generated visual instruction data

### Data Generation
- Used GPT-4 (text-only) with image captions and bounding boxes as context
- Generated three types of data: conversations, detailed descriptions, complex reasoning
- 158K visual instruction-following samples

## Results
- Strong multimodal chat and reasoning capabilities
- Competitive with GPT-4V on some tasks (at the time)
- 90.92% relative score vs. GPT-4 on multimodal evaluation
- SOTA on Science QA when combined with chain-of-thought

## Connections
- **Builds on**: [[sources/llama]] (LLM backbone), CLIP (vision encoder), [[sources/self-instruct]] (data generation paradigm)
- **Influenced**: LLaVA-1.5, LLaVA-NeXT, countless multimodal models, [[sources/gemma-3]] (multimodal Gemma)
- **Key concepts**: [[concepts/instruction-tuning]], [[concepts/fine-tuning]], [[concepts/multimodal-models]]
- **Organizations**: University of Wisconsin, Microsoft

## Citation
> Liu et al., "Visual Instruction Tuning," arXiv:2304.08485, 2023.
> https://huggingface.co/papers/2304.08485
