---
type: source
arxiv_id: "2506.09113"
title: "Seedance 1.0: Exploring the Boundaries of Video Generation Models"
authors: ["Yu Gao", "Haoyuan Guo", "Various"]
date: 2025-06-11
org: "ByteDance / Various"
tags: [video-generation, diffusion, multimodal, 2025]
upvotes: 108
---

# Seedance 1.0

> State-of-the-art video generation model combining multi-source data curation, efficient diffusion architecture, video-specific RLHF, and multi-stage distillation for high-quality text/image-to-video generation.

## Key Contributions
- **Multi-source data curation** with precision video captioning for high-quality training data
- **Efficient architecture** combining diffusion transformers with training paradigm innovations
- **Video-specific RLHF** using multi-dimensional reward mechanisms (temporal, visual, semantic)
- **Multi-shot generation** with consistent subject representation across shots
- **Multi-stage distillation** for inference acceleration while maintaining quality
- Achieves SOTA on video generation quality, motion plausibility, and prompt adherence

## Method
Full-stack video generation system:
1. **Data**: Multi-source curation with automated captioning pipeline for precise, meaningful descriptions
2. **Architecture**: Diffusion transformer backbone optimized for spatiotemporal generation
3. **Training**: Progressive resolution/duration training + fine-grained SFT
4. **Post-training**: Video-specific RLHF with rewards for fluidity, structural stability, instruction adherence
5. **Acceleration**: Multi-stage distillation for practical inference speeds

## Results
- SOTA on text-to-video quality metrics
- Strong image-to-video animation with high fidelity
- Multi-shot narrative coherence — consistent characters across video segments
- Practical inference speed via distillation

## Connections
- **Builds on**: [[sources/sd3|SD3/Rectified Flow]], [[sources/dit|DiT]], [[concepts/rectified-flow|Rectified Flow]]
- **Related**: [[sources/cogvideox|CogVideoX]], [[sources/svd|Stable Video Diffusion]]
- **Concepts**: [[concepts/diffusion-models|Diffusion Models]], [[concepts/rlhf|RLHF]] (video-specific)
- **Comparison**: [[comparisons/diffusion-architectures|Diffusion Architectures]]

## Citation
> Gao et al., "Seedance 1.0: Exploring the Boundaries of Video Generation Models," arXiv:2506.09113, 2025.
