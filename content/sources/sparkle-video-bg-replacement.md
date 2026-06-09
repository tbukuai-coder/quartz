---
type: source
arxiv_id: "2605.06535"
title: "Sparkle: Realizing Lively Instruction-Guided Video Background Replacement via Decoupled Guidance"
authors: ["Ziyun Zeng", "Yiqi Lin", "Guoqiang Liang", "Mike Zheng Shou"]
date: 2026-05
tags: [video-editing, background-replacement, diffusion-models, instruction-guided, video-generation]
upvotes: 1
---

# Sparkle: Realizing Lively Instruction-Guided Video Background Replacement via Decoupled Guidance

> A new dataset and benchmark for background replacement in video editing, addressing limitations in existing datasets through a scalable pipeline with improved guidance mechanisms via decoupled guidance.

## Key Contributions
- Introduces a new dataset and benchmark for background replacement in video editing
- Addresses limitations in existing datasets that predominantly focus on local editing or style transfer (which preserve original scene structure)
- Background replacement requires synthesizing entirely new, temporally consistent scenes while maintaining foreground objects
- Proposes decoupled guidance mechanisms to separately control foreground and background generation
- Scalable data synthesis pipeline for generating training pairs

## Method
The Sparkle approach:
1. **Decoupled guidance**: Separates foreground preservation guidance from background generation guidance
2. **Temporal consistency**: Ensures the generated background maintains temporal coherence across video frames
3. **Foreground-background interaction**: Handles complex interactions between foreground objects and new backgrounds (shadows, reflections, lighting)
4. **Scalable pipeline**: Automated data synthesis for generating high-quality training pairs with background replacement labels

## Results
- New benchmark for instruction-guided video background replacement
- Improved quality and temporal consistency compared to existing video editing methods

## Datasets Used
- Newly introduced video background replacement dataset

## Models Released
- GitHub: https://github.com/showlab/Sparkle (1 star)

## Connections
- Related: [[sources/seedance]] — video generation with RLHF
- Related: [[sources/cogvideox]] — open text-to-video generation
- Related: [[sources/edit-r1]] — RL for image editing
- Related concept: [[concepts/video-generation]], [[concepts/diffusion-models]]

## Citation
> Zeng et al., "Sparkle: Realizing Lively Instruction-Guided Video Background Replacement via Decoupled Guidance," arXiv:2605.06535, 2026.
