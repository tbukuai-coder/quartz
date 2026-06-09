---
type: source
arxiv_id: "2309.06180"
title: "Efficient Memory Management for Large Language Model Serving with PagedAttention"
authors: ["Woosuk Kwon", "Zhuohan Li", "Siyuan Zhuang", "Ying Sheng", "Lianmin Zheng", "Cody Hao Yu", "Joseph E. Gonzalez", "Hao Zhang", "Ion Stoica"]
date: 2023-09-12
org: "UC Berkeley"
tags: [inference, serving, efficiency, kv-cache]
upvotes: 54
---

# vLLM / PagedAttention

> PagedAttention applies OS-style virtual memory paging to KV caches, enabling vLLM to serve LLMs with 2–4× higher throughput than prior systems.

## Key Contributions
- **PagedAttention**: An attention algorithm that stores KV cache in non-contiguous paged memory blocks, inspired by virtual memory in operating systems
- **vLLM**: A high-throughput LLM serving system built on PagedAttention with near-zero KV cache waste
- **KV cache sharing**: Flexible sharing of KV cache within and across requests (parallel sampling, beam search, shared prefixes)
- **Preemption mechanisms**: Recomputation and swapping strategies for handling overload

## Method
The key insight is that KV cache memory for each request is huge, grows dynamically, and is wasted by fragmentation in existing systems (60–80% waste). PagedAttention partitions KV cache into fixed-size blocks that can be stored non-contiguously in GPU memory, using a block table (analogous to a page table) to map logical KV cache positions to physical memory. This eliminates both internal and external fragmentation. The centralized scheduler coordinates KV cache allocation across requests using copy-on-write for shared sequences.

## Results
- **2–4× throughput improvement** over FasterTransformer and Orca on OPT-13B/66B/175B and LLaMA-13B
- Improvements more pronounced with longer sequences, larger models, and complex decoding (beam search, parallel sampling)
- Near-zero memory waste (< 4%) vs. 60–80% in prior systems
- With parallel sampling: up to 55% memory saving from shared KV cache
- Block size of 16 tokens found optimal for balancing parallelism and fragmentation

## Datasets Used
- ShareGPT conversation traces (real-world workload)
- Alpaca (instruction-following workload)
- WMT16 English-to-German (shared prefix evaluation)

## Models Released
- **vLLM**: Open-source LLM serving engine (77,900+ GitHub stars) — now the dominant open-source inference server

## Connections
- Builds on: [[sources/attention-is-all-you-need|Transformer]], [[concepts/self-attention|Self-Attention]]
- Related systems: [[sources/sglang|SGLang]] (builds on vLLM concepts, adds RadixAttention)
- Complements: [[sources/medusa|Medusa]] (speculative decoding), [[concepts/flash-attention|FlashAttention]] (training efficiency)
- Related concepts: [[concepts/llm-serving|LLM Serving & Inference]]

## Citation
> Kwon et al., "Efficient Memory Management for Large Language Model Serving with PagedAttention," SOSP 2023, arXiv:2309.06180.
