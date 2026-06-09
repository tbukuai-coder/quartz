---
type: concept
tags: [architecture, foundational, positional-encoding, rope]
---

# Positional Encodings (RoPE, ALiBi)

> Methods for injecting **sequence position information** into Transformer models — enabling the model to distinguish token order, since self-attention is inherently permutation-invariant.

## Overview
Transformers process all tokens in parallel with no inherent notion of order. Without positional information, "The cat sat on the mat" and "mat the on sat cat The" would produce identical representations. Positional encodings solve this by adding position-dependent signals to token representations.

## Evolution

| Method | Year | Type | Max Context | Used By |
|---|---|---|---|---|
| **Sinusoidal** | 2017 | Absolute | Fixed | Original Transformer |
| **Learned** | 2018 | Absolute | Fixed | GPT-2, [[entities/models/bert-model\|BERT]] |
| **RoPE** | 2021 | Relative (rotary) | Extensible | [[entities/models/llama\|LLaMA]], [[entities/models/qwen\|Qwen]], [[entities/models/mistral\|Mistral]] |
| **ALiBi** | 2021 | Relative (bias) | Extensible | BLOOM, MPT |
| **NoPE** | 2024 | None | Via SSM | [[sources/jamba\|Jamba]] (SSM layers) |

## RoPE
Dominant positional encoding. Rotates query/key vectors in 2D subspaces — inner product depends only on relative position. Compatible with [[concepts/kv-cache|KV caching]].

### RoPE Extension
| Method | Training Cost | Used By |
|---|---|---|
| **[[sources/yarn\|YaRN]]** | **10× fewer tokens** | [[entities/models/qwen\|Qwen]], [[sources/deepseek-v3\|DeepSeek]] |
| Dynamic NTK | **Zero cost** | Most inference engines |
| LongRoPE | Two-stage fine-tuning | Microsoft |

## ALiBi
Adds position-dependent bias to attention: `q·k - m·|i-j|`. Simpler than RoPE but less adopted.

### Why RoPE Won
1. Works with FlashAttention, GQA, KV caching
2. YaRN enables 10× context extension
3. Optimized in all inference engines
4. LLaMA's choice made it the default

## Key Papers
- [[sources/attention-is-all-you-need]] — Original sinusoidal encoding
- [[sources/yarn]] — YaRN: Efficient RoPE context extension
- [[sources/jamba]] — Positional encodings optional in hybrids

## See Also
- [[concepts/transformer-architecture]] — Core Transformer component
- [[concepts/long-context]] — Context extension via positional encoding
- [[concepts/kv-cache]] — RoPE compatible with KV caching