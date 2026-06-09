---
type: source
arxiv_id: "2605.06356"
title: "SwiftI2V: Efficient High-Resolution Image-to-Video Generation via Conditional Segment-wise Generation"
authors: ["YaoYang Liu", "Yuechen Zhang", "Wenbo Li", "Yufei Zhao", "Rui Liu", "Long Chen"]
date: 2026-05
tags: [video-generation, image-to-video, high-resolution, conditional-generation, diffusion-transformer]
upvotes: 5
---

# SwiftI2V: Efficient High-Resolution Image-to-Video Generation via Conditional Segment-wise Generation

> An efficient high-resolution image-to-video generation framework using conditional segment-wise generation and bidirectional contextual interaction for scalable, input-faithful video synthesis with reduced computational requirements.

## Key Contributions
- Addresses the challenge of high-resolution (2K) image-to-video (I2V) generation
- Proposes conditional segment-wise generation that breaks the video into segments for parallel processing
- Introduces bidirectional contextual interaction to maintain cross-segment coherence
- Reduces token budget compared to end-to-end models while avoiding hallucination from cascading low-resolution generation
- Achieves scalable, input-faithful video synthesis

## Method
SwiftI2V uses a segment-wise approach:
1. **Conditional segment-wise generation**: The video is divided into segments, each generated conditionally on the input image and neighboring segments
2. **Bidirectional contextual interaction**: Information flows both forward and backward between segments to maintain global coherence
3. **Token budget management**: Efficient allocation of computational tokens across segments
4. **Cross-segment coherence**: Ensures temporal and visual consistency between adjacent video segments

This avoids two common pitfalls:
- End-to-end models that are prohibitively expensive at 2K resolution
- Cascading low-res → super-resolution approaches that hallucinate details and drift from input structure

## Results
- High-resolution (up to 2K) image-to-video generation
- Input-faithful synthesis preserving fine-grained appearance details
- Reduced computational requirements compared to end-to-end approaches

## Datasets Used
- Standard image-to-video generation benchmarks

## Models Released
- GitHub: https://github.com/HKUST-LongGroup/SwiftI2V (2 stars)

## Connections
- Related: [[sources/seedance]] — SOTA video generation
- Related: [[sources/cogvideox]] — open text-to-video generation
- Related: [[sources/unividx]] — unified multimodal video generation
- Related concept: [[concepts/video-generation]], [[concepts/diffusion-models]]

## Citation
> Liu et al., "SwiftI2V: Efficient High-Resolution Image-to-Video Generation via Conditional Segment-wise Generation," arXiv:2605.06356, 2026.
