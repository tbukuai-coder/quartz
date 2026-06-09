---
type: source
arxiv_id: "2505.24864"
title: "ProRL: Prolonged Reinforcement Learning Expands Reasoning Boundaries in Large Language Models"
authors: ["Mingjie Liu", "Shizhe Diao", "Ximing Lu", "Jian Hu", "Xin Dong"]
date: 2025-05-30
org: "NVIDIA / Various"
tags: [reasoning, rl, training, scaling, 2025]
upvotes: 146
---

# ProRL

> Demonstrates that prolonged RL training (not just a few epochs) genuinely expands reasoning boundaries in LLMs, challenging the view that RL merely amplifies pre-existing capabilities.

## Key Contributions
- **Challenged the prevailing assumption** that RL only amplifies reasoning already latent in the base model — showed that prolonged RL discovers genuinely novel reasoning strategies
- Introduced **ProRL** framework with KL divergence control and reference policy resetting for stable long-horizon RL
- Achieved **significant reasoning improvements** on pass@k evaluations, demonstrating expanded reasoning boundaries
- Showed that **continually scaling RL compute** reliably improves reasoning — no plateau observed
- Practical implications: invest more in RL compute, don't stop early

## Method
Key innovations for stable prolonged RL:
1. **KL divergence control**: Dynamically manage the KL penalty to prevent reward hacking while allowing the model to explore far from the initial distribution
2. **Reference policy resetting**: Periodically reset the reference policy to the current policy, allowing the model to continue learning without being anchored to the initial weights
3. **Extended training**: Train for significantly more RL steps than typical approaches (10-100× more)

## Results
- **Pass@k improvements**: Models discover new solution strategies not present in base model's distribution
- **AIME**: Continued improvement with more RL compute, no plateau
- **MATH-500**: Consistent gains beyond what SFT or short RL achieves
- **Novel strategies**: Qualitative analysis shows the model develops reasoning patterns not seen in training data

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]] (RL for reasoning), [[sources/open-reasoner-zero|Open-Reasoner-Zero]]
- **Related**: [[sources/deepseekmath|DeepSeekMath/GRPO]], [[concepts/grpo|GRPO]]
- **Challenges**: The view that RL merely amplifies pre-existing capabilities
- **Implications for**: [[comparisons/reasoning-models|Reasoning Models]] — invest in compute, not just data
- **Related concepts**: [[concepts/test-time-compute|Test-Time Compute]], [[concepts/rlhf|RLHF]]

## Citation
> Liu et al., "ProRL: Prolonged Reinforcement Learning Expands Reasoning Boundaries in Large Language Models," arXiv:2505.24864, 2025.
