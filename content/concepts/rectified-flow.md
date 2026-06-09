---
type: concept
tags: [diffusion, generation, training]
---

# Rectified Flow / Flow Matching

> A generative modeling framework that learns **straight-line paths** from noise to data — replacing complex diffusion noise schedules with simple linear interpolation. Rectified flow enables **fewer sampling steps** and **better training dynamics** than standard diffusion, and has become the foundation for modern image generators (SD3, FLUX).

## Overview
Rectified flow (also called flow matching) is an alternative to standard diffusion models. Instead of gradually adding and removing Gaussian noise via a fixed schedule (DDPM), rectified flow learns a velocity field that transforms noise into data along approximately straight paths. This simplification leads to faster sampling and more stable training.

## How It Works

### Standard Diffusion (DDPM)
```
Forward:  x_t = √(α_t) · x_0 + √(1-α_t) · ε    (curved noise schedule)
Reverse:  Predict ε from x_t → iteratively denoise (many steps needed)
```

### Rectified Flow
```
Forward:  z_t = (1-t) · x_0 + t · ε                (straight line)
Model:    Predict velocity v = ε - x_0              (direction of flow)
Reverse:  Follow ODE: dz/dt = v(z_t, t)            (fewer steps needed)
```

The straight-line interpolation means the model only needs to learn a simple velocity field, not a complex noise-conditioned denoiser.

### Reflow (Straightening)
The **rectification** procedure ([[sources/rectified-flow|original paper]]) iteratively retrains on the flow's own couplings, provably reducing transport costs and straightening trajectories. After 1–2 reflow iterations, the paths become nearly straight enough for **single-step generation**.

### Key Advantages
| Feature | Standard Diffusion | Rectified Flow |
|---|---|---|
| Noise schedule | Complex (cosine, linear) | Simple (linear interpolation) |
| Sampling steps | 20–50 typically | 4–8 sufficient |
| Training target | Noise prediction (ε) | Velocity prediction (v) |
| ODE solver | DDIM, DPM-Solver | Euler (simplest) |
| Loss weighting | Requires careful tuning | Naturally balanced |

## Key Papers
- [[sources/rectified-flow]] — **Original paper**: Flow Straight and Fast (Liu et al., 2022) — introduced rectified flow, reflow, and one-step generation
- [[sources/sd3]] — Scaling Rectified Flow Transformers for High-Resolution Image Synthesis (SD3/FLUX foundation)
- [[sources/dit]] — DiT: Diffusion Transformers (backbone architecture)
- [[sources/latent-diffusion]] — Latent Diffusion Models (operates in latent space)

## Models Using Rectified Flow
- **Stable Diffusion 3** ([[sources/sd3]]): MMDiT + rectified flow
- **FLUX** (Black Forest Labs): Rectified flow + DiT architecture
- **Sora** (OpenAI): Believed to use flow matching for video generation

## See Also
- [[concepts/diffusion-models]] — Standard diffusion models
- [[sources/sdxl]] — SDXL (predecessor using standard diffusion)
- [[comparisons/diffusion-architectures]] — U-Net vs DiT vs MMDiT
