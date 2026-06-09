---
type: entity
category: model
tags: [diffusion, image-generation, foundational]
---

# Stable Diffusion

> The most widely used **open-source image generation** model family, based on Latent Diffusion Models — enabling text-to-image, inpainting, and image editing on consumer hardware.

## Overview
Stable Diffusion, based on the Latent Diffusion Model paper, moved image generation to a compressed latent space, making high-quality generation practical on consumer GPUs. It spawned a massive ecosystem of community models, LoRA adapters, ControlNets, and applications.

## Model Family
| Model | Year | Architecture | Resolution | Key Feature |
|---|---|---|---|---|
| SD 1.5 | 2022 | U-Net LDM | 512px | First widely adopted version |
| SD 2.0/2.1 | 2022 | U-Net LDM | 768px | OpenCLIP, v-prediction |
| SDXL | 2023 | U-Net LDM (larger) | 1024px | Dual encoders, refiner |
| SD 3 | 2024 | DiT (Transformer) | 1024px+ | MMDiT, flow matching |
| FLUX | 2024 | DiT | 1024px+ | Rectified flow transformer |

## Ecosystem
- **LoRA adapters**: Thousands of style/subject adapters on HF Hub
- **ControlNet**: Controllable generation (pose, depth, edges)
- **ComfyUI / Automatic1111**: Community UIs
- **Diffusers** (HF): Standard library for diffusion models

## Related Papers
- [[sources/latent-diffusion]] — Foundational LDM paper

## See Also
- [[concepts/diffusion-models]]
