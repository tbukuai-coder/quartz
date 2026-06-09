---
type: source
arxiv_id: "2510.02283"
title: "Self-Forcing++: Towards Minute-Scale High-Quality Video Generation"
authors: ["Justin Cui", "Jie Wu", "Ming Li", "Tao Yang"]
date: 2025-10-03
org: "Various"
tags: [video-generation, diffusion, autoregressive, long-form, 2025]
upvotes: 98
---

# Self-Forcing++

> Enables minute-scale long-horizon video generation by distilling from short bidirectional teachers using self-generated long videos as guidance — solving the extrapolation problem in autoregressive video.

## Key Contributions
- Solves the **extrapolation problem**: short-horizon teachers can't demonstrate long videos, so the student must learn from self-generated long sequences
- Achieves **minute-scale video generation** (60+ seconds) with maintained quality and temporal consistency
- **No additional supervision or retraining** of the teacher needed
- Uses **sampled segments from self-generated long videos** to guide the student model
- 254 GitHub ⭐, practical approach to long video

## Method
1. Generate long videos autoregressively using the student model itself
2. Sample high-quality segments from these self-generated videos
3. Use segments as training targets alongside teacher-distilled short videos
4. Handles quality degradation via position embedding tricks and temporal consistency losses

## Results
- 60+ second coherent video generation
- Maintains spatial quality comparable to short-video baselines
- Temporal consistency across long horizons
- Significantly outperforms naive autoregressive extrapolation

## Connections
- **Builds on**: [[sources/dit|DiT]], [[concepts/diffusion-models|Diffusion Models]]
- **Related**: [[sources/seedance|Seedance 1.0]], [[sources/cogvideox|CogVideoX]], [[sources/svd|SVD]]
- **Concept**: [[concepts/distillation|Distillation]] (teacher-student for video)

## Citation
> Cui et al., "Self-Forcing++: Towards Minute-Scale High-Quality Video Generation," arXiv:2510.02283, 2025.
