---
type: source
arxiv_id: "2508.08221"
title: "Part I: Tricks or Traps? A Deep Dive into RL for LLM Reasoning"
authors: ["Zihe Liu", "Jiashun Liu", "Yancheng He", "Various"]
date: 2025-08-12
org: "Various"
tags: [reasoning, rl, guidelines, practical, 2025]
upvotes: 50
---

# Tricks or Traps? Deep Dive into RL for LLM Reasoning

> Systematic review that separates genuine RL improvements from artifacts. Produces clear, actionable guidelines and shows a minimalist technique combination outperforms complex recipes.

## Key Contributions
- **Standardized evaluation framework** for comparing RL techniques on equal footing
- Identified which RL tricks are **genuine improvements** vs **artifacts** of experimental setup
- Showed a **minimalist combination** (vanilla PPO + simple reward) can match or beat complex multi-trick approaches
- **Practical guidelines** organized by: training data, model initialization, algorithm choice, reward design
- Covers GRPO, DAPO, PPO, critic-free variants with controlled comparisons

## Key Findings
1. **Model initialization matters more than algorithm**: Starting from a well-SFT'd model dominates algorithm choice
2. **Critic-free RL** (GRPO, DAPO) is competitive with PPO when properly tuned
3. **Data quality >> data quantity** for RL training problems
4. **Many published tricks are entangled** with specific model/data combinations — don't generalize
5. **Minimalist recipe**: Good SFT init + vanilla PPO/GRPO + correctness reward = strong baseline

## Guidelines Summary
- **Start here**: SFT on high-quality reasoning data → GRPO with correctness reward
- **If stuck**: Increase problem diversity, not RL complexity
- **Avoid**: Stacking tricks without controlled ablation

## Connections
- **Practical companion to**: [[sources/rl-reasoning-survey|RL Survey]] (theory) — this paper is about what works in practice
- **Validates/challenges**: [[sources/prorl|ProRL]], [[sources/open-reasoner-zero|Open-Reasoner-Zero]], [[sources/deepseek-r1|DeepSeek-R1]]
- **Related concepts**: [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]]

## Citation
> Liu et al., "Part I: Tricks or Traps? A Deep Dive into RL for LLM Reasoning," arXiv:2508.08221, 2025.
