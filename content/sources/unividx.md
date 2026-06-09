---
type: source
arxiv_id: "2605.00658"
title: "UniVidX: A Unified Multimodal Framework for Versatile Video Generation via Diffusion Priors"
authors: ["Houyuan Chen", "Hong Li", "Xianghao Kong", "Tianrui Zhu", "Shaocong Xu", "Weiqing Xiao", "Yuwei Guo", "Chongjie Ye", "Lvmin Zhang", "Hao Zhao"]
date: 2026-05-02
org: "Tsinghua University"
tags: [video-generation, diffusion, multimodal, conditional-generation, 2026]
upvotes: 62
---

# UniVidX: Unified Multimodal Framework for Versatile Video Generation via Diffusion Priors

> A unified multimodal framework that leverages video diffusion model priors for versatile video generation across diverse visual modalities using stochastic condition masking, decoupled gated LoRA, and cross-modal self-attention.

## Key Contributions

- **UniVidX framework**: Unified formulation that treats pixel-aligned tasks as conditional generation in a shared multimodal space
- **Stochastic Condition Masking (SCM)**: Randomly partitions modalities into clean conditions and noisy targets, enabling omni-directional generation
- **Decoupled Gated LoRA (DGL)**: Assigns independent LoRAs to each modality, activated only when that modality is a generation target, preventing parameter interference
- **Cross-Modal Self-Attention (CMSA)**: Keys and values shared across modalities while queries remain modality-specific, ensuring cross-modal consistency

## Method

Existing methods train separate models for each problem setting (e.g., RGB→alpha, intrinsic→X), which locks each model into a fixed role and ignores correlations across visual modalities. UniVidX overcomes this by:

1. Formulating diverse multimodal graphics tasks as conditional generation in a shared space
2. Training a single T2V backbone to uniformly process pure text, visual, and hybrid inputs
3. Supporting three paradigms: Text→X, X→X, and Text&X→X

Two instantiations: **UniVid-Intrinsic** (RGB videos + intrinsic maps) and **UniVid-Alpha** (BL, alpha matte, foreground, background layers).

## Results

- Both models achieve SOTA performance across 15 distinct tasks
- Remarkable data efficiency: robust generalization to out-of-distribution, in-the-wild scenarios despite training on <1k videos
- Covers tasks including text-to-intrinsic, inverse rendering, video relighting, text-to-RGBA, video matting, video inpainting

## Connections
- Builds on: [[sources/seedance]], [[sources/cogvideox]], [[sources/svd]], [[concepts/diffusion-models]], [[sources/rectified-flow]]
- Related concepts: [[concepts/video-generation]], [[concepts/lora-peft]], [[concepts/self-attention]]
- Cited by / Influenced: Emerging work on unified multimodal generation

## Citation
> Chen et al., "UniVidX: A Unified Multimodal Framework for Versatile Video Generation via Diffusion Priors," arXiv:2605.00658, 2026.
