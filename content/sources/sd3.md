---
type: source
arxiv_id: "2403.03206"
title: "Scaling Rectified Flow Transformers for High-Resolution Image Synthesis"
authors: ["Patrick Esser", "Sumith Kulal", "Andreas Blattmann", "et al."]
date: 2024-03-05
org: "Stability AI"
tags: [diffusion, architecture, image-generation, 2024]
upvotes: 71
---

# Stable Diffusion 3 / Rectified Flow Transformers

> Introduced the **MMDiT (Multimodal Diffusion Transformer)** architecture and **rectified flow** formulation that powers **Stable Diffusion 3** and influenced **FLUX**. Demonstrated improved text-image alignment through separate text/image transformer streams with joint attention. 71 upvotes.

## Key Contributions
- **Rectified flow**: Replaced standard diffusion noise schedules with straight-line flow matching — simpler training, faster sampling
- **MMDiT architecture**: Separate weight sets for text and image modalities with **joint attention** — both modalities attend to each other
- **Improved noise sampling**: Log-normal noise schedule concentrating on medium noise levels — significant quality improvement
- **Scaling validation**: DiT-style scaling (more GFLOPs = better quality) extends to text-to-image generation
- **Three text encoders**: CLIP-L, CLIP-G, and T5-XXL for comprehensive text understanding

## Method
### Rectified Flow
Instead of the standard diffusion forward process (adding noise via fixed schedule):
```
z_t = (1 - t) · x + t · ε    (straight line from data to noise)
```
Velocity prediction: model learns v = ε - x (direction from data to noise). At inference, reverse the flow with ODE solver. Enables fewer sampling steps than standard diffusion.

### MMDiT Architecture
```
Text tokens → Text transformer stream ─┐
                                        ├── Joint attention (cross-attend) → Combined
Image tokens → Image transformer stream─┘
```
- Separate parameters for text and image processing
- Joint attention blocks where both modalities attend to each other
- Better text-image alignment than cross-attention (SDXL) or concat (DiT)

## Results
- **SD3-Medium** (2B): SOTA text-to-image quality at medium model size
- **Improved text rendering**: Significantly better at rendering text in images (T5 encoder)
- **Human preference**: Preferred over SDXL, DALL-E 3 in human evaluation
- **Scaling**: Clear quality improvement from 500M to 8B parameter models

## Impact
- **Stable Diffusion 3**: Commercial release from Stability AI using this architecture
- **FLUX** (Black Forest Labs): Built on rectified flow + MMDiT principles by same researchers
- **Rectified flow adoption**: Became standard formulation replacing DDPM/DDIM for new models
- Established that DiT + rectified flow is the future of image generation (replacing U-Net + DDPM)

## Connections
- Builds on: [[sources/dit|DiT]], [[sources/latent-diffusion|Latent Diffusion]], [[sources/sdxl|SDXL]]
- Extended by: FLUX (Black Forest Labs)
- Architecture: [[sources/siglip|SigLIP]] (vision encoder), T5 (text encoder)
- Concepts: [[concepts/diffusion-models]]

## Citation
> Esser et al., "Scaling Rectified Flow Transformers for High-Resolution Image Synthesis," ICML 2024, arXiv:2403.03206.
