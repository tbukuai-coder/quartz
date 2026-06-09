---
type: source
arxiv_id: "2605.15141"
title: "Causal Forcing++: Scalable Few-Step Autoregressive Diffusion Distillation for Real-Time Interactive Video Generation"
authors: ["Min Zhao", "Hongzhou Zhu", "Kaiwen Zheng", "Zihan Zhou", "Bokai Yan", "Xinyuan Li", "Xiao Yang", "Chongxuan Li", "Jun Zhu"]
date: 2026-05-15
org: "Tsinghua University"
tags: [video-generation, diffusion, distillation, real-time, interactive, 2026]
upvotes: 92
---

# Causal Forcing++: Scalable Few-Step Autoregressive Diffusion Distillation for Real-Time Interactive Video Generation

> Frame-wise autoregression with 1-2 sampling steps via causal consistency distillation — enables real-time interactive video generation with low latency and streaming controllability, advancing from chunk-wise to single-frame granularity.

## Key Contributions
- **Causal Consistency Distillation (Causal CD)**: distills bidirectional base models into causal few-step AR students that generate one frame at a time
- **Frame-wise autoregression**: pushes from chunk-wise (4-frame) to single-frame granularity for minimal latency
- **Few-step AR initialization**: warm-starts the causal student for stable training in the aggressive 1-2 step regime
- **Real-time interactive generation**: enables action-responsive video generation at low latency
- Strong performance on VBench and VisionReward benchmarks

## Method
Existing AR diffusion distillation methods work at chunk level (4 frames per generation step). Causal Forcing++ pushes to the extreme: frame-wise autoregression with only 1-2 denoising steps per frame. This is achieved by: (1) Causal CD — a causal variant of consistency distillation that maintains temporal coherence; (2) Few-step AR initialization that provides a stable starting point for the aggressive training regime. The result is a real-time interactive generator with sub-frame latency.

## Results
- Real-time video generation at frame-level granularity
- Strong performance on VBench quality and VisionReward alignment metrics
- Enables interactive world model applications (games, simulations)
- Compatible with Genie3-style world model generation

## Connections
- Builds on: [[sources/self-forcing-pp]], [[sources/continuous-time-distribution-matching]], [[concepts/diffusion-models]]
- Related: [[sources/gamma-world]], [[sources/anyflow]], [[sources/stream-t1]], [[concepts/video-generation]]
- Enables: real-time interactive world models, gaming applications

## Citation
> Zhao et al., "Causal Forcing++: Scalable Few-Step Autoregressive Diffusion Distillation for Real-Time Interactive Video Generation," arXiv:2605.15141, 2026.
