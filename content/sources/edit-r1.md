---
type: source
arxiv_id: "2604.27505"
title: "Edit-R1: Leveraging Verifier-Based Reinforcement Learning in Image Editing"
authors: ["Hanzhong Guo", "Jie Wu", "Jie Liu", "Yu Gao", "Zilyu Ye", "Linxiao Yuan", "Xionghui Wang", "Yizhou Yu", "Weilin Huang"]
date: 2026-04-22
org: "Chinese University of Hong Kong / ByteDance"
tags: [image-editing, rlhf, reward-model, vision, reinforcement-learning, 2026]
upvotes: 29
---

# Edit-R1: Verifier-Based Reinforcement Learning in Image Editing

> A framework that shifts image editing reward modeling from holistic scoring to reasoning verification using chain-of-thought analysis, achieving substantial gains on SOTA editors like FLUX.1-kontext and Qwen-Image-Edit.

## Key Contributions

- **Reasoning Reward Model (RRM)**: Paradigm shift from simple scorer to reasoning verifier that decomposes editing instructions into principles and generates CoT analysis
- **Group Contrastive Preference Optimization (GCPO)**: Novel RL algorithm optimizing pointwise reasoning-based reward model using pairwise preference data by contrasting "winner" and "loser" reasoning trajectories
- **GRPO-based downstream training**: Uses the trained non-differentiable RRM as verifier in reinforcement learning loop to improve editing models
- **State-of-the-art results**: 7B RL-RRM surpasses concurrent EditScore and delivers gains to FLUX.1-kontext and Qwen-Image-Edit

## Method

Key challenge: image editing needs nuanced evaluation (instruction fidelity, preservation of unedited regions, overall quality) but existing RMs give holistic scores. Edit-R1 solves this by:
1. Building a verifier that decomposes instructions and verifies each sub-task with CoT reasoning
2. Training RRM with GCPO on winner/loser trajectory groups
3. Using RRM as verifier in GRPO loop for downstream editing model improvement

## Results

- 7B RL-RRM significantly surpasses EditScore on EditRewardBench
- Substantial downstream gains to FLUX.1-kontext and Qwen-Image-Edit
- First framework to integrate reasoning verifier + CoT + RL for image editing

## Connections
- Builds on: [[sources/grpo]], [[concepts/rlhf]], [[sources/reasoning-vectors]], [[concepts/chain-of-thought]]
- Related concepts: [[concepts/preference-optimization]], [[concepts/diffusion-models]]
- Related comparisons: [[comparisons/diffusion-architectures]]
- Cited by / Influenced: Visual reward modeling and RL for image generation

## Citation
> Guo et al., "Edit-R1: Leveraging Verifier-Based Reinforcement Learning in Image Editing," arXiv:2604.27505, 2026.
