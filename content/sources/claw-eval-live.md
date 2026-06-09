---
type: source
arxiv_id: "2604.28139"
title: "Claw-Eval-Live: A Live Agent Benchmark for Evolving Real-World Workflows"
authors: ["Chenxin Li", "Zhengyang Tang", "Huangxin Lin", "Yunlong Lin", "Shijue Huang", "Shengyuan Liu", "Bowen Ye", "Rang Li", "Lei Li", "Benyou Wang"]
date: 2026-04-25
org: "Shenzhen University / CUHK"
tags: [agents, benchmarking, evaluation, workflow-agents, 2026]
upvotes: 31
---

# Claw-Eval-Live: Live Agent Benchmark for Evolving Real-World Workflows

> A dynamic benchmark for workflow agents that sources tasks from public workflow signals and evaluates both service-backed workflows and workspace repair, with quarterly refresh cycles to track evolving demands.

## Key Contributions

- **Live benchmark snapshot**: 105 tasks, 13 public models, 18 controlled services + sandboxed workspaces — refreshed quarterly from public signals
- **Signal-to-task release pipeline**: Maps ClawHub Top-500 signals into benchmark tasks through clustering, weighting, seed expansion, and discrimination-aware selection from 157 runnable candidates
- **Action-grounded hybrid grading**: Evaluates agents on observable execution evidence (audit logs, traces) rather than final-text plausibility alone
- **Dual-calibration design**: Task distribution stays close to evolving real-world workflows; scores anchored in execution evidence

## Method

Addresses two problems in agent benchmarks:
1. **Static task mixtures become stale**: Tool stacks evolve, enterprise bottlenecks shift — fixed benchmarks drift from current needs
2. **Final-text evaluation is insufficient**: Polished memos don't prove agents queried correct records or changed right state

Claw-Eval-Live separates a refreshable signal layer from a fixed execution layer, grading from observable traces rather than final responses.

## Results

- Best model passes only **66.7% of tasks**
- Service-backed workflows remain substantially harder than workspace repair
- Several business-critical workflow families remain far from solved

## Connections
- Builds on: [[sources/web2bigtable]], [[sources/interactweb-bench]], [[concepts/agents]], [[concepts/llm-evaluation]]
- Related comparisons: [[comparisons/reasoning-models]]
- Cited by / Influenced: Agent evaluation and deployment practices

## Citation
> Li et al., "Claw-Eval-Live: A Live Agent Benchmark for Evolving Real-World Workflows," arXiv:2604.28139, 2026.
