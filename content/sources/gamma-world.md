---
type: source
arxiv_id: "2605.28816"
title: "Gamma-World: Generative Multi-Agent World Modeling Beyond Two Players"
authors: ["Fangfu Liu", "Kai He", "Tianchang Shen", "Tianshi Cao", "Sanja Fidler", "Yueqi Duan", "Jun Gao", "Igor Gilitschenski", "Zian Wang", "Xuanchi Ren"]
date: 2026-05-28
org: "NVIDIA / University of Toronto"
tags: [video-generation, world-models, multi-agent, diffusion, 2026]
upvotes: 410
---

# Gamma-World: Generative Multi-Agent World Modeling Beyond Two Players

> First generative world model that scales interactive video generation to multiple simultaneously-controlled agents via permutation-symmetric encodings and sparse attention.

## Key Contributions
- Introduces **Simplex Rotary Agent Encoding**: a parameter-free extension of 3D RoPE that represents agents as vertices of a regular simplex in rotary angle space, giving each agent a distinct phase while remaining permutation-equivalent
- Proposes **Sparse Hub Attention**: learnable hub tokens mediate cross-agent interaction, reducing attention cost from quadratic to linear in the number of agents
- Distills a full-context diffusion teacher into a **causal student** with KV caching for real-time action-responsive generation at 24 FPS
- Generalizes from 2 to 4 players without additional training

## Method
The model builds on autoregressive diffusion for video generation. Each agent's actions are encoded with Simplex Rotary encoding that extends 3D RoPE — agents occupy symmetric vertices in angle space, making the model agnostic to agent ordering. Sparse Hub Attention replaces dense all-to-all cross-agent attention with a small set of learnable hub tokens that aggregate and distribute information across agents. For deployment, a causal student is distilled from the diffusion teacher using KV caching for sequential temporal block generation.

## Results
- Improved video fidelity (FVD), action controllability, and inter-agent consistency over slot-based and dense-attention baselines
- Scales to 4 simultaneous players in multiplayer virtual environments
- Achieves 24 FPS real-time generation

## Connections
- Builds on: [[sources/seedance]], [[sources/self-forcing-pp]], [[concepts/diffusion-models]]
- Related concepts: [[concepts/video-generation]], [[concepts/multi-agent-systems]], [[concepts/kv-cache]]
- Extends: DiT-based video generation to multi-agent interactive settings

## Citation
> Liu et al., "Gamma-World: Generative Multi-Agent World Modeling Beyond Two Players," arXiv:2605.28816, 2026.
