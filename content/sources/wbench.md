---
type: source
arxiv_id: "2605.25874"
title: "WBench: A Comprehensive Multi-turn Benchmark for Interactive Video World Model Evaluation"
authors: ["Kaining Ying", "Hengrui Hu", "Siyu Ren", "Jiamu Li", "Fengjiao Chen", "Ziwen Wang", "Xuezhi Cao", "Xunliang Cai", "Henghui Ding"]
date: 2026-05-26
org: "Meituan"
tags: [benchmark, world-models, video, multi-turn, evaluation, 2026]
upvotes: 101
---

# WBench: A Comprehensive Multi-turn Benchmark for Interactive Video World Model Evaluation

> First comprehensive multi-turn benchmark for interactive world models evaluating 5 dimensions (video quality, setting adherence, interaction adherence, consistency, physics compliance) across 289 test cases and 1,058 interaction turns.

## Key Contributions
- **5-dimensional evaluation**: video quality, setting adherence, interaction adherence, consistency, and physics compliance
- **Multi-turn interaction**: 1,058 interaction turns testing sustained world consistency under user actions
- **289 diverse test cases**: covers various scenarios and interaction types
- **Automatic sub-metrics**: vision model and multimodal model-based scoring for scalable evaluation
- **108 GitHub stars** at Meituan
- First unified standard for evaluating interactive world models (Gamma-World, SANA-WM class)

## Method
WBench evaluates interactive world models through multi-turn interactions where an evaluator issues sequential actions and the world model must maintain consistency while responding. Five dimensions are assessed: (1) video quality — perceptual fidelity; (2) setting adherence — does the world match specifications; (3) interaction adherence — do actions produce correct effects; (4) consistency — is the world self-consistent across turns; (5) physics compliance — do physical laws hold. Automatic metrics use vision and multimodal models for scalable scoring.

## Results
- Reveals significant gaps in current world models across physics compliance and long-term consistency
- Provides standardized comparison across diverse world model architectures
- Identifies interaction adherence as the hardest dimension for current models

## Connections
- Builds on: [[sources/gamma-world]], [[sources/sana-wm]], [[concepts/video-generation]]
- Related: [[sources/trust-imagination-wam]], [[concepts/llm-evaluation]]
- Evaluates: the entire class of interactive world models emerging in 2026

## Citation
> Ying et al., "WBench: A Comprehensive Multi-turn Benchmark for Interactive Video World Model Evaluation," arXiv:2605.25874, 2026.
