---
type: source
arxiv_id: "2505.11821"
title: "Reinforcing Multi-Turn Reasoning in LLM Agents via Turn-Level Credit Assignment"
authors: ["Siliang Zeng", "Quan Wei", "William Brown", "Oana Frunza", "Yuriy Nevmyvaka", "Mingyi Hong"]
date: 2025-05-19
org: "Morgan Stanley / University of Minnesota"
tags: [agents, rl, grpo, ppo, multi-turn, tool-use, credit-assignment, 2025]
upvotes: 14
---

# Reinforcing Multi-Turn Reasoning in LLM Agents via Turn-Level Credit Assignment

> The first systematic study of turn-level rewards in multi-turn RL for LLM agents — extending GRPO and PPO with fine-grained credit assignment across agent-environment interaction turns, achieving more stable training and higher accuracy.

## Key Contributions
- **Turn-level credit assignment**: Proposes MT-GRPO and MT-PPO algorithms that assign advantages at the granularity of individual turns rather than entire trajectories
- **Formal MDP framework**: Models multi-turn agent interaction as Markov Decision Processes with intermediate rewards at each turn
- **Turn-level reward design**: Both verifiable rewards (tool execution feedback) and LLM-as-judge rewards for flexible evaluation
- **Stable training**: MT-PPO achieves substantially more stable training, faster convergence, and near-perfect (99.9%) format correctness
- **Case study**: Reasoning-augmented search agent with multi-turn search and answer generation

## Method

### Multi-Turn Formulation
Multi-turn agent tasks are modeled as MDPs where each turn consists of:
- State s_k: Current context including tool results
- Action a_k: Tool call or reasoning output
- Reward R_k: Turn-level signal (retrieval quality, format correctness, etc.)

### MT-GRPO: Multi-Turn Group Relative Policy Optimization
For a two-turn setting with intermediate rewards {R_i^I} and outcome rewards {R_i^O}:
- First turn advantage: A_{i,1} = A_i^I + α·A_i^O
- Second turn advantage: A_{i,2} = A_i^O

Where A_i^I and A_i^O are computed by normalizing within each reward type's group.

**Limitation**: Requires G^(K-1) rollout samples for K turns — computationally prohibitive for long horizons.

### MT-PPO: Multi-Turn Proximal Policy Optimization
Uses a critic model for value estimation, avoiding the exponential sample complexity of MT-GRPO:
- More efficient and scalable for long-horizon tasks
- Leverages intermediate rewards via the critic's value function
- Achieves near-perfect format correctness (99.9%)

### Reward Design
Two types of turn-level rewards:
1. **Verifiable rewards**: Exact-match answer correctness, retrieval relevance
2. **LLM-as-judge rewards**: Flexible evaluation for nuanced turn quality

## Results

| Method | NQ (in-domain) | HotpotQA (in-domain) | Musique (OOD) | Format Correctness |
|---|---|---|---|---|
| GRPO (trajectory-level) | 0.391 | 0.306 | 0.129 | 0.534 |
| PPO (trajectory-level) | 0.483 | 0.382 | 0.199 | 0.895 |
| MT-PPO (turn-level) | **0.490** | **0.424** | **0.209** | **0.999** |

Key findings:
- MT-PPO consistently outperforms PPO and GRPO across all datasets
- Largest gains on multi-hop tasks (HotpotQA, Musique)
- Near-perfect format correctness — turn-level rewards stabilize structural correctness
- More stable training dynamics with faster early convergence
- Training curves show MT-PPO avoids the high variance and performance degradation seen in baseline PPO

## Datasets Used
- **NQ (Natural Questions)** — Single-hop general QA
- **TriviaQA** — Single-hop trivia
- **PopQA** — Single-hop factual QA
- **HotpotQA** — Two-hop reasoning
- **2WikiMultiHopQA** — Multi-hop Wikipedia QA
- **Musique** — Complex multi-hop QA

## Models Used
- Qwen2.5-7B as base model for all experiments

## Connections
- Builds on: [[sources/deepseek-r1|DeepSeek-R1]] (GRPO), [[sources/agentic-rl-reasoning|Agentic RL Reasoning]] (agentic RL paradigm), [[sources/react|ReAct]] (agent reasoning loop)
- Cited by / Influenced: Advances multi-turn agent RL with principled credit assignment
- Related concepts: [[concepts/agents|Agents & Tool Use]], [[concepts/grpo|GRPO]], [[concepts/rlhf|RLHF]]
- Related papers: [[sources/codeact|CodeAct]] (code-as-actions), [[sources/swe-rl|SWE-RL]] (RL on real trajectories)

## Citation
> Zeng et al., "Reinforcing Multi-Turn Reasoning in LLM Agents via Turn-Level Credit Assignment," arXiv:2505.11821, 2025.
