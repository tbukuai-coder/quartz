---
type: source
arxiv_id: "2508.10925"
title: "gpt-oss-120b & gpt-oss-20b Model Card"
authors: ["OpenAI"]
date: 2025-08-14
org: "OpenAI"
tags: [open-model, moe, reasoning, frontier, 2025]
upvotes: 20
---

# GPT-OSS (gpt-oss-120b / gpt-oss-20b)

> OpenAI's first open-weight models — MoE reasoning models with 120B and 20B parameters, released under an open license. A historic shift for the company.

## Key Contributions
- **OpenAI's first open-weight release** — a milestone shift from the company that defined closed-source AI
- Released **gpt-oss-120b** (MoE) and **gpt-oss-20b** (dense) under permissive license
- MoE architecture with efficient **mixture-of-expert transformer** design
- Trained with **large-scale distillation** from proprietary models + **reinforcement learning**
- Includes **agentic capabilities** including deep research and browsing

## Method
Both models use a Transformer architecture. The 120B model is a Mixture-of-Experts design, while the 20B is dense. Training involves:
1. **Large-scale distillation**: Knowledge distilled from proprietary o-series models
2. **Reinforcement learning**: Further refined with RL for reasoning and instruction following
3. **Agentic training**: Optimized for tool use, research, and multi-step reasoning

## Results
- **gpt-oss-120b**: Competitive with LLaMA-3-70B and Qwen2.5-72B on standard benchmarks
- **gpt-oss-20b**: Outperforms 120B on some tasks (better efficiency), competitive with smaller frontier models
- Strong performance on code generation (HumanEval), reasoning (MMLU, GPQA), and agentic tasks

## Models Released
- gpt-oss-120b (MoE, open weights)
- gpt-oss-20b (dense, open weights)

## Connections
- **From**: [[entities/orgs/openai|OpenAI]] — first open release
- **Architecture**: [[concepts/mixture-of-experts|Mixture of Experts]]
- **Competes with**: [[sources/llama-3|Llama 3]], [[sources/qwen25|Qwen2.5]], [[sources/deepseek-v3|DeepSeek-V3]]
- **Historic significance**: OpenAI joining the open-weight ecosystem changes the competitive landscape

## Citation
> OpenAI, "gpt-oss-120b & gpt-oss-20b Model Card," 2025.
