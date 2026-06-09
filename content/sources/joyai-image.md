---
type: source
arxiv_id: "2605.04128"
title: "Awaking Spatial Intelligence in Unified Multimodal Understanding and Generation"
authors: ["Lin Song", "Wenbo Li", "Guoqing Ma", "Wei Tang", "Bo Wang", "Yuan Zhang", "Yijun Yang", "Yicheng Xiao", "Jianhui Liu", "Yanbing Zhang"]
venue: "arXiv preprint"
year: 2026
date: "2026-05"
org: "JD.com"
upvotes: 10
tags: [multimodal, text-to-image, image-editing, spatial-intelligence, unified-model, diffusion]
github: "https://github.com/jd-opensource/JoyAI-Image"
---

# JoyAI-Image: Awaking Spatial Intelligence in Unified Multimodal Understanding and Generation

> A unified multimodal foundation model coupling a **spatially enhanced MLLM** with a **Multimodal Diffusion Transformer (MMDiT)** for visual understanding, text-to-image generation, and instruction-guided editing — enabling a bidirectional loop between perception and generation for stronger **spatial intelligence**.

## Key Contributions

1. **Unified architecture**: MLLM + VAE + MMDiT sharing a multimodal interface — perception and generation interact bidirectionally
2. **Spatial intelligence**: OpenSpatial data engine synthesizes 3D-box-centric spatial QA pairs; model achieves SOTA on spatial reasoning benchmarks
3. **Long-text rendering**: Dedicated supervision for text-heavy image generation (signage, documents, UI mockups)
4. **Instruction-guided editing**: JoyAI-Image-Edit handles diverse editing types with content preservation via learnable token injection
5. **Thinking with Novel Views (TwNV)**: Application pipeline where the model plans camera motions, synthesizes novel views, then reasons over multi-view inputs — improving spatial QA accuracy
6. **2,119 GitHub ⭐**: High community adoption

## Method

### Architecture
- **MLLM**: Spatially enhanced via OpenSpatial SFT on Qwen3-VL-8B — achieves 3D-grounded spatial reasoning
- **VAE**: Wan-2.1-VAE with causal 3D convolutions for high-fidelity latent compression
- **MMDiT**: Multimodal Diffusion Transformer jointly modeling text conditions, source images, and noisy latents
- **Shared interface**: MLLM provides spatial understanding that guides MMDiT generation; generated views feed back to MLLM for multi-view reasoning

### OpenSpatial: Automated Spatial Data Engine
- Synthesizes spatially-grounded QA from unified 3D box-centric representation
- Bridges 2D semantic understanding and 3D spatial intelligence
- Categories: depth estimation, spatial relationships, 3D grounding, novel view reasoning

### Training Recipe
1. **Spatial SFT**: Full-parameter fine-tuning on Qwen3-VL-8B with OpenSpatial data
2. **T2I pre-training**: Flow matching objective on progressive multi-stage data pipeline
3. **T2I fine-tuning**: High-quality data + long-text rendering supervision + DPO alignment
4. **Editing training**: Learnable token injection (SiLU gating) for source-image conditioning

## Results

### Spatial Understanding
- SOTA or competitive across 3D spatial benchmarks (ScanQA, VSR, spatial reasoning)
- OpenSpatial SFT significantly improves Qwen3-VL-8B on depth, relationships, grounding

### Text-to-Image Generation
- Competitive with FLUX.1-dev, DALL-E 3, Midjourney on general quality
- **SOTA on long-text rendering** — accurately renders complex text in images
- Strong instruction following and stylistic diversity

### Image Editing
- JoyAI-Image-Edit outperforms concurrent methods on spatial editing tasks
- High content preservation + precise instruction following
- Handles: object manipulation, style transfer, background changes, spatial rearrangement

### Thinking with Novel Views (TwNV)
- Accuracy improvements on spatial QA by generating and reasoning over novel views
- Demonstrates bidirectional perception-generation loop as reasoning strategy

## Connections

- [[sources/edit-r1|Edit-R1]] — RL for image editing; JoyAI focuses on spatial intelligence + unified architecture
- [[concepts/diffusion-models|Diffusion Models]] — MMDiT-based generation with flow matching
- [[concepts/multimodal-models|Multimodal Models]] — Unified understanding + generation in single model
- [[concepts/vision-language-models|Vision-Language Models]] — Spatially enhanced VLM component
- [[comparisons/vision-language-models|VLM Comparison]] — Adds unified understanding+generation paradigm
- [[sources/sd3|SD3]] — Flow-matching diffusion; JoyAI extends with spatial MLLM coupling
- [[entities/orgs/alibaba|Alibaba]] — JD.com competitor; similar unified model direction (Qwen-VL)
