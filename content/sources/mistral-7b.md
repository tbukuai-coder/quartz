---
type: source
arxiv_id: "2310.06825"
title: "Mistral 7B"
authors: ["Albert Q. Jiang", "Alexandre Sablayrolles", "Arthur Mensch", "et al."]
date: 2023-10-10
org: "Mistral AI"
tags: [open-models, efficiency, architecture, 2023]
upvotes: 58
---

# Mistral 7B

> A 7B-parameter model that **outperforms Llama 2 13B on all benchmarks** and Llama 1 34B on reasoning/math/code, using architectural innovations for efficiency.

## Key Contributions
- Demonstrated that careful architecture design can make a 7B model outperform 13B+ models
- Introduced **Sliding Window Attention (SWA)** for efficient long-sequence handling
- Used **Grouped-Query Attention (GQA)** for faster inference
- Released under Apache 2.0 license — fully permissive
- Also released Mistral 7B Instruct (fine-tuned for instruction following)

## Method
Architecture based on the LLaMA design with key additions:
- **Sliding Window Attention (SWA)**: Each layer attends to a fixed window of W=4096 previous tokens. With 32 layers, information can propagate across 32×4096 = 131K tokens — enabling theoretically unbounded sequence lengths with fixed compute
- **Grouped-Query Attention (GQA)**: 8 KV heads shared across 32 query heads (4:1 ratio), reducing KV cache size and accelerating inference
- **Rolling Buffer Cache**: Fixed-size KV cache that overwrites old entries, bounding memory usage

Training details were not disclosed in the paper.

## Results
- Outperforms **Llama 2 13B** on all benchmarks (2× smaller)
- Outperforms **Llama 1 34B** on reasoning, math, and code generation (5× smaller)
- Competitive with **Llama 2 34B** (code-specific) on code benchmarks

## Connections
- **Builds on**: [[sources/llama]] (architecture base), [[sources/attention-is-all-you-need]]
- **Extended by**: [[sources/mixtral]] (MoE version)
- **Used as base for**: [[sources/zephyr]] (alignment fine-tuning)
- **Key concepts**: [[concepts/gqa]], [[concepts/swa]], [[concepts/transformer-architecture]]
- **Models**: [[entities/models/mistral]]
- **Organizations**: [[entities/orgs/mistral-ai]]

## Citation
> Jiang et al., "Mistral 7B," arXiv:2310.06825, 2023.
> https://huggingface.co/papers/2310.06825
