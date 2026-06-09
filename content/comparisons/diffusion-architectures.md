---
type: comparison
tags: [diffusion, architecture, image-generation, synthesis]
---

# Comparison: Diffusion Architectures — U-Net vs DiT vs MMDiT

> The backbone revolution in image generation: from **U-Net** (Stable Diffusion 1–2, DALL-E 2) to **DiT** (Diffusion Transformers) to **MMDiT** (Stable Diffusion 3, FLUX). Each generation brought better scaling, quality, and text alignment.

## Overview

Diffusion models generate images by iteratively denoising random noise. The **backbone architecture** — the neural network that predicts how to denoise — has evolved through three generations, each unlocking significant quality improvements and new capabilities.

## Architecture Comparison

| Feature | U-Net | DiT | MMDiT |
|---|---|---|---|
| **Era** | 2020–2023 | 2022–2024 | 2024+ |
| **Used by** | SD 1.x, SD 2.x, SDXL, DALL-E 2 | Early DiT research | SD3, FLUX, Sora |
| **Core op** | Conv + cross-attention | Self-attention on patches | Joint attention (text+image) |
| **Scaling** | Difficult (conv layers) | Predictable (more FLOPs = better) | Predictable + better alignment |
| **Text conditioning** | Cross-attention to CLIP | AdaLN-Zero (class labels) | Joint attention to T5+CLIP |
| **Text rendering** | Poor | N/A (class-conditional) | Good (T5 encoder) |
| **Resolution** | Fixed (generate at target) | Patch-based (flexible) | Patch-based (flexible) |
| **FLOP efficiency** | Lower | Higher | Highest |
| **Noise formulation** | DDPM/DDIM | DDPM/DDIM | **Rectified flow** |

## Timeline & Key Models

| Year | Model | Architecture | Key Advance |
|---|---|---|---|
| 2021 | [[sources/latent-diffusion\|Latent Diffusion]] | U-Net | Diffusion in latent space (not pixels) |
| 2022 | DALL-E 2 | U-Net | CLIP-guided generation |
| 2022 | [[sources/dit\|DiT]] | DiT | Transformer replaces U-Net for diffusion |
| 2023 | [[sources/sdxl\|SDXL]] | U-Net (large) | Peak U-Net quality, dual text encoders |
| 2024 | [[sources/sd3\|SD3]] | MMDiT | Rectified flow + joint text-image attention |
| 2024 | FLUX | MMDiT variant | SOTA open text-to-image (by SD3 authors) |
| 2024 | Sora | DiT (3D) | Video generation with spatial-temporal DiT |
| 2026 | [[sources/continuous-time-distribution-matching\|Continuous-Time DMD]] | Any (distillation) | Few-step distillation in continuous time |
| 2026 | [[sources/sparkle-video-bg-replacement\|Sparkle]] | DiT/MMDiT | Video background replacement with decoupled guidance |
| 2026 | [[sources/swifti2v-highres\|SwiftI2V]] | DiT | High-resolution image-to-video via segment-wise generation |
| 2026 | [[sources/marble\|MARBLE]] | Any (RL fine-tuning) | Multi-reward gradient harmonization for diffusion RL |
| 2026 | [[sources/stream-t1\|Stream-T1]] | DiT (video) | Active test-time scaling for streaming video generation |
| 2026 | [[sources/cola-dlm\|Cola DLM]] | DiT (latent language) | Block-causal DiT prior for continuous latent text generation |
| 2026 | [[sources/reflectdrive-2\|ReflectDrive-2]] | Masked discrete diffusion (driving) | Masked discrete diffusion for autonomous driving trajectory planning |

## Key Insights

### 1. Transformers Scale Better Than U-Nets
DiT showed a clear scaling law: doubling GFLOPs consistently halves FID. U-Nets don't scale as predictably — adding more conv layers hits diminishing returns faster.

### 2. Joint Attention > Cross-Attention for Text Alignment
- **U-Net**: Text features are injected via cross-attention → text and image attend to each other asymmetrically
- **MMDiT**: Text and image tokens are **both in the same attention** → bidirectional information flow → much better text rendering and complex prompt following

### 3. Rectified Flow > DDPM
- [[concepts/rectified-flow|Rectified flow]]: Straight-line paths from noise to data → fewer sampling steps (4–8 vs 20–50)
- Simpler training objective (velocity prediction vs noise prediction)
- Better for distillation (straighter paths are easier to approximate)

### 4. The U-Net Isn't Dead (Yet)
U-Net still has advantages for:
- **Inpainting/outpainting**: Spatial structure from skip connections
- **ControlNet**: Architectural conditioning works well with U-Net skip connections
- **Efficiency at small scale**: U-Net can be smaller and faster for low-resolution generation
- **Existing ecosystem**: Many fine-tuned models, LoRAs, and tools built for U-Net SD

## Continuous-Time Distillation (2026)

[[sources/continuous-time-distribution-matching|Continuous-Time DMD (2026)]] advances distillation beyond discrete timesteps:

| Approach | Timestep Sampling | Key Limitation |
|---|---|---|
| Consistency Distillation | Full trajectory | Enforces self-consistency everywhere; rigid |
| Vanilla DMD | Sparse discrete points | Misses intermediate dynamics; restricted |
| **Continuous-Time DMD** | **Arbitrary trajectory points** | Flexible scheduling + velocity extrapolation |

- Operates on arbitrary points along the PF-ODE trajectory instead of predefined timesteps
- Dynamic scheduling adapts timestep selection to training progress
- Velocity field extrapolation predicts denoising beyond observed timesteps
- Preserves fine visual details better than discrete-time DMD variants

This is particularly relevant for few-step generation (4–8 steps) where timestep coverage is sparse.

## Multi-Reward RL Fine-Tuning: MARBLE (2026)

[[sources/marble|MARBLE (2026)]] introduces a principled framework for optimizing diffusion models across multiple reward dimensions simultaneously — a problem that was previously addressed with manual multi-stage schedules or separate specialist models:

### The Specialist Sample Problem
Most generated samples are informative for only a subset of rewards:
- Landscape image → strong aesthetic signal, no OCR signal
- Text rendering → strong OCR signal, average aesthetics
- Product photo → strong compositional signal, variable aesthetics

Weighted-sum aggregation $R(x) = \sum_k w_k R_k(x)$ dilutes informative dimensions. **80% of mini-batches show anti-aligned gradients** — the weighted-sum update actively pushes against at least one reward.

### MARBLE's Gradient-Space Harmonization
1. **Per-reward decomposition**: Independent advantage $A_k(x)$ per reward
2. **Gradient normalization**: $\hat{g}_k = g_k / \|g_k\|$ — removes scale disparities
3. **QP harmonization**: $\alpha^* = \arg\min_{\alpha \in \Delta^K} \|\sum_k \alpha_k \hat{g}_k\|^2$ — finds minimum-norm point in convex hull
4. **Rescaling**: $d_{\text{final}} = d^* \cdot \bar{n}$ — restores natural update scale
5. **Amortization**: Pre-computes coefficients via EMA — **0.97× speed** vs weighted-sum baseline

### Results
MARBLE jointly optimizes 5 rewards (PickScore, HPSv2, CLIPScore, OCR, GenEval) in a single training run, achieving **highest Composite score (+1.116)** and ranking first on 4 held-out quality metrics. This matches sequential multi-stage DiffusionNFT without manual curriculum design.

| Approach | GenEval | OCR | Aesthetic | Composite |
|---|---|---|---|---|
| SD3.5-M + CFG | 0.63 | 0.59 | 5.36 | -0.255 |
| + DiffusionNFT † (sequential) | 0.94 | 0.91 | 6.01 | +1.015 |
| **+ MARBLE** | **0.94** | **0.96** | **6.59** | **+1.116** |

Sequential multi-stage DiffusionNFT achieves comparable quality but requires manually scheduled curriculum (800 steps reward 1 → 300 steps reward 2 → 200 steps reward 1 → ...). MARBLE eliminates this hyperparameter search.

## Diffusion for Language Generation: Cola DLM (2026)

[[sources/cola-dlm|Cola DLM (2026)]] extends diffusion principles to **language modeling** via a hierarchical latent-space architecture:

- **Text VAE** (500M): Maps text ↔ continuous latent space with strict causal encoder/decoder
- **Block-Causal DiT** (1.8B): Models latent prior with Flow Matching; bidirectional within blocks, causal across blocks
- **Key innovation**: Uses diffusion **for latent prior transport** (not token-level denoising) — global semantic organization in continuous space, local textual realization through decoder

This weakens the fixed left-to-right inductive bias of autoregressive models and enables parallel generation within blocks. A critical finding: **estimated perplexity is poorly correlated with generation quality** for latent diffusion LMs — PPL should not be the sole evaluation metric for non-autoregressive language models.

## Diffusion for Autonomous Driving: ReflectDrive-2 (2026)

[[sources/reflectdrive-2|ReflectDrive-2 (2026)]] applies **masked discrete diffusion** to autonomous driving trajectory planning through a **decision–draft–reflect** pipeline:

1. **Decision**: Goal-point posterior proposes behavior hypotheses (lane keeping, yielding, overtaking)
2. **Draft**: Masked discrete diffusion parallel-decodes 16 trajectory tokens (8 waypoints) for each hypothesis
3. **Reflect**: AutoEdit rewrites trajectory tokens in-place, co-trained via RL over the full draft-and-edit rollout

The RL coupling is critical: before RL, inference-time AutoEdit adds +0.3 PDMS; after RL co-training, the same AutoEdit adds +1.9 PDMS — the drafter learns to emit revisable drafts and the editor learns corrections that improve closed-loop reward.

**Result**: **91.0 PDMS** on NAVSIM camera-only, surpassing all camera-only VLA peers (89.1–90.8). Best-of-6 oracle selection reaches **94.8 PDMS** (matching human reference).

## Video Generation Extensions (2026)

### Sparkle: Background Replacement
[[sources/sparkle-video-bg-replacement|Sparkle]] applies diffusion transformers to **instruction-guided video background replacement**:
- **Decoupled guidance**: Separate control paths for foreground preservation and background synthesis
- Requires temporal consistency across frames while synthesizing entirely new scenes
- Scalable data synthesis pipeline for training background replacement pairs

### SwiftI2V: High-Resolution Image-to-Video
[[sources/swifti2v-highres|SwiftI2V]] tackles 2K-resolution image-to-video:
- **Segment-wise generation**: Breaks video into segments for parallel processing (avoids end-to-end expense)
- **Bidirectional context**: Forward/backward information exchange between segments maintains global coherence
- Avoids cascading super-resolution hallucination

### Stream-T1: Active Test-Time Scaling
[[sources/stream-t1|Stream-T1 (2026)]] pioneers **active TTS for streaming video generation**:
- Chunk-level synthesis (4 denoising steps per chunk) with active noise propagation, reward pruning, and memory sinking
- Stream-Scaled Noise Propagation: Spherical interpolation with historical proven trajectories
- Stream-Scaled Reward Pruning: Dual-level evaluation (image rewards for spatial + video rewards for temporal)
- Stream-Scaled Memory Sinking: Three KV-cache eviction pathways (Discard/EMA-Sink/Append-Sink) guided by semantic boundaries

## Key Papers
- [[sources/latent-diffusion]] — Latent Diffusion Models (U-Net in latent space)
- [[sources/sdxl]] — SDXL (peak U-Net architecture)
- [[sources/dit]] — DiT: Diffusion Transformers
- [[sources/sd3]] — SD3: MMDiT + Rectified Flow
- [[sources/cogvideox]] — CogVideoX (3D DiT for video)
- [[sources/continuous-time-distribution-matching]] — Continuous-Time DMD for few-step distillation
- [[sources/marble]] — MARBLE: Multi-reward gradient harmonization for diffusion RL
- [[sources/sparkle-video-bg-replacement]] — Sparkle: Video background replacement
- [[sources/swifti2v-highres]] — SwiftI2V: High-resolution image-to-video
- [[sources/stream-t1]] — Stream-T1: Active test-time scaling for streaming video
- [[sources/cola-dlm]] — Cola DLM: Continuous latent diffusion language model
- [[sources/reflectdrive-2]] — ReflectDrive-2: RL-aligned self-editing for masked diffusion driving planners
- [[sources/clip]] — CLIP (text encoder backbone)
- [[sources/siglip]] — SigLIP (improved vision-language pretraining)

## See Also
- [[concepts/diffusion-models]] — Diffusion model fundamentals
- [[concepts/rectified-flow]] — Rectified Flow / Flow Matching
- [[concepts/transformer-architecture]] — Transformer fundamentals
- [[concepts/video-generation]] — Video generation techniques
- [[entities/models/stable-diffusion]] — Stable Diffusion model family
