---
type: source
arxiv_id: "2605.20025"
title: "AutoResearchClaw: Self-Reinforcing Autonomous Research with Human-AI Collaboration"
authors: ["Jiaqi Liu", "Shi Qiu", "Mairui Li", "Bingzhou Li", "Haonian Ji", "Siwei Han", "Xinyu Ye", "Peng Xia", "Zihan Dong", "Congyu Zhang"]
date: 2026-05-20
org: "AIMING Lab"
tags: [agents, autonomous-research, multi-agent, scientific-discovery, 2026]
upvotes: 185
---

# AutoResearchClaw: Self-Reinforcing Autonomous Research with Human-AI Collaboration

> Multi-agent autonomous research system with structured debate, self-healing execution, cross-run evolution, and human-in-the-loop collaboration — achieves 13,071 GitHub stars and outperforms AI Scientist v2 on ARC-Bench.

## Key Contributions
- **Structured multi-agent debate**: hypotheses are challenged from multiple perspectives before experiments
- **Self-healing executor**: experiments that fail inform the next attempt rather than terminating the pipeline
- **Pivot/Refine decision loop**: system decides whether to refine current hypothesis or pivot to a new one based on experimental evidence
- **Verifiable result reporting**: all conclusions are grounded in reproducible experimental results
- **Cross-run evolution**: lessons accumulate across research cycles, unlike single-shot systems
- **Human-in-the-loop collaboration**: maintains human oversight at key decision points
- Outperforms AI Scientist v2 and previous autonomous research systems on ARC-Bench

## Method
AutoResearchClaw models the research process as iterative cycles of hypothesis generation (via multi-agent debate), experimental execution (with self-healing on failure), result verification, and decision-making (pivot or refine). A memory system carries experience across runs, and human collaboration points allow intervention at critical junctures. The system does not treat research as a linear pipeline but as an iterative process with feedback loops.

## Results
- Outperforms AI Scientist v2 on ARC-Bench across multiple scientific domains
- 13,071 GitHub stars indicating strong community adoption
- Successfully completes multi-cycle research projects with accumulating insights
- Maintains research quality while reducing human intervention to key checkpoints

## Connections
- Builds on: [[sources/auto-research-agents]], [[sources/intern-atlas]], [[sources/agent-native-research-artifact]]
- Related: [[sources/ai-co-mathematician]], [[sources/eywa]], [[concepts/multi-agent-systems]]
- Related concepts: [[concepts/agents]], [[comparisons/code-models-agents]]

## Citation
> Liu et al., "AutoResearchClaw: Self-Reinforcing Autonomous Research with Human-AI Collaboration," arXiv:2605.20025, 2026.
