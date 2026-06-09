---
type: concept
tags: [inference, serving, efficiency, deployment]
---

# LLM Serving & Inference

> The systems, algorithms, and optimizations that make it practical to deploy LLMs in production — from KV cache management to structured output decoding.

## Overview
Serving LLMs at scale is fundamentally different from training. The autoregressive generation process creates unique challenges: dynamic memory allocation (output length unknown in advance), sequential token generation (limits parallelism), and massive KV cache requirements (grows linearly with sequence length × batch size). The field has evolved from naive single-request serving to sophisticated systems handling thousands of concurrent requests.

## Key Challenges
1. **KV cache memory**: Each token's key-value states must be stored for all layers. For a 70B model, this can be 2+ GB per request
2. **Dynamic memory allocation**: Output lengths vary dramatically — pre-allocating wastes memory; fragmentation limits batch size
3. **Throughput vs. latency**: Batching improves throughput but can increase per-request latency
4. **Structured outputs**: Constraining generation to valid JSON/regex adds overhead — see [[concepts/structured-generation|Structured Generation]]
5. **Prefix sharing**: Many requests share common prefixes (system prompts, few-shot examples)

## How It Works

### Memory Management
- **[[sources/vllm|PagedAttention (vLLM)]]**: OS-style virtual memory paging for KV caches — non-contiguous storage eliminates fragmentation, achieving near-zero waste
- **Continuous batching**: Process requests at the iteration level, not batch level — new requests join mid-generation

### KV Cache Optimization
- **[[sources/sglang|RadixAttention (SGLang)]]**: Automatic prefix caching using a radix tree — shared prefixes reused across requests
- **KV cache compression**: Quantization, eviction policies, and sparse attention patterns reduce memory

### Decoding Acceleration
- **[[concepts/speculative-decoding|Speculative decoding]]**: Use a smaller draft model to propose tokens, verify in parallel with the large model ([[sources/medusa|Medusa]] adds multiple decoding heads instead)
- **[[concepts/structured-generation|Structured output decoding]]**: [[sources/sglang|SGLang's compressed FSM]] skips multiple constrained tokens at once; [[sources/outlines|Outlines]] provides FSM-based vocabulary indexing

### Model Compression for Serving
- **[[concepts/post-training-quantization|Post-training quantization]]**: GPTQ/AWQ compress models to INT4, reducing VRAM 4× and enabling consumer GPU deployment

### Serving Frameworks
| System | Key Innovation | Throughput Gain |
|---|---|---|
| [[sources/vllm\|vLLM]] | PagedAttention | 2–4× |
| [[sources/sglang\|SGLang]] | RadixAttention + Compressed FSM | Up to 6.4× |
| TGI (HuggingFace) | Flash decoding, watermark | Production-ready |
| TensorRT-LLM (NVIDIA) | Custom CUDA kernels | Hardware-optimized |

## Key Papers
- [[sources/vllm|vLLM / PagedAttention]] (2023) — introduced paged KV cache management
- [[sources/sglang|SGLang]] (2023) — RadixAttention + structured output optimization
- [[sources/medusa|Medusa]] (2024) — speculative decoding with multiple heads
- [[sources/flash-attention|FlashAttention]] (2022) — efficient attention computation (training + inference)

## See Also
- [[concepts/structured-generation|Structured Generation]] — Guaranteed valid outputs (JSON, regex, grammar)
- [[concepts/speculative-decoding|Speculative Decoding]]
- [[concepts/post-training-quantization|Post-Training Quantization]] — GPTQ/AWQ for deployment
- [[concepts/quantization|Quantization]]
- [[concepts/flash-attention|FlashAttention]]