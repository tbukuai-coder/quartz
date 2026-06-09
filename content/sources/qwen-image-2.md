---
type: source
arxiv_id: "2605.10730"
title: "Qwen-Image-2.0 Technical Report"
authors: ["Bing Zhao", "Chenfei Wu", "Deqing Li", "Hao Meng", "Jiahao Li", "Jie Zhang", "Jingren Zhou", "Junyang Lin", "Kaiyuan Gao", "Kuan Cao"]
date: 2026-05-12
org: "Alibaba / Qwen Team"
tags: [image-generation, diffusion, multimodal, editing, text-rendering, 2026]
upvotes: 110
---

# Qwen-Image-2.0 Technical Report

> Omni-capable image generation foundation model unifying high-fidelity synthesis and precise editing via Qwen3-VL condition encoder + Multimodal Diffusion Transformer, excelling at ultra-long text rendering, multilingual typography, and compositional generation.

## Key Contributions
- **Unified generation + editing framework**: single model handles text-to-image, image editing, and conditional generation
- **Qwen3-VL as condition encoder**: repurposes a powerful VLM to encode complex multimodal conditions (text, images, layouts) for the diffusion model
- **Multimodal Diffusion Transformer (MMDiT)**: joint condition-target modeling for coherent generation
- **Ultra-long text rendering**: handles paragraphs of text in generated images with correct typography
- **Multilingual typography**: generates text in multiple languages with proper fonts and layout
- **Large-scale data curation + multi-stage training pipeline**: progressive training from low to high resolution with quality-filtered data at each stage

## Method
Qwen-Image-2.0 couples Qwen3-VL as the condition encoder (understanding complex text and image inputs) with a Multimodal Diffusion Transformer for joint condition-target modeling. The condition encoder provides rich semantic features that guide the diffusion process. A multi-stage training pipeline progressively increases resolution and quality. Large-scale data curation focuses on text-rich, compositionally complex scenarios.

## Results
- SOTA on text rendering benchmarks (long passages, multilingual)
- High-fidelity photorealistic generation competitive with DALL-E 3 and SD3.5
- Robust instruction following for complex editing tasks
- Efficient deployment for production use

## Connections
- Builds on: [[sources/sd3]], [[sources/dit]], [[sources/qwen25-vl]], [[concepts/diffusion-models]]
- Related: [[sources/joyai-image]], [[sources/edit-r1]], [[entities/orgs/alibaba]]
- Related concepts: [[concepts/multimodal-models]], [[concepts/tokenization]], [[comparisons/diffusion-architectures]]
- Organization: [[entities/orgs/alibaba]]

## Citation
> Zhao et al., "Qwen-Image-2.0 Technical Report," arXiv:2605.10730, 2026.
