---
type: source
arxiv_id: "2409.12191"
title: "Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution"
authors: ["Qwen Team"]
date: 2024-09-18
org: "Alibaba / Qwen"
tags: [multimodal, vlm, open-models, 2024]
upvotes: 79
---

# Qwen2-VL

> Alibaba's vision-language model that introduced **Naive Dynamic Resolution** and **Multimodal Rotary Position Embedding (M-RoPE)** for processing images at any resolution and videos of any duration. The foundation for [[sources/qwen25-vl|Qwen2.5-VL]]'s visual agent capabilities. 19K GitHub stars.

## Key Contributions
- **Naive Dynamic Resolution**: Processes images at their native resolution without fixed grid constraints — variable number of visual tokens based on actual content
- **Multimodal RoPE (M-RoPE)**: Extends [[sources/rope|RoPE]] to encode 3D position information: temporal (video frame), height, and width — enables unified image/video understanding
- **Video understanding**: Processes videos of 20+ minutes by encoding frames with temporal position information
- **Three sizes**: Qwen2-VL-2B, 7B, and 72B covering edge to cloud

## Method
### Naive Dynamic Resolution
Instead of resizing all images to a fixed resolution:
1. Map image to nearest supported resolution while preserving aspect ratio
2. Split into 14×14 patches
3. Each patch → visual token
4. Number of tokens varies per image (e.g., 256 for small, 1280 for high-res)

### M-RoPE (Multimodal Rotary Position Embedding)
Decomposes position encoding into three components:
- **Temporal**: Frame index for video (1 for images)
- **Height**: Row position within the image
- **Width**: Column position within the image

This naturally handles: single images, multi-resolution images, and videos of varying length.

## Results
| Model | MMMU (val) | DocVQA | ChartQA | Video-MME |
|---|---|---|---|---|
| Qwen2-VL-72B | 64.5 | 96.5 | 88.3 | 71.2 |
| GPT-4o | 69.1 | 92.8 | 85.7 | 71.9 |
| Qwen2-VL-7B | 54.1 | 94.5 | 83.0 | 63.3 |
| InternVL2-8B | 51.8 | 91.6 | 83.3 | 54.0 |

Qwen2-VL-72B approaches GPT-4o on most benchmarks while being open-weight.

## Impact
- Foundation for [[sources/qwen25-vl|Qwen2.5-VL]] (visual agent capabilities)
- M-RoPE adopted as standard for VLM positional encoding
- Demonstrated that dynamic resolution is superior to fixed-grid approaches
- 19K+ GitHub stars — one of the most popular VLM repositories

## Connections
- Extended by: [[sources/qwen25-vl|Qwen2.5-VL]]
- Builds on: [[sources/qwen25|Qwen2.5]] (LLM backbone), [[sources/rope|RoPE]] (position encoding)
- Models: [[entities/models/qwen]]
- Org: [[entities/orgs/alibaba]]
- Concepts: [[concepts/vision-language-models]], [[concepts/positional-encodings]]

## Citation
> Qwen Team, "Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution," arXiv:2409.12191, 2024.
