---
type: source
arxiv_id: "2604.27251"
title: "Compliance versus Sensibility: On the Reasoning Controllability in Large Language Models"
authors: ["Xingwei Tan", "and colleagues"]
date: 2026-04-21
org: "Unknown"
tags: [chain-of-thought, reasoning, steering, mechanistic-interpretability, safety, 2026]
upvotes: 5
---

# Compliance vs. Sensibility: Reasoning Controllability in LLMs

> First rigorous assessment of reasoning conflicts in LLMs — when user reasoning instructions conflict with models' internal priors — with mechanistic analysis and steering-based mitigation via Contrastive Activation Addition.

## Key Contributions

- **Reasoning conflict identification**: Models face tension between instruction compliance (reason as instructed) and logical sensibility (reason as question demands)
- **Comprehensive evaluation**: First rigorous assessment across 3 open-source families + 2 frontier models on 4 datasets spanning deduction, induction, and abduction
- **Mechanistic analysis**: LLMs encode and understand reasoning instructions in middle-to-late layers; compliance/divergence decision is an active mid-computation process
- **Steering mitigation**: Contrastive Activation Addition (CAA) enhances reasoning compliance by up to **29%**

## Method

Evaluates whether CoT reasoning derives from generalizable capabilities or remains tied to pre-training tasks. Tests what happens when user specifies a reasoning strategy (deduction/induction/abduction) that conflicts with the problem's natural strategy.

## Results

- Reasoning conflicts are widespread and systematic across models
- Models often prioritize task-appropriate patterns over explicit instructions
- Steering mechanisms can significantly improve compliance without retraining

## Connections
- Builds on: [[sources/meta-abilities-alignment]], [[concepts/chain-of-thought]], [[sources/reasoning-vectors]]
- Related concepts: [[concepts/llm-safety]], [[concepts/structured-generation]]
- Related papers: [[sources/deepseek-r1]], [[sources/s1]]

## Citation
> Tan et al., "Compliance versus Sensibility: On the Reasoning Controllability in Large Language Models," arXiv:2604.27251, 2026.
