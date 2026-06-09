---
type: source
arxiv_id: "2412.18653"
title: "1.58-bit FLUX"
authors: ["Chenglin Yang", "Xueqing Deng", "Dongwon Kim", "Xiaoxing Wang"]
date: 2024-12-24
org: "Various"
tags: [quantization, diffusion, image-generation, efficiency, 2024]
upvotes: 86
---

# 1.58-bit FLUX

> Extreme quantization of the FLUX.1-dev text-to-image model to 1.58-bit (ternary) weights while maintaining comparable generation quality, demonstrating that diffusion transformers are highly compressible.

## Key Contributions
- Quantized FLUX.1-dev to 1.58-bit (ternary: {-1, 0, 1}) — most aggressive quantization of a large image gen model
- Maintained comparable generation quality on GenEval and T2I-CompBench benchmarks
- Used self-supervised quantization: model generates its own training signals
- Developed custom kernels for efficient ternary inference
- Demonstrated DiT/MMDiT architectures are remarkably robust to extreme quantization

## Method
1. Ternary weight mapping with learned per-group scale factors
2. Self-supervised fine-tuning from full-precision model outputs
3. Custom ternary inference kernels (additions/subtractions only, no multiplication)
4. Selective precision for critical layers

## Results
- GenEval: 0.71 (1.58-bit) vs 0.73 (full precision) — minimal quality loss
- Model size: ~6x reduction (~2.3GB vs 24GB+)
- T2I-CompBench: Comparable across all metrics

## Connections
- Quantizes FLUX.1-dev (built on [[sources/sd3|SD3/Rectified Flow]])
- Related: [[concepts/post-training-quantization|PTQ]], [[concepts/quantization|Quantization]]
- Demonstrates DiT architectures ([[sources/dit|DiT]]) robust to extreme compression

## Citation
> Yang et al., "1.58-bit FLUX," arXiv:2412.18653, 2024.
