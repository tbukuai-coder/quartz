---
type: source
arxiv_id: "2605.23904"
title: "SkillOpt: Executive Strategy for Self-Evolving Agent Skills"
authors: ["Yifan Yang", "Ziyang Gong", "Weiquan Huang", "Qihao Yang", "Ziwei Zhou", "Zisu Huang", "Yan Li", "Xuemei Gao", "Qi Dai", "Bei Liu"]
date: 2026-05-25
org: "Microsoft"
tags: [agents, skill-optimization, text-space-optimization, rl, 2026]
upvotes: 212
---

# SkillOpt: Executive Strategy for Self-Evolving Agent Skills

> First systematic text-space optimizer for agent skills — treats skills as trainable external agent state with bounded edits, validation gates, and reproducible optimization schedules, achieving +9.6 to +39.0 gains over no-skill baselines.

## Key Contributions
- Introduces **SkillOpt**: treats agent skills as external state of a frozen model, optimized with deep-learning-style discipline (learning rate → edit budget, validation gate, rejected-edit buffer)
- **Bounded text updates**: cosine-scheduled edit budget limits add/delete/replace operations per step, preventing skill regression
- **Minibatch reflection**: optimizer model reflects on batched trajectories (not single traces) to extract reusable procedural patterns
- **Validation gate + rejected-edit buffer**: candidate skills must improve on held-out set; rejected edits are cached to avoid repeated failures
- **Epoch-wise slow/meta update**: retains longer-horizon lessons across optimization steps
- Achieves 4,068 GitHub stars; +9.6 to +39.0 absolute gains across 6 diverse benchmarks

## Method
A frozen target model executes rollouts with the current skill. An optimizer model performs minibatch reflection over successes and failures, proposes bounded add/delete/replace edits ranked by expected utility, and clips to top-L_t edits (cosine schedule). Candidate skills are validated on a held-out set; rejected edits enter a buffer for negative feedback. The slow/meta update consolidates cross-step lessons. No target model weights are changed — only the textual skill evolves.

## Results
- GPT-5.5: +9.6 SearchQA, +38.9 Spreadsheet, +39.0 OfficeQA, +12.4 DocVQA, +29.3 LiveMath, +11.9 ALFWorld
- Outperforms TextGrad, GEPA, Trace2Skill, LLM skill, and human-written skills
- Zero deployment inference overhead (skill is just prepended text)
- Transfers across model sizes and harness types

## Connections
- Builds on: [[sources/skillos]], [[sources/skill1]], [[concepts/agents]]
- Related: [[sources/agentic-rl-reasoning]], [[sources/multi-turn-agent-rl]], [[sources/creativitybench]]
- Related concepts: [[concepts/agents]], [[concepts/structured-generation]]
- Organization: [[entities/orgs/microsoft]]

## Citation
> Yang et al., "SkillOpt: Executive Strategy for Self-Evolving Agent Skills," arXiv:2605.23904, 2026.
