---
type: source
arxiv_id: "2508.07629"
title: "Klear-Reasoner: Advancing Reasoning Capability via Gradient-Preserving Clipping Policy Optimization"
authors: ["Zhenpeng Su", "Leiyu Pan", "Xue Bai", "Various"]
date: 2025-08-11
org: "Kuaishou / Various"
tags: [reasoning, rl, grpo, ppo, clipping, long-cot, sft, 2025]
upvotes: 43
---

# Klear-Reasoner: Gradient-Preserving Clipping Policy Optimization

> A detailed post-training report for reasoning models, introducing **GPPO** (Gradient-Preserving Clipping Policy Optimization) that fixes two key problems with RL clipping mechanisms — clipping suppresses exploration signals and ignores suboptimal trajectories. Achieves **90.5% on AIME 2024** and **83.2% on AIME 2025** from Qwen3-8B-Base. 82 GitHub ⭐.

## Key Contributions
- **Complete post-training report**: Covers the entire workflow from data preparation → long CoT SFT → RL, with detailed ablation studies — filling the reproducibility gap in reasoning model research
- **GPPO algorithm**: Fixes two critical issues in RL clipping: (1) standard clipping suppresses exploration by cutting gradients entirely, (2) suboptimal trajectories contribute zero learning signal. GPPO "gently backpropagates gradients from clipped tokens" rather than zeroing them
- **SFT insights**: Demonstrates that a small number of **high-quality** data sources outperforms diverse low-quality sources, and that **difficult samples without accuracy filtering** achieve better results
- **Strong results at 8B scale**: From Qwen3-8B-Base achieves 90.5% AIME24, 83.2% AIME25, 66.0% LCB-V5, 58.1% LCB-V6

## Method
### Long CoT SFT
- Quality-centric data construction (inspired by OpenThoughts): use **hard problems only** from competition math + LeetCode
- Key finding: filtering for correctness hurts — including incorrect but challenging CoT traces improves the model's ability to learn from difficulty
- Sources: OpenR1-Math-220k, OpenThoughts, competition data

### GPPO (Gradient-Preserving Clipping Policy Optimization)
Built on token-level GRPO + DAPO's Clip-Higher, with two fixes:
1. **Gradient preservation**: Instead of zeroing the gradient when the importance ratio exceeds the clip threshold, GPPO applies a soft decay — preserving learning signal from clipped tokens
2. **Negative sample learning**: Standard clipping discards all signal from suboptimal trajectories. GPPO maintains gradient flow from these samples, enabling the model to learn what *not* to do
3. Formalized as a generalized clipped objective with a smooth transition function replacing the hard clip boundary

### Training Details
- Base: Qwen3-8B-Base → Long CoT SFT → RL with GPPO
- RL data: Math + Code from Skywork-OR1, AceReason, NuminaMath, Taco, LiveCodeBench
- Framework: VERL (ByteDance)

## Results
| Benchmark | Klear-8B-SFT | Klear-8B (RL) | Qwen3-8B | Light-R1-8B |
|---|---|---|---|---|
| AIME 2024 | 74.3 | **90.5** | 78.7 | 76.0 |
| AIME 2025 | 57.5 | **83.2** | 68.8 | 62.1 |
| LCB-V5 | 53.9 | **66.0** | 57.6 | 51.9 |
| LCB-V6 | 41.1 | **58.1** | 48.1 | 46.0 |

### Ablation: GPPO vs alternatives
- GPPO outperforms both GRPO+Clip-Higher and CISPO (concurrent work)
- Gradient norm analysis shows GPPO maintains healthier gradient flow during training
- GPPO converges faster and achieves higher final performance

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/deepseekmath|DeepSeekMath/GRPO]], DAPO (Clip-Higher)
- **Related**: [[sources/prorl|ProRL]] (prolonged RL), [[sources/open-reasoner-zero|ORZ]] (PPO vs GRPO)
- **Concepts**: [[concepts/grpo|GRPO]], [[concepts/chain-of-thought|Chain-of-Thought]]
- **Comparisons**: [[comparisons/rl-reasoning-methods|RL Reasoning Methods]], [[comparisons/reasoning-models|Reasoning Models]]
- **GitHub**: https://github.com/suu990901/KlearReasoner

## Citation
> Su et al., "Klear-Reasoner: Advancing Reasoning Capability via Gradient-Preserving Clipping Policy Optimization," arXiv:2508.07629, 2025.
