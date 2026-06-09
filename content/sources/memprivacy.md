---
type: source
arxiv_id: "2605.09530"
title: "MemPrivacy: Privacy-Preserving Personalized Memory Management for Edge-Cloud Agents"
authors: ["Yining Chen", "Jihao Zhao", "Bo Tang", "Haofen Wang", "Feiyu Xiong", "Zhiyu Li"]
date: 2026-05-13
org: "MemTensor"
tags: [agents, privacy, memory, edge-cloud, safety, 2026]
upvotes: 147
---

# MemPrivacy: Privacy-Preserving Personalized Memory Management for Edge-Cloud Agents

> Type-aware placeholder system for agent memory that protects sensitive user data during cloud-assisted memory management while maintaining semantic integrity for effective personalization — addresses critical privacy gap in deployed agent systems.

## Key Contributions
- **Privacy taxonomy for agent memory**: categorizes sensitive information types in agent memory systems
- **Type-aware semantically structured placeholders**: replaces sensitive data with typed placeholders that preserve semantic structure for memory operations
- **Edge-cloud privacy split**: sensitive data stays on-device (edge); only anonymized semantics go to cloud for memory management
- **Maintained memory utility**: unlike aggressive masking that destroys task-relevant semantics, placeholders preserve operational meaning
- **100 GitHub stars** at MemTensor

## Method
MemPrivacy identifies that cloud-assisted memory management (needed for long-term agent adaptation) exposes sensitive user information. Existing privacy methods rely on aggressive masking that removes task-relevant semantics, degrading memory quality. MemPrivacy instead: (1) extracts privacy-sensitive information via a privacy taxonomy; (2) replaces it with type-aware placeholders that preserve semantic structure (e.g., "[LOCATION: home]" instead of the actual address); (3) cloud-side memory operations work on placeholder-augmented data; (4) re-hydration happens only on-device.

## Results
- Maintains high memory utility (personalization quality) while protecting privacy
- Minimal inference latency overhead from placeholder processing
- Low utility loss compared to aggressive masking baselines

## Connections
- Builds on: [[sources/mia-signature]], [[concepts/agents]], [[concepts/llm-safety]]
- Related: [[sources/skillsvote]], [[sources/agentdog-1-5]], [[concepts/long-context]]
- Fills gap: privacy infrastructure for deployed agent memory systems

## Citation
> Chen et al., "MemPrivacy: Privacy-Preserving Personalized Memory Management for Edge-Cloud Agents," arXiv:2605.09530, 2026.
