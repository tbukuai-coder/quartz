---
type: concept
tags: [inference, architecture, efficiency, serving]
---

# KV Cache

> The **key-value cache** stores previously computed attention states during autoregressive generation, avoiding recomputation at each step — the dominant memory bottleneck in LLM inference and the target of most serving optimizations.

## Overview
When an LLM generates text token by token, each new token must attend to all previous tokens. Without caching, this would require recomputing attention for every prior token at every step — O(n²) work for a sequence of length n. The KV cache stores the key (K) and value (V) projections from all previous positions, so each new token only needs to compute its own Q, K, V and attend to the cached K/V states.

The KV cache is the **single largest memory consumer** during LLM inference.

## Memory Calculation
```
KV cache size = 2 × L × H × D × S × P  (per request)
```
**Example**: Llama-2-70B at 4K context in FP16: ~1.3 GB per request. 100 concurrent requests → 130 GB.

## Why It's a Bottleneck

| Model | KV Cache per 4K Request | 100 Concurrent |
|---|---|---|
| Llama-2-7B | ~160 MB | ~16 GB |
| Llama-2-70B | ~1.3 GB | ~130 GB |
| Llama-3-405B | ~5+ GB | ~500+ GB |

## Optimization Techniques

### Architecture-Level
| Technique | Reduction | Used By |
|---|---|---|
| [[concepts/gqa|GQA]] | 4–8× | [[entities/models/llama|Llama 2+]], [[entities/models/mistral|Mistral]] |
| Multi-head Latent Attention (MLA) | ~93% | [[sources/deepseek-v3|DeepSeek-V3]] |
| [[concepts/swa|Sliding Window Attention]] | Bounded | [[entities/models/mistral|Mistral 7B]] |
| Hybrid SSM-Attention | ~90% | [[sources/jamba|Jamba]] |

### Serving-Level
| Technique | Key Innovation | System |
|---|---|---|
| [[sources/vllm|PagedAttention]] | OS-style paging | vLLM |
| [[sources/sglang|RadixAttention]] | Prefix caching with radix tree | SGLang |
| KV cache quantization | INT8/INT4 compression | Various |

## Key Papers
- [[sources/vllm]] — PagedAttention for KV cache management
- [[sources/sglang]] — RadixAttention for prefix caching
- [[sources/deepseek-v3]] — MLA for KV cache compression
- [[sources/flash-attention]] — Efficient attention computation

## See Also
- [[concepts/llm-serving]] — Serving systems built around KV cache optimization
- [[concepts/gqa]] — GQA reduces KV cache via head sharing
- [[concepts/long-context]] — Long context amplifies KV cache pressure
- [[concepts/speculative-decoding]] — Amortizes KV cache cost