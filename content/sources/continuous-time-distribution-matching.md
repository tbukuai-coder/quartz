---
type: source
arxiv_id: "2605.06376"
title: "Continuous-Time Distribution Matching for Few-Step Diffusion Distillation"
authors: ["Tao Liu", "Hao Yan", "Mengting Chen", "Taihang Hu", "Zhengrong Yue", "Zihao Pan", "Jinsong Lan", "Xiaoyong Zhu", "Ming-Ming Cheng", "Bo Zheng"]
date: 2026-05
tags: [diffusion-models, distillation, consistency-distillation, continuous-time, image-generation, velocity-field]
upvotes: 17
---

# Continuous-Time Distribution Matching for Few-Step Diffusion Distillation

> Migrates diffusion model distillation from discrete to continuous optimization, enabling arbitrary points along sampling trajectories and preserving fine visual details through dynamic scheduling and velocity field extrapolation.

## Key Contributions
- Proposes continuous-time Distribution Matching Distillation (DMD) that operates on arbitrary points along the PF-ODE trajectory instead of predefined discrete timesteps
- Introduces dynamic scheduling and velocity field extrapolation for preserving fine visual details
- Bridges the gap between Consistency Distillation (which enforces self-consistency along the full trajectory) and vanilla DMD (which uses sparse discrete supervision)
- Achieves few-step generation with higher fidelity than discrete-time alternatives

## Method
The approach reformulates Distribution Matching Distillation in continuous time:
1. **Continuous trajectory sampling**: Instead of sampling at fixed discrete timesteps, the method can evaluate loss at any point along the probability flow ODE trajectory
2. **Dynamic scheduling**: Adaptive timestep selection based on training progress
3. **Velocity field extrapolation**: Predicts denoising velocity beyond observed timesteps for better generalization
4. The continuous formulation preserves the mode-seeking nature of reverse KL divergence while removing the timestep quantization bottleneck

## Results
- Enables arbitrary points along sampling trajectories for distillation
- Preserves fine visual details better than discrete-time DMD variants
- Competitive with Consistency Distillation on image generation benchmarks while offering more flexible training

## Datasets Used
- Standard image generation benchmarks (likely ImageNet, COCO)

## Models Released
- Code available at https://github.com/byliutao/cdm

## Connections
- Builds on: [[sources/dit]] — Diffusion Transformer architecture
- Related: [[sources/seedance]], [[sources/self-forcing-pp]] — video generation distillation
- Related concept: [[concepts/diffusion-models]], [[concepts/distillation]]

## Citation
> Liu et al., "Continuous-Time Distribution Matching for Few-Step Diffusion Distillation," arXiv:2605.06376, 2026.
