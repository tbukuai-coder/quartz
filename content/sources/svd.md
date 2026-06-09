---
type: source
arxiv_id: "2311.15127"
title: "Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets"
authors: ["Andreas Blattmann", "Tim Dockhorn", "Sumith Kulal", "et al."]
date: 2023-11-25
org: "Stability AI"
tags: [video-generation, diffusion, open-models, 2023]
upvotes: 15
---

# Stable Video Diffusion (SVD)

> The first high-quality **open video generation model** — extends Stable Diffusion's latent diffusion approach to video by adding **temporal layers** to the U-Net. Demonstrates a **three-stage training pipeline** (image pretraining → video pretraining → high-quality video finetuning) and introduces systematic video data curation.

## Key Contributions
- **Open video generation**: First competitive open-source video generation model
- **Three-stage training**: Image → video → HQ video finetuning pipeline
- **Data curation matters**: Systematic study of how video data quality affects generation quality
- **Image-to-video**: Particularly strong at animating static images
- **Temporal attention**: Added temporal self-attention and cross-frame attention to SD's U-Net

## Method
### Three-Stage Training
1. **Image pretraining**: Start with Stable Diffusion 2.1 (strong image prior)
2. **Video pretraining**: Add temporal layers, train on large video dataset (LVD, 580M clips)
3. **HQ video finetuning**: Fine-tune on small curated high-quality video set

### Architecture
- Base: SD 2.1 U-Net with added temporal attention layers
- Temporal layers: Self-attention across frames for motion consistency
- Conditioning: First frame (image-to-video) or text prompt (text-to-video)

### Data Curation (Key Finding)
The paper's most important finding: **video data quality is more important than quantity**.
- Large Video Dataset (LVD): 580M video clips from web
- Systematic filtering by: optical flow, aesthetic score, text-video alignment, caption quality
- Well-curated 1M clip subset outperforms training on full 580M

## Impact
- First open-source video generation model competitive with proprietary systems
- SVD-XT: Extended to 25 frames (vs. 14 in base)
- Foundation for many community video generation tools
- Demonstrated that image diffusion models can be efficiently adapted to video
- Preceded DiT-based video models (CogVideoX, Sora) which later surpassed U-Net approach

## Connections
- Builds on: [[sources/latent-diffusion|Latent Diffusion]], [[sources/sdxl|SDXL]]
- Succeeded by: [[sources/cogvideox|CogVideoX]] (DiT-based video)
- Org: [[entities/orgs/stability-ai|Stability AI]]
- Concepts: [[concepts/diffusion-models]]
- Models: [[entities/models/stable-diffusion]]
- Comparisons: [[comparisons/diffusion-architectures]]

## Citation
> Blattmann et al., "Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets," arXiv:2311.15127, 2023.
