---
type: source
arxiv_id: "2212.09748"
title: "Scalable Diffusion Models with Transformers"
authors: ["William Peebles", "Saining Xie"]
date: 2022-12-19
org: "UC Berkeley / NYU"
tags: [diffusion, architecture, image-generation, foundational, 2022]
upvotes: 17
---

# DiT: Diffusion Transformers

> Replaced the U-Net backbone in latent diffusion models with a **Transformer** — establishing the **Diffusion Transformer (DiT)** architecture that underpins modern image generators including **FLUX**, **Stable Diffusion 3**, and **Sora**. Showed that DiTs scale predictably with compute: higher GFLOPs consistently yield lower FID.

## Key Contributions
- **Transformer backbone for diffusion**: Replaced U-Net with a Transformer operating on latent patches — simpler, more scalable
- **Scaling law for diffusion**: Forward pass GFLOPs strongly predict generation quality (FID) — larger transformers = better images
- **DiT-XL/2**: Achieved 2.27 FID on class-conditional ImageNet 256×256 — SOTA at the time
- **Patchification**: Converts spatial latents into a sequence of patches for transformer processing
- **AdaLN-Zero conditioning**: Adaptive LayerNorm with zero initialization for class conditioning — best conditioning mechanism

## Method
```
Image → VAE encoder → latent (32×32×4)
  → Patchify (e.g., 2×2 patches → 256 tokens)
    → DiT blocks (self-attention + FFN with AdaLN-Zero)
      → Unpatchify → predicted noise
        → Diffusion denoising → VAE decode → Image
```

### Architecture Variants
| Model | Layers | Hidden | Heads | GFLOPs | FID-50K |
|---|---|---|---|---|---|
| DiT-S/2 | 12 | 384 | 6 | 6.1 | 68.4 |
| DiT-B/2 | 12 | 768 | 12 | 23.0 | 43.5 |
| DiT-L/2 | 24 | 1024 | 16 | 80.7 | 9.62 |
| DiT-XL/2 | 28 | 1152 | 16 | 118.6 | **2.27** |

## Impact
DiT became the foundation for the next generation of image/video generators:
- **Stable Diffusion 3** (Stability AI): MMDiT architecture based on DiT principles
- **FLUX** (Black Forest Labs): Rectified flow + DiT-based architecture
- **Sora** (OpenAI): Video generation using DiT-like architecture
- **CogVideoX** ([[sources/cogvideox]]): Video generation with 3D DiT
- Replaced U-Net as the dominant backbone in diffusion models

## Connections
- Extended by: SD3/FLUX (rectified flow + DiT), Sora (video DiT)
- Builds on: [[sources/latent-diffusion|Latent Diffusion]], [[sources/attention-is-all-you-need|Transformer]]
- Related: [[concepts/diffusion-models]], [[concepts/transformer-architecture]]

## Citation
> Peebles & Xie, "Scalable Diffusion Models with Transformers," ICCV 2023, arXiv:2212.09748.
