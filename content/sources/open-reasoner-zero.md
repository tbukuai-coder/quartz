---
type: source
arxiv_id: "2503.24290"
title: "Open-Reasoner-Zero: An Open Source Approach to Scaling Up Reinforcement Learning on the Base Model"
authors: ["Jingcheng Hu", "Yinmin Zhang", "Qi Han", "Daxin Jiang", "Xiangyu Zhang", "Heung-Yeung Shum"]
date: 2025-03-31
org: "StepFun / Tsinghua University"
tags: [reasoning, rl, ppo, grpo, open-source, 2025]
upvotes: 62
---

# Open-Reasoner-Zero

> First fully open-source implementation of large-scale reasoning-oriented RL on base models, showing vanilla PPO with GAE(λ=1, γ=1) beats GRPO and achieves superior results to DeepSeek-R1-Zero in 1/10 the training steps.

## Key Contributions
- **PPO > GRPO for reasoning RL**: Demonstrates that PPO with a learned critic is more stable and effective than GRPO (which uses group-relative advantages without a critic)
- **Minimalist recipe**: Vanilla PPO + GAE(λ=1, γ=1) + rule-based rewards + no KL regularization — sufficient for emergent reasoning
- **10× more efficient** than DeepSeek-R1-Zero pipeline on the same base model
- **Fully open**: Code, training data, model weights for 0.5B, 1.5B, 7B, 32B released
- **Critic analysis**: Quantitatively shows how the learned critic identifies and devalues repetitive patterns, improving training stability

## Method
1. **Algorithm**: PPO with Generalized Advantage Estimation (GAE) using λ=1, γ=1 — equivalent to using Monte Carlo returns minus value baseline
2. **Key design choices** (validated through ablations):
   - **PPO over GRPO**: Learned critic provides per-token advantage estimates; GRPO's group-relative normalization causes training instability
   - **GAE λ=1**: Maximum bias-variance trade-off toward unbiased estimates; lower λ values cause degradation
   - **No KL regularization**: Unnecessary — PPO's clipping already constrains policy updates
   - **Rule-based rewards**: Simple correctness checking (math answer = ground truth)
3. **Training**: Directly from Qwen2.5-{7B, 32B} base models — no SFT warm-up needed
4. **Critic initialization**: Both policy and critic from same base model; value head randomly initialized

## Results
- **Qwen2.5-32B base → ORZ-32B**: Outperforms DeepSeek-R1-Zero-Qwen-32B on AIME2024 (avg pass@1: 53.3 vs comparable), MATH500, GPQA Diamond
- **10× fewer training steps** than DeepSeek-R1-Zero pipeline
- Emergent reasoning behaviors: self-correction, backtracking, verification — same phenomena as R1-Zero
- Response length grows naturally with training (from ~500 to ~8000 tokens)
- PPO training significantly more stable than GRPO (no mid-training quality collapse)
- Scales from 0.5B to 32B — reasoning improves at every scale

## Datasets Used
- MATH training set (rule-based rewards)
- AIME, GPQA (evaluation only)

## Models Released
- **ORZ-{0.5B, 1.5B, 7B, 32B}** — all open-weight, trained from Qwen2.5 base models

## Connections
- Compares to: [[sources/deepseek-r1|DeepSeek-R1]] / R1-Zero (GRPO approach), [[sources/deepseekmath|DeepSeekMath/GRPO]]
- Complements: [[sources/s1|s1]] (SFT distillation approach — different paradigm for reasoning)
- Builds on: [[sources/qwen25|Qwen2.5]] (base models)
- Concepts: [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]], [[concepts/test-time-compute|Test-Time Compute Scaling]]

## Citation
> Hu et al., "Open-Reasoner-Zero: An Open Source Approach to Scaling Up Reinforcement Learning on the Base Model," arXiv:2503.24290, 2025.
