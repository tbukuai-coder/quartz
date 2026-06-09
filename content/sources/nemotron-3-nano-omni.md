---
type: source
arxiv_id: "2604.24954"
title: "Nemotron 3 Nano Omni: Efficient and Open Multimodal Intelligence"
authors: ["NVIDIA"]
date: 2026-04-12
org: "NVIDIA"
tags: [multimodal, omni-model, moe, efficiency, nvidia, 2026]
upvotes: 16
---

# Nemotron 3 Nano Omni: Efficient Open Multimodal Intelligence

> A 30B-A3B MoE omni-modal model with native audio, text, image, and video support, achieving 3× higher throughput than Qwen3-Omni and 9× higher per-GPU output token throughput on NVIDIA B200.

## Key Contributions

- **30B-A3B MoE backbone**: Replaces dense Nemotron Nano V2 12B with more efficient MoE architecture for long multimodal sequences
- **Native audio support**: Extends text/image/video to full omni-modal coverage
- **Dynamic image resolution**: Replaces tiling with aspect-ratio-preserving strategy
- **Temporal video compression**: Conv3D-based compression achieving 2× temporal token reduction
- **256K context length**: Extended from 128K for long-context multimodal reasoning
- **Multi-stage training**: Progressive modality introduction mitigates catastrophic forgetting

## Results

- **Throughput**: 3× higher single-stream output than Qwen3-Omni; 9× higher per-GPU at fixed interactivity target on B200
- **Document understanding**: Leading results on OCRBench-V2, MMLongBench-DOC
- **Audio-visual reasoning**: Top results on VoiceBench, WorldSense, DailyOmni
- **Cost efficiency**: Most cost-efficient open video understanding model on MediaPerf
- Released in BF16, FP8, and NVFP4 formats

## Connections
- Builds on: [[sources/nemotron-3-super]], [[sources/llama-nemotron]], [[concepts/multimodal-models]]
- Related entities: [[entities/orgs/nvidia]], [[entities/models/llama]]
- Related comparisons: [[comparisons/vision-language-models]], [[comparisons/moe-architectures]]
- Cited by / Influenced: Efficient omni-modal deployment

## Citation
> NVIDIA, "Nemotron 3 Nano Omni: Efficient and Open Multimodal Intelligence," arXiv:2604.24954, 2026.
