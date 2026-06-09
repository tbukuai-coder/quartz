---
type: source
arxiv_id: "2604.27083"
title: "Co-Evolving Policy Distillation"
authors: ["Naibin Gu", "Chenxu Yang", "Qingyi Si", "Chuanyu Qin", "Dingyu Yao", "Peng Fu", "Zheng Lin", "Weiping Wang", "Nan Duan", "Jiaqi Wang"]
date: 2026-04-19
org: "Chinese Academy of Sciences"
tags: [rlhf, distillation, post-training, multimodal, reasoning, 2026]
upvotes: 48
---

# Co-Evolving Policy Distillation (CoPD)

> A unified approach to integrating multiple expert capabilities through parallel training and bidirectional policy distillation, outperforming mixed RLVR and traditional OPD in multi-modal reasoning tasks.

## Key Contributions

- **Unified analysis of RLVR and OPD paradigms**: Identifies capability loss mechanisms — mixed RLVR suffers from inter-capability divergence cost, while expert-then-OPD fails due to large behavioral pattern gaps
- **Co-Evolving Policy Distillation (CoPD)**: Parallel training of experts with OPD introduced during ongoing RLVR rather than after complete training
- **Bidirectional policy distillation**: Experts serve as mutual teachers, co-evolving to maintain consistent behavioral patterns while preserving complementary knowledge
- **All-in-one integration**: Achieves unified text, image, and video reasoning capabilities

## Method

CoPD addresses two failure modes of existing approaches:
1. Mixed RLVR: Experts interfere with each other during joint training (divergence cost)
2. Expert-then-OPD: Student cannot fully absorb teacher capabilities due to behavioral gap

Solution: Train experts in parallel, perform bidirectional distillation *during* ongoing RLVR training (not after), so experts co-evolve with aligned behavioral patterns.

## Results

- Significantly outperforms mixed RLVR and MOPD baselines
- Surpasses domain-specific experts on multi-modal reasoning tasks
- Suggests a novel training scaling paradigm via model parallel training

## Connections
- Builds on: [[sources/dpo]], [[sources/grpo]], [[concepts/distillation]], [[sources/agentic-rl-reasoning]]
- Related concepts: [[concepts/rlhf]], [[concepts/preference-optimization]], [[concepts/multi-token-prediction]]
- Related papers: [[sources/deepseek-r1]], [[sources/open-reasoner-zero]], [[sources/tricks-or-traps-rl]]

## Citation
> Gu et al., "Co-Evolving Policy Distillation," arXiv:2604.27083, 2026.
