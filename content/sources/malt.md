---
type: source
arxiv_id: "2412.01928"
title: "MALT: Improving Reasoning with Multi-Agent LLM Training"
authors: ["Sumeet Ramesh Motwani", "Chandler Smith", "Rocktim Jyoti Das", "Markian Rybchuk"]
date: 2024-12-02
org: "University of Oxford / Various"
tags: [multi-agent, reasoning, rl, training, 2024]
upvotes: 46
---

# MALT: Multi-Agent LLM Training

> First framework for jointly training multiple LLMs to collaborate on reasoning tasks, achieving significant improvements over single-model approaches.

## Key Contributions
- Introduced **MALT** (Multi-Agent LLM Training), the first framework for training multiple LLMs to work together on tasks
- Defined **specialized roles**: Generator (produces answers), Verifier (checks correctness), Refiner (improves wrong answers)
- Proposed **trajectory-expansion** and **credit assignment** strategies to generate diverse training data
- Achieved **~15% improvement on MATH** and ~14% on GSM8K over single-agent baselines using Llama 3.1 8B
- Demonstrated that **jointly trained agents outperform independently trained ones** — cooperation emerges from joint reward signals

## Method
MALT trains three specialized LLMs in a sequential pipeline:
1. **Generator**: Produces initial solutions to reasoning problems
2. **Verifier**: Evaluates whether the generator's solution is correct
3. **Refiner**: Takes incorrect solutions + verification feedback and produces improved answers

Training uses **joint outcome-based rewards**: all three models receive reward based on the final answer quality, not just their individual outputs. This incentivizes cooperation.

**Trajectory expansion**: For each problem, sample multiple generator outputs, creating diverse trajectories. The verifier and refiner see different trajectories, increasing training diversity.

**Credit assignment**: A novel strategy attributes the final outcome back to each agent's contribution, enabling more targeted optimization.

## Results
- **MATH**: 64.9% (MALT) vs 50.0% (single Llama-3.1-8B), ~15 point improvement
- **GSM8K**: 91.3% (MALT) vs 77.0% (single), ~14 point improvement
- **CQA (CommonsenseQA)**: 78.2% (MALT) vs 72.0% (single)
- Jointly trained agents consistently outperform agents trained independently for each role
- Multi-agent pipeline outperforms self-refinement (one model doing all roles)

## Models Released
- Llama 3.1 8B-based Generator, Verifier, and Refiner checkpoints

## Connections
- **Builds on**: [[sources/llama-3|Llama 3]], [[concepts/chain-of-thought|Chain-of-Thought]], [[concepts/reward-modeling|Reward Modeling]]
- **Related**: [[sources/mixture-of-agents|Mixture-of-Agents]] (inference-time multi-agent), [[sources/open-reasoner-zero|Open-Reasoner-Zero]] (single-agent RL reasoning)
- **Related concepts**: [[concepts/agents|LLM Agents]], [[concepts/rlhf|RLHF]], [[concepts/grpo|GRPO]]
- **Influenced**: Multi-agent training paradigm for reasoning tasks

## Citation
> Motwani et al., "MALT: Improving Reasoning with Multi-Agent LLM Training," arXiv:2412.01928, 2024.
