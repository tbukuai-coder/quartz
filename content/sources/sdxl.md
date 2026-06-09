---
type: source
arxiv_id: "2307.01952"
title: "SDXL: Improving Latent Diffusion Models for High-Resolution Image Synthesis"
authors: ["Dustin Podell", "Zion English", "Kyle Lacey", "Andreas Blattmann", "Tim Dockhorn", "Jonas Müller", "Joe Penna", "Robin Rombach"]
date: 2023-07-04
org: "Stability AI"
tags: [diffusion, image-generation, text-to-image, 2023]
upvotes: 92
---

# SDXL — Stable Diffusion XL

> The dominant open-source text-to-image model — 3× larger UNet, dual text encoders, multi-aspect-ratio training. 2M+ HF downloads, thousands of community fine-tunes. 27K+ GitHub stars.

## Key Contributions
- **3× larger UNet**: Primarily through more attention blocks and larger cross-attention context — more transformer-like, less convolutional
- **Dual text encoders**: CLIP-ViT-L + OpenCLIP-ViT-bigG — text understanding from two complementary encoders concatenated for cross-attention
- **Multi-aspect-ratio training**: Train on multiple resolutions/aspect ratios — first open model to handle non-square images natively
- **Conditioning innovations**: Size conditioning (prevent artifacts from low-res training images) + crop conditioning (prevent crop artifacts)
- **Refinement model**: Separate image-to-image model that enhances outputs at high resolution

## Method
1. **Base UNet**: 2.6B params (vs. SD 1.5's 860M). More attention blocks, especially at lower resolutions. Cross-attention dimension doubled via dual text encoders
2. **Text encoding**: Concatenate CLIP-ViT-L (penultimate hidden states) + OpenCLIP-ViT-bigG (pool + hidden states) → richer text representation
3. **Conditioning**: Add original image size and crop coordinates as conditioning signals — model learns to "undo" resizing/cropping artifacts
4. **Multi-aspect training**: Bucket images by aspect ratio, train each batch at a single ratio. Supports 512×512 to 2048×512+
5. **Refinement**: Separate SDEdit-style model trained on noising-denoising at low noise levels — sharpens details at full resolution

## Results
- Dramatically better prompt adherence, image quality, and coherence vs. SD 1.5/2.1
- Multi-aspect ratio: natural handling of landscape, portrait, square
- Community adoption: Thousands of LoRA fine-tunes, ControlNet adapters, IP-Adapters on HF Hub
- Most fine-tuned diffusion model in history
- Foundation for SD3, Flux, and subsequent architectures

## Models Released
- **SDXL-base-1.0** — 2M+ HF downloads
- **SDXL-refiner-1.0** — refinement model
- **SDXL-turbo** — distilled 1-step version

## Connections
- Builds on: [[sources/latent-diffusion|Latent Diffusion / Stable Diffusion]]
- Extended by: SD3 (flow matching + DiT), FLUX (rectified flow)
- Related: [[sources/cogvideox|CogVideoX]] (video generation)
- Concepts: [[concepts/diffusion-models|Diffusion Models]]

## Citation
> Podell et al., "SDXL: Improving Latent Diffusion Models for High-Resolution Image Synthesis," arXiv:2307.01952, 2023.
