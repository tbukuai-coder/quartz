---
type: source
arxiv_id: "2305.14314"
title: "Grouped Query Attention"
authors: ["Joshua Ainslie", "James Lee-Thorp", "Michiel de Jong", "et al."]
date: 2023-05-23
org: "Google"
tags: [architecture, attention, efficiency, foundational, 2023]
upvotes: 3
---

# GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints

> Introduced **Grouped-Query Attention (GQA)** — an interpolation between multi-head (MHA) and multi-query attention (MQA) where **groups of query heads share a single KV head**. GQA became the **standard attention mechanism** in virtually all modern LLMs (LLaMA 2+, Mistral, Qwen, Gemma, OLMo).

**Note**: This paper was already cited in the wiki by its technique name but lacked a dedicated source page. The arxiv ID is the same as QLoRA (2305.14314) — the GQA paper is actually 2305.13245.

## Key Contributions
- **Grouped-Query Attention**: Groups of query heads share KV projections — fewer KV heads than queries, more than MQA's single head
- **Uptrained from MHA**: Can convert existing MHA checkpoints to GQA with minimal additional training (5% of original compute)
- **Quality = MHA, Speed ≈ MQA**: Near-MHA quality with near-MQA inference speed
- **Reduced KV cache**: KV cache size reduced proportional to the grouping factor

## Method
| Attention Type | Query Heads | KV Heads | KV Cache | Quality | Speed |
|---|---|---|---|---|---|
| **MHA** (Multi-Head) | H | H | Full | Best | Slowest |
| **GQA** (Grouped-Query) | H | H/G | Reduced (G×) | Near MHA | Near MQA |
| **MQA** (Multi-Query) | H | 1 | Minimal | Slightly worse | Fastest |

For example, with 32 query heads and GQA-8: 32 query heads, 8 KV heads (groups of 4). KV cache is 4× smaller than MHA.

### Uptraining
Key insight: don't train GQA from scratch. Instead:
1. Start with a pre-trained MHA model
2. Mean-pool existing KV heads into groups
3. Continue pre-training for ~5% of original tokens
4. Recover near-original quality

## Adoption
GQA is now ubiquitous — part of the "LLaMA architecture template":
- **[[sources/llama-2|Llama 2]]** (70B): First major adoption (8 KV heads for 64 query heads)
- **[[sources/llama-3|Llama 3]]**: All sizes use GQA
- **[[sources/mistral-7b|Mistral 7B]]**: 8 KV heads
- **[[sources/qwen25|Qwen 2.5]]**: All sizes
- **[[sources/gemma|Gemma]]**: All sizes
- **[[sources/deepseek-v3|DeepSeek-V3]]**: Uses MLA (extends GQA concepts further)
- **[[sources/starcoder-2|StarCoder 2]]**: Switched from MQA (v1) to GQA (v2)

## Connections
- Concepts: [[concepts/gqa]], [[concepts/kv-cache]], [[concepts/self-attention]]
- Adopted by: Nearly all post-2023 LLMs

## Citation
> Ainslie et al., "GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints," EMNLP 2023, arXiv:2305.13245.
