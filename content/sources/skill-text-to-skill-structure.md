---
type: source
arxiv_id: "2604.24026"
title: "From Skill Text to Skill Structure: The Scheduling-Structural-Logical Representation for Agent Skills"
authors: ["Unknown"]
date: 2026-04-17
org: "Unknown"
tags: [agents, skill-representation, structured-generation, agent-safety, 2026]
upvotes: 5
---

# SSL Representation: Scheduling-Structural-Logical Representation for Agent Skills

> A three-layer structured representation (Scheduling-Structural-Logical) that disentangles agent skill artifacts into goal-level context, execution trajectory, and primitive operations — improving skill discovery and risk assessment.

## Key Contributions

- **SSL representation**: First structured representation designed specifically for disentangling agent skill artifacts, inspired by Schank & Abelson's classical work on linguistic knowledge representation
- **Three-layer JSON graph**:
  - **Scheduling layer** (Memory Organization Packets): Goal-oriented organizers for retrieving and contextualizing experience
  - **Structural layer** (Script Theory): Ordered scenes with expectations and transitions
  - **Logical layer** (Conceptual Dependency): Primitive action structures abstracting away from surface wording
- **LLM-based normalizer**: Converts existing SKILL.md files into SSL schema while remaining paired with original source
- **Release-ready datasets**: 6,184-skill corpus, 403 task-grounded queries, 500 skills with six-dimensional risk labels

## Results

- **Skill Discovery**: SSL-derived description improves retrieval MRR from 0.573 → **0.707** (+23.4%)
- **Risk Assessment**: SKILL.md + SSL view improves macro F1 from 0.744 → **0.787** (+5.8%)
- Exposes useful evidence across distinct skill-centered tasks while complementing original text

## Connections
- Builds on: [[sources/web2bigtable]], [[concepts/agents]], [[concepts/structured-generation]]
- Related concepts: [[concepts/llm-safety]], [[concepts/multi-agent-systems]]
- Related papers: [[sources/react]], [[sources/codeact]], [[sources/toolformer]]
- Cited by / Influenced: Agent skill registries, reusable agent capabilities, agent security

## Citation
> "From Skill Text to Skill Structure: The Scheduling-Structural-Logical Representation for Agent Skills," arXiv:2604.24026, 2026.
