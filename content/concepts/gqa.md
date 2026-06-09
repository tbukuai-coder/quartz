---
type: concept
tags: [architecture, efficiency]
---

# Grouped-Query Attention (GQA)

> A middle ground between Multi-Head Attention and Multi-Query Attention — **groups of query heads share a single KV head**, reducing KV cache memory while preserving quality.

## Overview
Standard Multi-Head Attention (MHA) gives each head its own Q, K, V projections. Multi-Query Attention (MQA) shares K, V across all heads — fast but quality loss. GQA groups query heads and assigns each group a shared KV head. This achieves most of MQA's speed with minimal quality loss.

## Configuration Examples
| Method | Heads | KV Heads | Ratio | Used By |
|---|---|---|---|---|
| MHA | 32 | 32 | 1:1 | BERT, GPT-2 |
| GQA | 32 | 8 | 4:1 | [[entities/models/mistral|Mistral]], [[entities/models/llama|Llama 2+]], [[entities/models/qwen|Qwen]] |
| MQA | 32 | 1 | 32:1 | PaLM, Falcon |

## Why It Matters
During inference, the **KV cache** (stored key-value states for all tokens) dominates memory. GQA reduces KV cache by the grouping ratio (4× with 4:1 ratio), enabling:
- Larger batch sizes
- Longer sequences
- Faster inference

## Key Papers
- [[sources/mistral-7b]] — Uses GQA (8 KV heads for 32 query heads)
- [[sources/llama-2]] — Adopted GQA from Llama 2 70B onward

## See Also
- [[concepts/self-attention]]
- [[concepts/swa]]
- [[concepts/transformer-architecture]]
