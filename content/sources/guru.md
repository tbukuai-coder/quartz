---
type: source
arxiv_id: "2506.14965"
title: "Revisiting Reinforcement Learning for LLM Reasoning from A Cross-Domain Perspective"
authors: ["Zhoujun Cheng", "Shibo Hao", "Tianyang Liu", "Fan Zhou", "Various (LLM360)"]
date: 2025-06-20
org: "LLM360 / Various"
tags: [reasoning, rl, cross-domain, grpo, data-curation, 2025]
upvotes: 50
---

# Guru: Cross-Domain RL for LLM Reasoning

> Introduces **Guru**, a curated 92K-example RL reasoning corpus spanning six domains (Math, Code, Science, Logic, Simulation, Tabular), with domain-specific reward design — revealing that RL for reasoning behaves differently across domains and that in-domain training is essential for underrepresented domains. 148 GitHub ⭐.

## Key Contributions
- **Guru corpus**: 92K verifiable reasoning examples across **six domains** — Math, Code, Science, Logic, Simulation, and Tabular — each built with domain-specific reward design, deduplication, and filtering
- **Cross-domain analysis**: Systematically revisits RL-for-reasoning findings across domains, revealing that prior conclusions (drawn from math/code only) don't generalize uniformly
- **Domain-dependent skill acquisition**: Domains frequently seen during pretraining (Math, Code, Science) benefit from cross-domain RL, while underrepresented domains (Logic, Simulation, Tabular) **require in-domain training** — suggesting RL can facilitate genuine skill acquisition, not just knowledge elicitation
- **Guru-7B and Guru-32B**: State-of-the-art among open models RL-trained with publicly available data, outperforming best baselines by **7.9%** and **6.7%** on a 17-task evaluation suite across all six domains
- **Pass@k improvements**: Models effectively improve Pass@k of their base models, especially on complex tasks less likely to appear in pretraining data

## Method
1. **Data curation**: For each of six domains, design domain-specific verifiable reward signals (math: answer matching; code: execution; science: structured answer extraction; logic/simulation/tabular: custom verification pipelines)
2. **Deduplication and filtering**: Domain-specific quality filtering to ensure reliability for RL
3. **Cross-domain RL training**: Train using GRPO with the full Guru corpus, systematically evaluating cross-domain transfer vs. in-domain specialization
4. **Evaluation**: 17-task suite spanning all six domains

Key insight: Most RL reasoning research focuses narrowly on math/code. By expanding to six domains with verifiable rewards, Guru reveals that the benefits and dynamics of RL differ fundamentally by domain.

## Results
- **Guru-7B**: Outperforms best open RL baselines by 7.9% on 17-task suite
- **Guru-32B**: Outperforms best open RL baselines by 6.7%
- Cross-domain training helps well-represented domains but fails for underrepresented ones
- In-domain training is essential for Logic, Simulation, and Tabular reasoning
- Pass@k gains are strongest on complex, novel tasks

## Connections
- **Builds on**: [[sources/deepseek-r1|DeepSeek-R1]], [[sources/deepseekmath|DeepSeekMath/GRPO]]
- **Related**: [[sources/general-reasoner|General-Reasoner]] (also cross-domain RL), [[sources/rl-reasoning-survey|RL Survey]], [[sources/tricks-or-traps-rl|Tricks or Traps]]
- **Concepts**: [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]], [[concepts/synthetic-data|Synthetic Data]]
- **Comparisons**: [[comparisons/rl-reasoning-methods|RL Reasoning Methods]], [[comparisons/reasoning-models|Reasoning Models]]
- **GitHub**: https://github.com/LLM360/Reasoning360

## Citation
> Cheng et al., "Revisiting Reinforcement Learning for LLM Reasoning from A Cross-Domain Perspective," arXiv:2506.14965, 2025.
