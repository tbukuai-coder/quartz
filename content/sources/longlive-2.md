---
type: source
arxiv_id: "2605.18739"
title: "LongLive-2.0: An NVFP4 Parallel Infrastructure for Long Video Generation"
authors: ["Yukang Chen", "Luozhou Wang", "Wei Huang", "Shuai Yang", "Bohan Zhang", "Yicheng Xiao", "Ruihang Chu", "Weian Mao", "Qixin Hu", "Shaoteng Liu"]
date: 2026-05-19
org: "NVIDIA"
tags: [video-generation, infrastructure, quantization, nvfp4, parallel-training, 2026]
upvotes: 112
---

# LongLive-2.0: An NVFP4 Parallel Infrastructure for Long Video Generation

> NVFP4-based parallel infrastructure for minute-scale video generation addressing speed and memory bottlenecks via Balanced SP (sequence-parallel AR training), W4A4 quantized LoRA, asynchronous streaming VAE decoding, and KV cache quantization on Blackwell GPUs.

## Key Contributions
- **Balanced SP (Sequence-Parallel AR Training)**: co-designs teacher-forcing layout with SP execution by pairing clean-history and noisy-target temporal chunks on each GPU rank
- **NVFP4 quantized training**: W4A4 LoRA weights for memory-efficient diffusion model tuning
- **Asynchronous streaming VAE decoding**: overlaps VAE decode with generation for reduced latency
- **KV cache quantization**: enables longer sequences within GPU memory constraints
- **2,166 GitHub stars** — strong community adoption
- Full NVFP4 pipeline from training through inference on Blackwell GPUs

## Method
LongLive-2.0 addresses the full training-to-inference pipeline for long video generation. For training, Balanced SP distributes autoregressive diffusion training across GPUs by pairing clean-history chunks with noisy-target chunks on each rank, enabling efficient teacher-forcing with sequence parallelism. NVFP4 (4-bit) quantization is applied to LoRA weights during training (W4A4). For inference, KV cache quantization and asynchronous streaming VAE decoding reduce memory and latency for minute-scale generation.

## Results
- Minute-scale video generation with high fidelity
- Significant memory reduction via NVFP4 quantization throughout the pipeline
- Scales to Blackwell GPU clusters with reduced inter-GPU communication
- Achieves practical deployment speeds for long video generation

## Connections
- Builds on: [[sources/seedance]], [[sources/stream-t1]], [[sources/quartet]], [[concepts/video-generation]]
- Related: [[sources/gamma-world]], [[sources/self-forcing-pp]], [[concepts/mixed-precision-training]]
- Organization: [[entities/orgs/nvidia]]

## Citation
> Chen et al., "LongLive-2.0: An NVFP4 Parallel Infrastructure for Long Video Generation," arXiv:2605.18739, 2026.
