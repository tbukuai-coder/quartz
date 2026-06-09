---
type: source
arxiv_id: "2312.07104"
title: "SGLang: Efficient Execution of Structured Language Model Programs"
authors: ["Lianmin Zheng", "Liangsheng Yin", "Zhiqiang Xie", "Jeff Huang", "Chuyue Sun", "Cody Hao Yu", "Shiyi Cao", "Christos Kozyrakis", "Ion Stoica", "Joseph E. Gonzalez", "Hao Zhang"]
date: 2023-12-12
org: "UC Berkeley / Stanford"
tags: [inference, serving, structured-generation, kv-cache, agents, 2023]
upvotes: 8
---

# SGLang

> A system for efficient execution of complex LLM programs, introducing RadixAttention for automatic KV cache reuse and compressed finite state machines for structured output decoding — up to 6.4× throughput improvement.

## Key Contributions
- **RadixAttention**: Automatic KV cache reuse using a radix tree (LRU cache) — shared prefixes across requests are cached and reused without manual management
- **Compressed Finite State Machine (FSM)**: Accelerates constrained/structured output decoding (JSON, regex) by jumping multiple tokens at once
- **SGLang DSL**: A Python-embedded domain-specific language for programming multi-call LLM workflows with primitives for generation, parallelism, and control flow
- **API speculative execution**: Optimizes latency for API-only models by speculatively executing calls in parallel

## Method
1. **RadixAttention**: Maintains a global radix tree of all KV cache entries. When a new request arrives, it finds the longest matching prefix in O(n) time and reuses the cached KV values. Cache-aware scheduling reorders requests to maximize prefix hits. Provably optimal under LRU eviction for tree-structured workloads
2. **Compressed FSM**: Instead of checking constraints token-by-token, compresses deterministic FSM transitions — if the next 5 tokens are forced by the regex/JSON schema, they're generated in one step, skipping sampling overhead
3. **Frontend DSL**: Primitives include `gen()` (generation), `select()` (constrained choice), `fork()` (parallel branches), and `image()` (multimodal input). Interpreter mode for debugging, compiler mode for optimization
4. **Distributed RadixAttention**: Each worker maintains sub-trees; a router's meta-tree tracks all sub-trees for optimal dispatch

## Results
- **Up to 6.4× throughput** and **3.7× latency reduction** vs. vLLM and Guidance on Llama/Mixtral/LLaVA
- Improvements on: agent control, logical reasoning, few-shot learning, JSON decoding, RAG pipelines, multi-turn chat
- Cache hit rates of 50–90% on structured workloads (tree-of-thought, multi-turn)
- Compressed FSM decoding: up to 2× speedup on JSON/regex-constrained generation
- Now the second most popular LLM serving engine after vLLM

## Datasets Used
- ShareGPT (multi-turn chat evaluation)
- Tree-of-thought reasoning traces
- JSON decoding benchmarks

## Models Released
- **SGLang runtime** — open-source serving engine (GitHub: sgl-project/sglang)

## Connections
- Complements: [[sources/vllm|vLLM]] (PagedAttention — SGLang builds on similar ideas but adds prefix caching and structured output)
- Related: [[sources/medusa|Medusa]] (speculative decoding), [[concepts/flash-attention|FlashAttention]]
- Enables: [[concepts/agents|LLM Agents]] (multi-call workflows), [[concepts/rag|RAG]] pipelines
- Concepts: [[concepts/llm-serving|LLM Serving & Inference]], [[concepts/speculative-decoding|Speculative Decoding]]

## Citation
> Zheng et al., "SGLang: Efficient Execution of Structured Language Model Programs," arXiv:2312.07104, 2023.
