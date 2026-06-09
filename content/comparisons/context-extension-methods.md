---
type: comparison
tags: [long-context, positional-encodings, architecture, 2024, 2025]
---

# Context Extension Methods: From 4K to 2M+ Tokens

> Comparing approaches to extending LLM context windows — positional interpolation (YaRN, LongRoPE), efficient attention, and alternative architectures.

## Overview
Extending LLM context beyond training length is critical for real-world applications. Multiple approaches exist, each with different tradeoffs in training cost, quality preservation, and maximum extension.

## Positional Interpolation Methods

| Method | Year | Max Extension | Fine-tune Steps | Short-Context Loss | Key Idea |
|---|---|---|---|---|---|
| Position Interpolation | 2023 | ~4× (4K→16K) | Full retraining | Moderate | Linear RoPE scaling |
| NTK-Aware | 2023 | ~8× | Moderate | Low | Per-frequency scaling |
| [[sources/yarn\|YaRN]] | 2023 | ~64× (4K→128K) | **10× fewer tokens** | Low | NTK + dynamic + temperature |
| [[sources/longrope\|LongRoPE]] | 2024 | **512× (4K→2M)** | **1K steps** | Moderate→fixed | Non-uniform per-dimension search |
| [[sources/longrope2\|LongRoPE2]] | 2025 | ~32× (4K→128K) | **30-50% fewer than LongRoPE** | **<0.5%** | Simplified search + mixed training |

## Training-Based Approaches

| Method | Year | Key Finding | Cost |
|---|---|---|---|
| [[sources/prolong\|ProLong]] | 2024 | Long-context SFT data matters more than long pretraining | Moderate |
| Llama 3.1 | 2024 | Native 128K via massive pretraining | Very high |
| Qwen2.5-1M | 2025 | YaRN-based extension to 1M tokens | High |

## Alternative Architectures

| Architecture | Context Scaling | Inference Cost | Maturity |
|---|---|---|---|
| [[sources/mamba\|Mamba/SSM]] | O(n) linear | Low | Growing |
| [[sources/jamba\|Jamba]] | O(n) + O(n²) hybrid | Medium | Production |
| [[sources/nemotron-h\|Nemotron-H]] | Hybrid | Low (3× faster) | New |
| Ring Attention | O(n²) distributed | High | Research |

## Key Insights
1. **YaRN is the practical standard** — used by Qwen, DeepSeek, Mistral for production models
2. **LongRoPE pushed the frontier** to 2M tokens but requires careful fine-tuning
3. **LongRoPE2 optimizes for quality** — near-lossless at shorter extensions
4. **ProLong shows SFT data matters** — just extending pretraining context isn't enough
5. **SSM hybrids (Jamba, Mamba-2)** offer the best theoretical scaling but less mature

## See Also
- [[concepts/long-context|Long Context]]
- [[concepts/positional-encodings|Positional Encodings]]
- [[concepts/kv-cache|KV Cache]]
- [[concepts/flash-attention|FlashAttention]]
