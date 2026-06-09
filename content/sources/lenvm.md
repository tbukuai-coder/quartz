---
type: source
arxiv_id: "2604.27039"
title: "Length Value Model: Scalable Value Pretraining for Token-Level Length Modeling"
authors: ["Eric AI Lab"]
date: 2026-04-19
org: "Unknown"
tags: [length-control, autoregressive-models, value-estimation, efficiency, llm-training, 2026]
upvotes: 19
---

# Length Value Model (LenVM): Token-Level Length Modeling

> A token-level framework that models remaining generation length as a value estimation problem, enabling fine-grained length control and interpretable generation dynamics in LLMs and VLMs.

## Key Contributions

- **Token-level length modeling**: Treats generation length as value estimation rather than coarse sequence-level prediction
- **Annotation-free supervision**: Constant negative reward per token yields dense, unbiased, scalable training signal
- **Inference-time length control**: Predicts remaining generation length from prompt boundary, enables continuous performance-efficiency trade-off
- **Interpretable generation dynamics**: Token-level values reveal how specific tokens shift reasoning toward shorter or longer regimes

## Method

Formulates length modeling as RL value estimation:
- Each generated token receives constant negative reward
- Predicts bounded, discounted return as monotone proxy for remaining generation horizon
- No human annotations needed — fully self-supervised from autoregressive training

## Results

- **LIFEBench exact length matching**: 7B model score improves from 30.9 → 64.8, outperforming frontier closed-source models
- **GSM8K at 200-token budget**: 63% accuracy vs 6% for token budget baseline
- Accurately predicts total generation length from prompt boundary
- Provides interpretable view of how reasoning length evolves token-by-token

## Connections
- Builds on: [[concepts/chain-of-thought]], [[concepts/test-time-compute]], [[sources/deepconf]]
- Related concepts: [[concepts/rlhf]], [[concepts/sampling-strategies]]
- Related papers: [[sources/interleaved-reasoning]], [[sources/repro]]
- Cited by / Influenced: Efficient reasoning, length-aware RL training

## Citation
> "Length Value Model: Scalable Value Pretraining for Token-Level Length Modeling," arXiv:2604.27039, 2026.
