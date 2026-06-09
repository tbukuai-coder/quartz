---
type: source
arxiv_id: "2605.15178"
title: "SANA-WM: Efficient Minute-Scale World Modeling with Hybrid Linear Diffusion Transformer"
authors: ["Haoyi Zhu", "Haozhe Liu", "Yuyang Zhao", "Tian Ye", "Junsong Chen", "Jincheng Yu", "Tong He", "Song Han", "Enze Xie"]
date: 2026-05-15
org: "NVIDIA / HKU"
tags: [world-models, video-generation, linear-attention, camera-control, efficiency, 2026]
upvotes: 84
---

# SANA-WM: Efficient Minute-Scale World Modeling with Hybrid Linear Diffusion Transformer

> Efficient 2.6B-parameter open-source world model generating minute-scale 720p video with precise 6-DoF camera control via hybrid Gated DeltaNet + softmax attention, dual-camera branches, two-stage generation, and metric-scale pose supervision.

## Key Contributions
- **Hybrid Linear Attention**: combines frame-wise Gated DeltaNet (GDN) for efficient temporal modeling with softmax attention for spatial quality
- **Dual-camera branches**: separate processing for ego-motion and scene cameras with 6-DoF trajectory control
- **Two-stage generation pipeline**: coarse-then-fine approach for minute-scale coherent video
- **Metric-scale pose supervision**: enables precise camera control with real-world scale awareness
- **2.6B parameters** — efficient compared to industrial baselines (LingBot-World, HY-WorldPlay)
- Open-source with competitive industrial-level visual quality

## Method
SANA-WM uses a Hybrid Linear Diffusion Transformer that combines Gated DeltaNet (a linear-attention variant with gated updates) for efficient temporal context aggregation with standard softmax attention for high-quality spatial generation. Dual-camera branches handle ego-motion independently from scene rendering. A two-stage pipeline first generates coarse temporal structure, then refines to high-fidelity 720p. Metric-scale pose supervision from annotated data enables precise 6-DoF camera control.

## Results
- Minute-scale 720p video generation with precise camera control
- Visual quality comparable to large-scale industrial baselines
- Significantly more efficient (2.6B vs much larger industrial models)
- Supports NVFP4 quantization for deployment on Blackwell GPUs

## Connections
- Builds on: [[sources/gamma-world]], [[sources/seedance]], [[concepts/video-generation]], [[concepts/state-space-models]]
- Related: [[sources/longlive-2]], [[sources/stream-t1]], [[concepts/diffusion-models]]
- Architecture: hybrid linear attention + softmax — bridge between SSM and Transformer camps

## Citation
> Zhu et al., "SANA-WM: Efficient Minute-Scale World Modeling with Hybrid Linear Diffusion Transformer," arXiv:2605.15178, 2026.
