---
type: source
arxiv_id: "2605.13724"
title: "AnyFlow: Any-Step Video Diffusion Model with On-Policy Flow Map Distillation"
authors: ["Yuchao Gu", "Guian Fang", "Yuxin Jiang", "Weijia Mao", "Song Han", "Han Cai", "Mike Zheng Shou"]
date: 2026-05-14
org: "NVIDIA / NUS"
tags: [video-generation, diffusion, distillation, flow-matching, 2026]
upvotes: 101
---

# AnyFlow: Any-Step Video Diffusion Model with On-Policy Flow Map Distillation

> Any-step video diffusion distillation that improves upon consistency distillation by optimizing full ODE sampling trajectories via flow-map transition learning and backward simulation, maintaining quality at any step count (1-step to many-step).

## Key Contributions
- **Flow-map transition learning**: learns transition maps between arbitrary time points on the ODE trajectory, enabling flexible step counts at inference
- **Backward simulation**: corrects accumulated discretization error via backward ODE integration from the student's generated samples
- **On-policy distillation**: trains on the student's own trajectory distribution rather than teacher's, eliminating exposure bias
- **Any-step flexibility**: unlike consistency distillation which degrades with more steps, AnyFlow maintains quality across all step counts
- **354 GitHub stars** at NVIDIA/NVlabs

## Method
Consistency distillation maps noisy inputs directly to the clean endpoint, which breaks the original ODE structure and degrades when more steps are used. AnyFlow instead learns flow maps — transitions between arbitrary pairs of timepoints on the probability-flow ODE. Training uses on-policy distillation: the student generates samples from its own distribution, then backward simulation provides supervision by integrating back along the ODE. This preserves the ODE trajectory structure, enabling test-time scaling (more steps = better quality).

## Results
- Superior quality at 1-step, 2-step, and multi-step generation compared to consistency distillation
- Maintains desirable test-time scaling (more steps improve quality) unlike consistency models
- State-of-the-art video generation quality across step budgets

## Connections
- Builds on: [[sources/continuous-time-distribution-matching]], [[sources/self-forcing-pp]], [[concepts/diffusion-models]]
- Related: [[sources/longlive-2]], [[sources/gamma-world]], [[concepts/distillation]], [[concepts/rectified-flow]]
- Organization: [[entities/orgs/nvidia]]

## Citation
> Gu et al., "AnyFlow: Any-Step Video Diffusion Model with On-Policy Flow Map Distillation," arXiv:2605.13724, 2026.
