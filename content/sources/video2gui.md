---
type: source
arxiv_id: "2605.14747"
title: "Video2GUI: Synthesizing Large-Scale Interaction Trajectories for Generalized GUI Agent Pretraining"
authors: ["Weimin Xiong", "Shuhao Gu", "Bowen Ye", "Zihao Yue", "Lei Li", "Feifan Song", "Sujian Li", "Hao Tian"]
date: 2026-05-21
org: "Peking University"
tags: [agents, gui, pretraining, data-synthesis, multimodal, 2026]
upvotes: 145
---

# Video2GUI: Synthesizing Large-Scale Interaction Trajectories for Generalized GUI Agent Pretraining

> Fully automated framework extracting grounded GUI interaction trajectories from unlabeled internet videos via coarse-to-fine filtering, enabling large-scale pretraining data for generalized GUI agents without costly manual annotations.

## Key Contributions
- **Automated trajectory extraction from internet video**: converts unlabeled screen recordings into structured GUI interaction trajectories
- **Coarse-to-fine filtering pipeline**: progressively filters noisy video data to extract high-quality interaction sequences
- **Large-scale GUI pretraining dataset**: enables pretraining across diverse real-world applications without manual annotation
- **Generalized GUI agents**: models pretrained on Video2GUI data generalize to unseen applications and platforms
- Addresses the key bottleneck of data scarcity in GUI agent research

## Method
Video2GUI automatically processes unlabeled internet videos (screen recordings, tutorials, demos) through a coarse-to-fine pipeline: (1) coarse filtering identifies videos containing GUI interactions; (2) fine-grained extraction localizes clicks, scrolls, and keystrokes with bounding-box grounding; (3) structured agent trajectories are assembled with action types, coordinates, and temporal ordering. The resulting dataset spans diverse applications, enabling GUI agents to generalize beyond narrow domains.

## Results
- Significant improvements on GUI grounding and action benchmarks after pretraining
- Generalizes across platforms (web, mobile, desktop) and application domains
- Eliminates dependency on costly manual annotation for GUI agent training data

## Connections
- Builds on: [[sources/llava]], [[concepts/agents]], [[concepts/vision-language-models]]
- Related: [[sources/skillopt]], [[sources/code-as-agent-harness]], [[sources/swe-webdevbench]]
- Fills gap: scalable data generation for GUI agents

## Citation
> Xiong et al., "Video2GUI: Synthesizing Large-Scale Interaction Trajectories for Generalized GUI Agent Pretraining," arXiv:2605.14747, 2026.
