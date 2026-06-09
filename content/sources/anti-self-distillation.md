---
type: source
arxiv_id: "2605.11609"
title: "Anti-Self-Distillation for Reasoning RL via Pointwise Mutual Information"
authors: ["Guobin Shen", "Xiang Cheng", "Chenxiao Zhao", "Lei Huang", "Jindong Li", "Dongcheng Zhao", "Xing Yu"]
date: 2026-05-20
org: "CAS / UCAS"
tags: [rl, reasoning, self-distillation, pmi, grpo, 2026]
upvotes: 195
---

# Anti-Self-Distillation for Reasoning RL via Pointwise Mutual Information

> Reverses the direction of knowledge transfer in on-policy self-distillation for math reasoning, using PMI analysis to show that privileged context inflates teacher confidence on already-predictable tokens, and an entropy-triggered gate to selectively apply anti-distillation.

## Key Contributions
- **PMI analysis** of self-distillation failure: privileged context (verified solutions) inflates teacher confidence on tokens already predictable by the student, providing no useful signal
- **Anti-Self-Distillation**: reverses the KL direction — pushes the student *away* from the teacher on low-PMI tokens where the teacher is spuriously confident
- **Entropy-triggered gate**: applies anti-distillation selectively at high-entropy positions where the student is uncertain, avoiding damage at confident positions
- Achieves consistent improvements over GRPO baseline on math reasoning without external teachers

## Method
On-policy self-distillation conditions a teacher copy on privileged context (e.g., verified solutions) and pulls the student toward it. PMI analysis shows this fails for math reasoning because the teacher's confidence boost concentrates on tokens already predictable without the privilege. Anti-SD reverses the transfer: at positions where the student's entropy is high but teacher PMI is low, it pushes the student distribution *away* from the teacher, encouraging exploration of alternative tokens. An entropy-triggered gate ensures this only applies where the student is genuinely uncertain.

## Results
- Improves over GRPO baseline on MATH, GSM8K, and competition-level benchmarks
- More token-efficient reasoning trajectories (shorter solutions with equal/higher accuracy)
- No external stronger teacher required — uses only self-distillation with reversed direction

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]], [[sources/tricks-or-traps-rl]]
- Related: [[sources/resrl]], [[sources/nonsense-helps-lope]], [[sources/delta-token-credit]]
- Related concepts: [[concepts/distillation]], [[concepts/rlhf]], [[comparisons/rl-reasoning-methods]]

## Citation
> Shen et al., "Anti-Self-Distillation for Reasoning RL via Pointwise Mutual Information," arXiv:2605.11609, 2026.
