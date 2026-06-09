---
type: source
arxiv_id: "2605.27365"
title: "LocateAnything: Fast and High-Quality Vision-Language Grounding with Parallel Box Decoding"
authors: ["Shihao Wang", "Shilong Liu", "Yuanguo Kuang", "Xinyu Wei", "Yangzhou Liu", "Zhiqi Li", "Yunze Man", "Guo Chen", "Andrew Tao", "Guilin Liu"]
date: 2026-05-27
org: "NVIDIA"
tags: [vlm, grounding, detection, efficiency, 2026]
upvotes: 130
---

# LocateAnything: Fast and High-Quality Vision-Language Grounding with Parallel Box Decoding

> Unified generative grounding and detection via Parallel Box Decoding — decodes box geometry as atomic units rather than sequential coordinate tokens, improving both localization accuracy and decoding throughput.

## Key Contributions
- **Parallel Box Decoding (PBD)**: decodes all geometric elements of a bounding box simultaneously as atomic units, rather than sequential 1D coordinate tokens
- **Geometric coherence**: preserves coupled structure of box geometry (x, y, w, h are interdependent) instead of treating them as independent tokens
- **Faster decoding throughput**: parallel generation of box coordinates eliminates sequential bottleneck
- **Improved localization accuracy**: geometric coupling during decoding produces more precise boxes
- **Unified grounding + detection**: single framework handles both VL grounding and open-vocabulary detection
- Trained on large-scale data for robust generalization

## Method
Standard VLMs serialize each 2D bounding box into multiple 1D coordinate tokens decoded sequentially. This mismatches the coupled geometric structure (coordinates are interdependent) and creates an inference bottleneck. LocateAnything introduces Parallel Box Decoding: each box is decoded as a single atomic unit with all geometric elements generated simultaneously. This preserves geometric coherence and enables parallel inference, dramatically improving both quality and speed.

## Results
- Higher localization accuracy than sequential coordinate-token approaches
- Significantly faster decoding throughput via parallelized box generation
- Unified performance across visual grounding and detection tasks
- Scales with large-scale training data

## Connections
- Builds on: [[sources/clip]], [[sources/grit]], [[concepts/vision-language-models]]
- Related: [[sources/opensearch-vl]], [[sources/citevqa]], [[concepts/llm-serving]]
- Organization: [[entities/orgs/nvidia]]

## Citation
> Wang et al., "LocateAnything: Fast and High-Quality Vision-Language Grounding with Parallel Box Decoding," arXiv:2605.27365, 2026.
