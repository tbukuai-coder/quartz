---
type: source
arxiv_id: "2605.00416"
title: "Learning while Deploying: Fleet-Scale Reinforcement Learning for Generalist Robot Policies"
authors: ["Yi Wang", "Xinchen Li", "Pengwei Xie", "Pu Yang", "Buqing Nie", "Yunuo Cai", "Qinglin Zhang", "Chendi Qu", "Jeffrey Wu", "Jianheng Song", "and 6 more"]
date: 2026-05-02
org: "Unknown"
tags: [robotics, vla, reinforcement-learning, fleet-scale, continual-learning, embodied-ai, 2026]
upvotes: 7
---

# Learning while Deploying: Fleet-Scale RL for Generalist Robot Policies

> An offline-to-online RL framework that enables continual post-training of Vision-Language-Action (VLA) policies from fleet-scale deployment experience, achieving 0.95 average success rate across long-horizon manipulation tasks.

## Key Contributions

- **Learning While Deploying (LWD) paradigm**: Recasts deployment from training endpoint to a source of continual policy improvement via fleet-scale data flywheel
- **Distributional Implicit Value Learning (DIVL)**: Learns multi-step return distributions from heterogeneous off-policy deployment data with sparse rewards, preserving rare high-return modes that scalar critics collapse
- **Q-learning with Adjoint Matching (QAM)**: Converts critic gradients into stable step-wise supervision for flow-based VLA policies without backpropagating through full multi-step denoising
- **Real-world validation**: 16 dual-arm robots across 8 manipulation tasks including 3–5 minute long-horizon precision tasks (Gongfu tea, cocktails, fruit juice)

## Method

The framework addresses three key challenges:
1. **Heterogeneous deployment data**: Robots collect data asynchronously under different policy versions, with sparse rewards, failures, partial recoveries, and human interventions
2. **Off-policy learning stability**: DIVL retains in-support policy improvement property of Implicit Q-Learning while modeling full return distributions
3. **Generative policy extraction**: QAM provides stable gradients for flow-based action generators without destabilizing the pretrained VLA model

Two-stage pipeline:
1. **Offline pretraining** on diverse data mixtures
2. **Online finetuning** with streaming deployment data, optimizing the same RL objective to avoid offline-to-online mismatch

## Results

- **Average success rate: 0.95** across all tasks
- Substantially outperforms pretrained model and relevant baselines
- Performance gap especially pronounced on **long-horizon tasks** where RL propagates rewards through multi-step dynamic programming
- Demonstrates scaling with fleet experience accumulation

## Connections
- Builds on: [[sources/exoactor]], [[concepts/agents]], [[concepts/rlhf]]
- Related concepts: [[concepts/multimodal-models]], [[concepts/vision-language-models]]
- Related papers: [[sources/cogvideox]], [[sources/seedance]]
- Cited by / Influenced: Continual learning for embodied AI, fleet-scale robotics

## Citation
> Wang et al., "Learning while Deploying: Fleet-Scale Reinforcement Learning for Generalist Robot Policies," arXiv:2605.00416, 2026.
