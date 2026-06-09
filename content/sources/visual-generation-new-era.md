---
type: source
arxiv_id: "2604.28185"
title: "Visual Generation in the New Era: An Evolution from Atomic Mapping to Agentic World Modeling"
authors: ["Keming Wu", "Zuhao Yang", "Kaichen Zhang", "Shizun Wang", "Haowei Zhu", "Sicong Leng", "Zhongyu Yang", "Qijie Wang", "Sudong Wang", "Ziting Wang", "and 17 more"]
date: 2026-04-25
org: "Multiple Institutions"
tags: [vision, visual-generation, survey, agentic-ai, world-models, 2026]
upvotes: 82
---

# Visual Generation in the New Era: From Atomic Mapping to Agentic World Modeling

> A comprehensive roadmap arguing that visual generation must evolve beyond appearance synthesis toward intelligent visual generation grounded in structure, dynamics, and causal understanding — organized as a five-level capability taxonomy.

## Key Contributions

- **Five-level taxonomy of visual intelligence**: Atomic Generation → Conditional Generation → In-Context Generation → Agentic Generation → World-Modeling Generation
- **Synthesis of major technical drivers**: Transition from diffusion to flow matching, unified understanding-and-generation systems, VLM-based relabeling, post-training alignment (DPO, GRPO, reward models)
- **Application progression**: From conditional generation and domain adaptation to reasoning-driven editing and embodied interaction
- **Stress-testing perspective**: In-the-wild evaluation reveals failures in spatial logic, physical reasoning, identity preservation, and causal grounding despite high aesthetic quality

## Key Insights

- 2025 alone contributed 188 papers (45.7% of post-2014 references analyzed), reflecting exponential acceleration
- Frontier systems (Nano Banana, GPT-Image, Qwen-Image, Z-Image) excel at photorealism but fail on puzzle-like spatial reconstruction, multi-step state-transition editing, and persistent character identity
- Conventional metrics (FID, CLIP-based alignment) are increasingly insufficient; need richer task-specific evaluation and in-the-wild stress testing
- Success increasingly depends on data curation, VLM-driven relabeling, synthetic data distillation, and post-training alignment rather than parameter scaling alone

## Connections
- Builds on: [[sources/sd3]], [[sources/rectified-flow]], [[sources/seedance]], [[sources/dit]], [[concepts/diffusion-models]]
- Related concepts: [[concepts/agents]], [[concepts/multimodal-models]], [[concepts/structured-generation]]
- Related comparisons: [[comparisons/diffusion-architectures]], [[comparisons/vision-language-models]]
- Cited by / Influenced: Emerging work on agentic visual intelligence and playable world models

## Citation
> Wu et al., "Visual Generation in the New Era: An Evolution from Atomic Mapping to Agentic World Modeling," arXiv:2604.28185, 2026.
