---
type: entity
category: org
tags: [together-ai, infrastructure, open-source, redpajama]
---

# Together AI

> An AI infrastructure company focused on making **open-source AI accessible** — creators of [[entities/datasets/redpajama|RedPajama]] (the first open reproduction of LLaMA's training data), the Together Inference Engine, and contributors to key open research including FlashAttention, Mixture-of-Agents, and open model training at scale.

## Overview
Together AI (formerly Together Computer) bridges the gap between open-source model research and practical deployment. Founded by researchers including Tri Dao (co-author of [[concepts/flash-attention|FlashAttention]]) and Ce Zhang, the company operates on two fronts: (1) advancing open-source AI research through data, models, and infrastructure contributions, and (2) providing a cloud platform for efficient inference and fine-tuning of open models. Their RedPajama project was a pivotal moment in open-source AI, enabling the community to train LLMs on a fully open data recipe.

## Key Contributions

### Datasets
- **[[entities/datasets/redpajama|RedPajama-Data-1T]]** (2023): First open reproduction of the LLaMA training data recipe — 1.2T tokens from Common Crawl, C4, GitHub, Wikipedia, books, ArXiv, StackExchange. 1,100+ likes on HF Hub.
- **RedPajama-Data-V2** (2023): Massively expanded to 30T+ tokens across 5 languages (en, de, fr, es, it) with quality signals for custom filtering. 400+ likes.

### Models
- **RedPajama-INCITE** (2023): 3B and 7B models trained on RedPajama-1T — base, instruct, and chat variants (Apache 2.0)
- **GPT-JT-6B** (2022): Early instruction-tuned model combining GPT-J with chain-of-thought and P3 data
- **LLaMA-2-7B-32K** (2023): Extended Llama 2 to 32K context (538 likes)
- **Evo** (2024): Genomics foundation model using StripedHyena (hybrid SSM architecture)

### Research & Infrastructure
- **FlashAttention**: Tri Dao (Together AI co-founder) is the creator of [[concepts/flash-attention|FlashAttention]], the IO-aware exact attention algorithm now standard in all LLM training
- **[[sources/mixture-of-agents|Mixture-of-Agents (MoA)]]** (2024): Multi-agent architecture where open-source LLMs collectively surpass GPT-4o on AlpacaEval 2.0 (65.1% vs 57.5%)
- **Together Inference Engine**: High-performance inference platform for open models

## Philosophy
Together AI represents a distinct approach in the AI industry: building commercial infrastructure while actively contributing open datasets and models. Their RedPajama project demonstrated that corporate actors can drive open-source progress — the dataset enabled dozens of downstream models and research projects that would not have been possible without open training data.

## Papers in This Wiki
- [[sources/mixture-of-agents]] — Mixture-of-Agents: open LLMs collectively surpass GPT-4o

## See Also
- [[entities/datasets/redpajama]] — RedPajama dataset
- [[concepts/flash-attention]] — FlashAttention
- [[concepts/multi-agent-systems]] — Multi-Agent LLM Systems
- [[concepts/training-infrastructure]] — Training at scale
- [[concepts/llm-serving]] — Inference infrastructure
- [[comparisons/pretraining-data]] — Data strategy comparison
