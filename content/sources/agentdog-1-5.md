---
type: source
arxiv_id: "2605.29801"
title: "AgentDoG 1.5: A Lightweight and Scalable Alignment Framework for AI Agent Safety and Security"
authors: ["Dongrui Liu", "Yu Li", "Zhonghao Yang", "Peng Wang", "Guanxu Chen", "Yuejin Xie", "Qinghua Mao", "Wanying Qu", "Yanxu Zhu", "Tianyi Zhou"]
date: 2026-05-29
org: "Multi-institution"
tags: [agents, safety, alignment, guardrails, 2026]
upvotes: 134
---

# AgentDoG 1.5: A Lightweight and Scalable Alignment Framework for AI Agent Safety and Security

> Lightweight agent safety alignment framework with updated taxonomy for emergent risks, influence-function purification for efficient SFT data selection, Docker-level RL environments, and real-time online guardrail for interactive agentic scenarios.

## Key Contributions
- **Updated agent safety taxonomy**: accommodates emergent risks from Codex-era agents operating in open environments
- **Influence-function purification**: efficiently selects minimal SFT samples for safety alignment without large-scale annotation
- **Docker-level RL training environments**: realistic sandboxed environments for safety-aware RL training
- **Online guardrail**: real-time safety moderation for interactive agentic scenarios
- **Lightweight and scalable**: minimal samples needed, deploys efficiently in production

## Method
AgentDoG 1.5 addresses the gap between agent capability (cross-environment execution) and safety alignment. The framework: (1) defines an updated safety taxonomy covering new risk categories from advanced agents; (2) uses influence-function purification to select the most informative safety training examples from large pools; (3) trains with agentic safety SFT in Docker-level sandboxed environments; (4) deploys a real-time online guardrail for production agent systems that monitors and intervenes during execution.

## Results
- Effective safety alignment with minimal training samples
- Real-time guardrail with low latency overhead
- Covers broad spectrum of agent safety risks (tool misuse, data exfiltration, unauthorized access)

## Connections
- Builds on: [[sources/xl-safetybench]], [[sources/benchmarkless-safety-scoring]], [[concepts/llm-safety]]
- Related: [[sources/memprivacy]], [[sources/skillsvote]], [[concepts/agents]]
- Fills gap: production-ready safety infrastructure for deployed agents

## Citation
> Liu et al., "AgentDoG 1.5: A Lightweight and Scalable Alignment Framework for AI Agent Safety and Security," arXiv:2605.29801, 2026.
