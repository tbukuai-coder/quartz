---
type: source
arxiv_id: "2605.06200"
title: "A^2TGPO: Agentic Turn-Group Policy Optimization with Adaptive Turn-level Clipping"
authors: ["Dingwei Chen", "Zefang Zong", "Zhipeng Ma", "Leo Luo", "Yang Li", "Chengming Li", "Peng Chen", "Jie Jiang"]
date: 2026-05
tags: [reinforcement-learning, agents, grpo, tool-use, multi-turn, credit-assignment, agentic-llm]
upvotes: 7
---

# A²TGPO: Agentic Turn-Group Policy Optimization with Adaptive Turn-level Clipping

> Addresses sparse trajectory-level rewards and process credit assignment in agentic LLM reinforcement learning through adaptive turn-level clipping, information gain normalization, and variance-rescaled discounted accumulation.

## Key Contributions
- Tackles the sparse reward and credit assignment problem for agentic LLMs that make multi-turn tool calls
- Existing approaches either require separate external process reward models (adding overhead) or use tree-based structural rollouts (constraining trajectory diversity)
- Proposes A²TGPO (Agentic Turn-Group Policy Optimization) with three key innovations:
  1. **Information Gain normalization**: Normalizes rewards by the information gained from each turn
  2. **Variance-rescaled discounted accumulation**: Adjusts discounting based on reward variance across the trajectory
  3. **Adaptive turn-level clipping**: Clips policy updates at the turn level rather than the sequence level

## Method
A²TGPO adapts GRPO for multi-turn agentic scenarios:
1. **Turn-level grouping**: Groups rollout samples by turn rather than by full trajectory
2. **Information gain**: Measures how much each tool call contributes to solving the task, normalizing rewards
3. **Variance rescaling**: High-variance turns get more conservative updates; low-variance turns get more aggressive updates
4. **Adaptive clipping**: The clipping threshold ε adapts per-turn based on turn-level statistics

This avoids the limitations of:
- External PRMs (additional model overhead)
- Tree-based rollouts (constrained trajectory diversity)
- Standard GRPO (poor credit assignment for multi-turn interactions)

## Results
- Improved policy optimization for tool-using LLM agents
- Better credit assignment across multi-turn interactions
- More stable training for agentic RL

## Datasets Used
- Multi-turn agent benchmarks with tool use

## Models Released
- GitHub: https://github.com/CuSO4-Chen/A-TGPO (1 star)

## Connections
- Builds on: [[sources/deepseek-r1]], [[concepts/grpo]] — GRPO foundation
- Related: [[sources/agentic-rl-reasoning]] — RL for tool-using agents
- Related: [[sources/multi-turn-agent-rl]] — turn-level credit assignment
- Related: [[sources/eywa]] — heterogeneous agentic framework
- Related concept: [[concepts/agents]], [[concepts/grpo]]

## Citation
> Chen et al., "A²TGPO: Agentic Turn-Group Policy Optimization with Adaptive Turn-level Clipping," arXiv:2605.06200, 2026.
