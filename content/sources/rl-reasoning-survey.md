---
type: source
arxiv_id: "2509.08827"
title: "A Survey of Reinforcement Learning for Large Reasoning Models"
authors: ["Tsinghua C3I", "Various"]
date: 2025-09-12
org: "Tsinghua / Various"
tags: [reasoning, rl, survey, grpo, ppo, scaling, 2025]
upvotes: 193
---

# A Survey of RL for Large Reasoning Models

> The definitive survey of RL for reasoning in LLMs post-DeepSeek-R1 — covering algorithms (PPO, GRPO, DAPO), training data, reward design, infrastructure, and scaling challenges. 2,445 GitHub ⭐.

## Key Contributions
- **Comprehensive taxonomy** of RL methods for reasoning: PPO variants, GRPO, DAPO, reward design, data strategies
- Covers the full stack: **algorithms → training data → infrastructure → downstream applications**
- Analyzes the shift from LLMs to **Large Reasoning Models (LRMs)** as a distinct paradigm
- Identifies **foundational challenges** for scaling RL toward ASI: reward hacking, exploration, compute efficiency
- Most-cited and most-starred open resource for RL reasoning research (2,445 GitHub ⭐)

## Scope
The survey covers post-DeepSeek-R1 developments across:
1. **Foundational RL algorithms**: PPO, GRPO, DAPO, REINFORCE, variants with critic-free designs
2. **Reward design**: Outcome-based (ORM), process-based (PRM), rule-based, AI-judge rewards
3. **Training data**: Math, code, scientific reasoning, agentic tasks; synthetic vs curated
4. **Infrastructure**: Distributed RL training, on-policy vs off-policy, memory efficiency
5. **Applications**: Math competition (AIME/IMO), code (SWE-bench), general reasoning, agents
6. **Open challenges**: Reward hacking, catastrophic forgetting, compute scaling, evaluation reliability

## Key Findings
- **GRPO and PPO remain dominant** but critic-free variants are gaining ground
- **Reward design is the bottleneck** — most gains come from better rewards, not better algorithms
- **Data quality trumps quantity** for reasoning RL — curated problems > random problems
- **Infrastructure gaps** are a major barrier to academic research scaling RL
- **Post-R1 explosion**: >100 papers in 6 months on RL for reasoning

## Connections
- **Covers**: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/deepseekmath|DeepSeekMath/GRPO]], [[sources/open-reasoner-zero|Open-Reasoner-Zero]], [[sources/prorl|ProRL]], [[sources/swe-rl|SWE-RL]]
- **Related concepts**: [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]], [[concepts/process-reward-models|PRMs]], [[concepts/test-time-compute|Test-Time Compute]]
- **Related comparisons**: [[comparisons/reasoning-models|Reasoning Models]], [[comparisons/alignment-methods|Alignment Methods]]

## Citation
> "A Survey of Reinforcement Learning for Large Reasoning Models," arXiv:2509.08827, 2025.
