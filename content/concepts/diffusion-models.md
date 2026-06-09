---
type: concept
tags: [diffusion, image-generation]
---

# Diffusion Models

> A family of generative models that learn to **reverse a noise-adding process**, iteratively denoising random noise into structured outputs — the dominant paradigm for image generation.

## Overview
Diffusion models work by: (1) gradually adding noise to data until it becomes pure noise (forward process), then (2) learning to reverse this process, starting from noise and iteratively denoising to produce a sample (reverse process). Combined with latent space compression, this produces the best open image generation models.

## How It Works
### Forward Process (Adding Noise)
```
x₀ → x₁ → x₂ → ... → xT ≈ N(0, I)
```
Gradually add Gaussian noise over T steps until the image is pure noise.

### Reverse Process (Denoising)
```
xT → xT₋₁ → ... → x₁ → x₀
```
A neural network learns to predict and remove the noise at each step.

### Latent Diffusion ([[sources/latent-diffusion]])
Instead of operating on pixels, compress to a latent space first:
```
Image → Encoder → Latent → [Diffusion Process] → Latent → Decoder → Image
```
This reduces computation by 10–100× while maintaining quality.

## Key Architectures
| Architecture | Year | Method | Examples |
|---|---|---|---|
| **U-Net LDM** | 2022 | U-Net denoiser in latent space | SD 1.5, SDXL |
| **DiT** | 2023 | Transformer denoiser | SD 3, FLUX, Sora |
| **MMDiT** | 2024 | Multi-modal DiT | SD 3 |
| **Flow Matching** | 2024 | Rectified flow instead of DDPM | FLUX, SD 3 |

## Conditioning Mechanisms
- **Text conditioning**: CLIP/T5 text embeddings via cross-attention
- **ControlNet**: Spatial conditioning (pose, depth, edges)
- **IP-Adapter**: Image conditioning
- **Classifier-free guidance**: Trade diversity for fidelity

## Continuous-Time Distillation

[[sources/continuous-time-distribution-matching|Continuous-Time DMD (2026)]] migrates diffusion distillation from discrete to continuous optimization:
- Operates on arbitrary points along the PF-ODE trajectory instead of predefined timesteps
- Dynamic scheduling adapts timestep selection to training progress
- Velocity field extrapolation predicts denoising beyond observed timesteps
- Preserves fine visual details better than discrete-time DMD variants

This bridges Consistency Distillation (full trajectory self-consistency) and vanilla DMD (sparse discrete supervision), enabling more flexible and higher-fidelity few-step generation.

## Multi-Reward RL Fine-Tuning: MARBLE

[[sources/marble|MARBLE (2026)]] addresses a critical gap in diffusion model alignment — how to optimize multiple reward dimensions (aesthetic quality, text-image alignment, text rendering, compositional accuracy) **simultaneously** with a single model:

### The Specialist Sample Problem
Most generated samples are informative for only a subset of rewards:
- Cat image → strong aesthetic signal, no OCR signal
- Text rendering → strong OCR signal, average aesthetics

Weighted-sum aggregation $R(x) = \sum_k w_k R_k(x)$ dilutes informative dimensions. Gradient-level diagnosis: weighted-sum update is **anti-aligned with at least one reward's gradient in 80% of mini-batches**.

### MARBLE's Gradient-Space Harmonization
1. **Per-reward advantage decomposition**: Independent advantage $A_k(x)$ per reward
2. **Gradient normalization**: $\hat{g}_k = g_k / \|g_k\|$ removes scale disparities
3. **QP harmonization**: Solve $\alpha^* = \arg\min_{\alpha \in \Delta^K} \|\sum_k \alpha_k \hat{g}_k\|^2$ — minimum-norm point in convex hull of normalized gradients
4. **Rescaling**: $d_{\text{final}} = d^* \cdot \bar{n}$ restores natural update scale
5. **KL regularization**: Applied separately, outside harmonization

**Amortized variant**: Exploits DiffusionNFT's affine structure to pre-compute coefficients via EMA — reduces overhead from 0.56× to **0.97× speed** vs weighted-sum baseline.

### Results
- Jointly optimizes 5 rewards (PickScore, HPSv2, CLIPScore, OCR, GenEval) in single run
- Highest Composite score (+1.116), best on 4 held-out metrics
- Matches sequential multi-stage DiffusionNFT without manual curriculum design

## Video Background Replacement: Sparkle

[[sources/sparkle-video-bg-replacement|Sparkle (2026)]] advances video editing with **instruction-guided background replacement**:
- **Decoupled guidance**: Separate control paths for foreground preservation and background synthesis
- **Temporal consistency**: New backgrounds maintain coherent motion across frames
- Addresses the gap between style transfer (local editing) and full scene replacement (global synthesis)
- Scalable training data pipeline for background replacement pairs

## High-Resolution Image-to-Video: SwiftI2V

[[sources/swifti2v-highres|SwiftI2V (2026)]] tackles high-resolution (2K) image-to-video generation:
- **Segment-wise generation**: Parallel processing of video segments instead of end-to-end generation
- **Bidirectional context**: Forward and backward information exchange between segments
- Avoids the expense of end-to-end models and the hallucination of cascading super-resolution
- Preserves fine-grained input image details at scale

## Diffusion for Language Generation: Cola DLM

[[sources/cola-dlm|Cola DLM (2026)]] extends diffusion principles to **language modeling** via hierarchical latent-space decomposition:

### Architecture
1. **Text VAE** (500M): Encoder maps text → continuous latent; decoder reconstructs text from latent
2. **Block-Causal DiT** (1.8B): Models latent prior with Flow Matching; bidirectional within blocks, causal across blocks
3. **Conditional Decoder**: Generates text from prefix + generated latent blocks

### Key Innovation
Uses diffusion **not for token-level denoising** but for **latent prior transport** — global semantic organization in continuous space, local textual realization through decoder. This:
- Weakens fixed left-to-right inductive bias of autoregressive models
- Enables parallel generation within blocks
- Provides explicit global semantic modeling absent in token-level diffusion

### Critical Finding: The Likelihood-Generation Gap
Estimated perplexity is **poorly correlated with generation quality** for latent diffusion LMs. Flow Matching training naturally misaligns with conditional PPL. This implies PPL should not be the sole evaluation metric for non-autoregressive language models.

### Results
- ~2B parameters (strictly matched with AR and LLaDA baselines)
- Favorable scaling curves up to ~2000 EFLOPs
- Competitive on multiple benchmarks despite different inductive bias
- Preliminary evidence for extension to vision (cross-modal bridge)

## Diffusion for Autonomous Driving: ReflectDrive-2

[[sources/reflectdrive-2|ReflectDrive-2 (2026)]] applies **masked discrete diffusion** to autonomous driving trajectory planning:

### Decision–Draft–Reflect Pipeline
1. **Decision**: Goal-point posterior proposes behavior hypotheses (lane keeping, yielding, overtaking)
2. **Draft**: Masked discrete diffusion parallel-decodes trajectory tokens for each hypothesis
3. **Reflect**: AutoEdit rewrites trajectory tokens in-place via RL-coupled self-correction

### RL-Coupled AutoEdit
The key insight: simply adding a self-editing step on top of a trained drafter yields little (+0.3 PDMS). But when the **full draft-and-edit rollout is trained end-to-end with a single reward signal**, the drafter learns to emit revisable drafts and the editor learns corrections that improve closed-loop reward (+1.9 PDMS).

### Results
- **91.0 PDMS** on NAVSIM camera-only (best among camera-only VLA planners)
- **94.8 PDMS** under best-of-6 oracle selection (matches human reference)
- **31.8 ms/frame** on NVIDIA Thor with shared-prefix KV cache, ASD temporal refiner, and fused CUDA unmasking

## Key Papers
- [[sources/latent-diffusion]] — Latent Diffusion Models / Stable Diffusion
- [[sources/continuous-time-distribution-matching]] — Continuous-Time DMD for few-step distillation
- [[sources/marble]] — MARBLE: Multi-reward gradient harmonization for diffusion RL
- [[sources/sparkle-video-bg-replacement]] — Sparkle: Video background replacement with decoupled guidance
- [[sources/swifti2v-highres]] — SwiftI2V: High-resolution image-to-video via segment-wise generation
- [[sources/cola-dlm]] — Cola DLM: Continuous latent diffusion language model
- [[sources/reflectdrive-2]] — ReflectDrive-2: RL-aligned self-editing for masked diffusion driving planners

## See Also
- [[entities/models/stable-diffusion]]
- [[concepts/transformer-architecture]]
- [[concepts/video-generation]]
