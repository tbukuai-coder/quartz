---
type: source
arxiv_id: "2604.27711"
title: "ExoActor: Exocentric Video Generation as Generalizable Interactive Humanoid Control"
authors: ["Yi Wang", "Xinchen Li", "Pengwei Xie", "Pu Yang", "Buqing Nie", "Yunuo Cai", "Qinglin Zhang", "Chendi Qu", "Jeffrey Wu", "Jianheng Song", "and 6 more"]
date: 2026-04-23
org: "UC Berkeley / Tsinghua"
tags: [robotics, video-generation, humanoid-control, embodied-ai, vision-language-action, 2026]
upvotes: 38
---

# ExoActor: Exocentric Video Generation for Humanoid Control

> A framework bridging generative video modeling and humanoid robot control through third-person video generation — synthesizing imagined demonstrations that are converted into executable behaviors without task-specific data collection.

## Key Contributions

- **Third-person video as control interface**: Uses exocentric video generation to model interaction dynamics between robots, environments, and objects
- **Unified pipeline**: Video generation → whole-body and hand motion estimation → end-to-end motion execution
- **Decoupled design**: Separates high-level interaction modeling (video) from low-level control, enabling independent improvement of each component
- **No task-specific data needed**: Leverages pretrained video models' implicit knowledge

## Method

Given a task description and initial third-person observation:
1. Synthesize plausible execution process as third-person video plan
2. Transform videos into executable behaviors through motion estimation
3. Execute via whole-body and hand motion tracking

Tasks span difficulty levels: B-level (easy), A-level (moderate), S-level (challenging).

## Results

- Demonstrates feasibility on real-world humanoid tasks across diverse scenarios
- Enables interaction-aware behaviors without task-specific demonstrations
- Modular pipeline allows extensibility and adaptability

## Connections
- Builds on: [[sources/seedance]], [[concepts/video-generation]], [[concepts/agents]]
- Related concepts: [[concepts/multimodal-models]], [[concepts/vision-language-models]]
- Related papers: [[sources/cogvideox]], [[sources/svd]], [[sources/learning-while-deploying]]

## Citation
> Wang et al., "ExoActor: Exocentric Video Generation as Generalizable Interactive Humanoid Control," arXiv:2604.27711, 2026.
