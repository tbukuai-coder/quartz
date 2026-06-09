---
type: source
arxiv_id: "2112.10752"
title: "High-Resolution Image Synthesis with Latent Diffusion Models"
authors: ["Robin Rombach", "Andreas Blattmann", "Dominik Lorenz", "Patrick Esser", "Björn Ommer"]
date: 2021-12-20
org: "CompVis / Stability AI"
tags: [diffusion, image-generation, foundational]
upvotes: 17
---

# Latent Diffusion Models (Stable Diffusion)

> Introduced **Latent Diffusion Models (LDMs)** — performing the diffusion process in a compressed latent space rather than pixel space, making high-quality image generation computationally feasible. This is the paper behind **Stable Diffusion**.

## Key Contributions
- Moved diffusion from **pixel space to latent space** — reducing compute by 10–100×
- Used a **pre-trained autoencoder** to compress images into a lower-dimensional latent space
- Introduced **cross-attention conditioning** for flexible text, layout, and semantic guidance
- Made high-resolution image synthesis practical on consumer GPUs
- Foundation for **Stable Diffusion** — the most widely used open image generation model

## Method
### Two-Stage Architecture
1. **Autoencoder**: Compress images into a compact latent representation (`z = E(x)`)
   - Encoder `E`: Image → Latent space
   - Decoder `D`: Latent space → Image
   - Trained with perceptual loss + adversarial loss

2. **Diffusion Model in Latent Space**:
   - U-Net based denoising model operates on the latent representation
   - Standard DDPM training: add noise, learn to predict noise
   - Much cheaper than pixel-space diffusion (latent is 4–16× smaller)

3. **Cross-Attention Conditioning**:
   - Condition on text (CLIP embeddings), layouts, semantic maps, etc.
   - Cross-attention layers in the U-Net attend to conditioning embeddings
   - Enables text-to-image, inpainting, super-resolution, semantic synthesis

## Results
- SOTA on image inpainting, class-conditional generation, text-to-image
- Training cost reduced by ~10× compared to pixel-space diffusion
- Inference on a single consumer GPU
- Foundation for Stable Diffusion 1.x, 2.x, SDXL, and community ecosystem

## Connections
- **Foundation for**: Stable Diffusion, SDXL, Stable Diffusion 3, community models
- **Key concepts**: [[concepts/diffusion-models]], [[concepts/latent-space]]
- **Related**: [[sources/llava]] (multimodal ecosystem), DALL-E (OpenAI)
- **Organizations**: CompVis (LMU Munich), Stability AI

## Citation
> Rombach et al., "High-Resolution Image Synthesis with Latent Diffusion Models," arXiv:2112.10752, 2021.
> https://huggingface.co/papers/2112.10752
