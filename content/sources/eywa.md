---
type: source
arxiv_id: "2604.27351"
title: "Eywa: A Heterogeneous Agentic Framework for Scientific Foundation Model Collaboration"
authors: ["Zihao Li", "Jiaru Zou", "Feihao Fang", "Xuying Ning", "Mengting Ai", "Tianxin Wei", "Sirui Chen", "Xiyuan Yang", "Jingrui He"]
date: 2026-04-21
org: "University of Illinois Urbana-Champaign"
tags: [multimodal, agents, scientific-ai, multi-agent-systems, 2026]
upvotes: 193
---

# Eywa: Heterogeneous Agentic Framework for Scientific Foundation Model Collaboration

> A heterogeneous agentic framework that extends language-centric LLM systems to scientific foundation models by integrating domain-specific models with language-based reasoning interfaces, inspired by the Avatar Pandora ecosystem analogy.

## Key Contributions

- **EywaAgent**: Augments domain-specific foundation models with an FM-LLM "Tsaheylu" interface, allowing language agents to guide inference, planning, and decision-making on specialized scientific tasks
- **EywaMAS**: Multi-agent extension where EywaAgents replace existing language agents in multi-agent systems
- **EywaOrchestra**: Planning-based orchestration framework where a central planner dynamically coordinates both language agents and EywaAgents
- **EywaBench**: New benchmark spanning physical, life, and social sciences for evaluating heterogeneous agentic systems

## Method

Inspired by Avatar's Tsaheylu (neural bond for cross-species communication), Eywa addresses the limitation that many scientific foundation models (for symbolic data, time series, molecular structures) do not natively support language as input/output modality.

The three-stage framework:
1. **EywaAgent** builds an FM-LLM interface, augmenting domain-specific FMs with language-based reasoning
2. **EywaMAS** enables collaboration between EywaAgents and conventional LLM agents
3. **EywaOrchestra** dynamically orchestrates across heterogeneous experts with a central planner

## Results

- EywaAgent improves utility by ~7% across physical, life, and social science tasks while reducing token usage by ~30% and execution time by ~10%
- EywaMAS improves utility while reducing token and time usage in multi-agent settings
- EywaOrchestra dynamically orchestrates heterogeneous models and improves over single-agent and multi-agent baselines

## Connections
- Builds on: [[sources/react]], [[sources/toolformer]], [[sources/codeact]], [[sources/multi-turn-agent-rl]]
- Related concepts: [[concepts/agents]], [[concepts/multi-agent-systems]], [[concepts/multimodal-models]]
- Cited by / Influenced: Emerging work on scientific AI agents

## Citation
> Li et al., "Eywa: A Heterogeneous Agentic Framework for Scientific Foundation Model Collaboration," arXiv:2604.27351, 2026.
