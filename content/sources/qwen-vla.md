---
type: source
arxiv_id: "2605.30280"
title: "Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments"
authors: ["Qiuyue Wang", "Mingsheng Li", "Jian Guan", "Jinhui Ye", "Sicheng Xie", "Yitao Liu", "Junhao Chen", "Zhixuan Liang", "Jie Zhang", "Xintong Hu"]
date: 2026-05-29
org: "Alibaba / Qwen Team"
tags: [robotics, vla, embodied-ai, multimodal, unified-model, 2026]
upvotes: 122
---

# Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments

> Unified embodied foundation model extending Qwen's VL stack to continuous action generation via DiT-based action decoder, joint pretraining, and embodiment-aware prompt conditioning — handles manipulation, navigation, and trajectory prediction across robot platforms.

## Key Contributions
- **DiT-based action decoder**: generates continuous actions via diffusion transformer conditioned on VL representations
- **Joint pretraining**: unified training across heterogeneous embodied tasks (manipulation, navigation, trajectory prediction)
- **Embodiment-aware prompt conditioning**: adapts to different robot platforms without separate fine-tuning
- **Visual grounding + spatial reasoning**: leverages Qwen VL capabilities for embodied perception
- **Out-of-distribution generalization**: transfers across unseen environments and robot embodiments

## Method
Qwen-VLA extends Qwen's vision-language modeling stack from perception to embodied action. A DiT-based action decoder generates continuous action sequences conditioned on the VL model's representations. Joint pretraining across diverse embodied datasets (manipulation, navigation, trajectory prediction) with embodiment-aware prompt conditioning enables a single model to handle multiple robot platforms. The shared VL backbone provides visual grounding and spatial reasoning that transfers across tasks.

## Results
- Strong performance across manipulation, navigation, and trajectory prediction
- Generalizes to unseen environments and novel robot embodiments
- Single unified model replaces task-specific specialized systems

## Connections
- Builds on: [[sources/physbrain]], [[sources/qwen25-vl]], [[entities/orgs/alibaba]]
- Related: [[sources/learning-while-deploying]], [[sources/exoactor]], [[concepts/multimodal-models]]
- Organization: [[entities/orgs/alibaba]] / Qwen ecosystem

## Citation
> Wang et al., "Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments," arXiv:2605.30280, 2026.
