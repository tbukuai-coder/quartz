---
type: source
arxiv_id: "2605.04451"
title: "RemoteZero: Geospatial Reasoning with Zero Human Annotations"
authors: ["Liang Yao", "Fan Liu", "Shengxiang Xu", "Chuanyi Zhang", "Rui Min", "Shimin Di", "Yuhui Zheng"]
date: 2026-05
tags: [multimodal, geospatial, remote-sensing, mllm, grpo, self-supervised, zero-annotation]
upvotes: 4
---

# RemoteZero: Geospatial Reasoning with Zero Human Annotations

> Enables geospatial reasoning without box supervision by leveraging semantic verification capabilities of MLLMs for self-evolving localization from unlabeled remote sensing data using GRPO training.

## Key Contributions
- Eliminates the final dependency on human-annotated ground-truth coordinates for geospatial reasoning
- Proposes self-evolving localization where the model improves its spatial reasoning from unlabeled remote sensing imagery
- Uses semantic verification capabilities of Multimodal Large Language Models (MLLMs) as a reward signal
- Trains with GRPO (Group Relative Policy Optimization) using semantic verification rewards

## Method
The approach works as follows:
1. A geospatial MLLM generates reasoning chains and target location predictions from remote sensing imagery
2. Instead of comparing to human-annotated boxes, the model uses semantic verification: checking whether the predicted region semantically matches the query intent
3. The semantic verification score serves as the reward signal for GRPO training
4. Through iterative self-evolution, the model improves localization accuracy without any human spatial annotations

## Results
- Enables true self-evolution on abundant unlabeled remote sensing data
- Breaks the dependency between autonomous reasoning and human-annotated spatial endpoints

## Datasets Used
- Unlabeled remote sensing imagery datasets

## Models Released
- None explicitly mentioned

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]] — GRPO training methodology
- Related: [[sources/eywa]] — heterogeneous agentic framework
- Related: [[sources/grit]] — visual reasoning with bounding boxes
- Related concept: [[concepts/agents]], [[concepts/multimodal-models]]

## Citation
> Yao et al., "RemoteZero: Geospatial Reasoning with Zero Human Annotations," arXiv:2605.04451, 2026.
