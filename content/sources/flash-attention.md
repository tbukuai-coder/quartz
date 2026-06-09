---
type: source
arxiv_id: "2205.14135"
title: "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness"
authors: ["Tri Dao", "Daniel Y. Fu", "Stefano Ermon", "Atri Rudra", "Christopher Ré"]
date: 2022-05-27
org: "Stanford University"
tags: [efficiency, architecture, foundational]
upvotes: 15
---

# FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness

> An **IO-aware** attention algorithm that computes exact attention 2–4× faster and with 5–20× less memory by minimizing HBM reads/writes through tiling and recomputation.

## Key Contributions
- Identified the **memory bandwidth bottleneck** in standard attention (HBM reads/writes, not FLOPs)
- Introduced **tiling** — computing attention in blocks that fit in SRAM, avoiding materializing the full N×N attention matrix in HBM
- Used **recomputation** in the backward pass instead of storing the attention matrix
- Achieved **2–4× wall-clock speedup** and **5–20× memory reduction** with exact (not approximate) attention
- Enabled training with **longer sequences** (up to 16K+ tokens) that were previously impractical
- Solved the **Path-X** challenge (16K sequence length) for the first time

## Method
Standard attention materializes the full `N × N` attention matrix in GPU HBM (high bandwidth memory). FlashAttention avoids this by:

1. **Tiling**: Split Q, K, V into blocks; compute attention one block at a time in SRAM (fast on-chip memory)
2. **Online softmax**: Compute softmax incrementally across blocks without materializing the full matrix
3. **No attention matrix storage**: The N×N matrix is never written to HBM
4. **Backward pass recomputation**: Recompute attention blocks during backprop instead of storing them

The algorithm accounts for the GPU memory hierarchy (SRAM → HBM → DRAM) and minimizes data movement — hence "IO-aware."

## Results
- **2–4× speedup** in attention computation vs. PyTorch standard attention
- **5–20× memory savings** — enables much longer sequences
- First to solve **Path-X** (16K token classification) and **Path-256** challenges
- BERT-large training: 15% faster end-to-end
- GPT-2 training: 3× faster than HuggingFace and 1.8× faster than Megatron

## Connections
- **Builds on**: [[sources/attention-is-all-you-need]] (optimizes the core attention operation)
- **Extended by**: FlashAttention-2 (2× faster, better parallelism), FlashAttention-3
- **Used by**: Virtually all modern LLM training — [[sources/llama-2]], [[sources/mistral-7b]], [[sources/qwen25]], etc.
- **Key concepts**: [[concepts/flash-attention]], [[concepts/self-attention]], [[concepts/transformer-architecture]]

## Citation
> Dao et al., "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness," arXiv:2205.14135, 2022.
> https://huggingface.co/papers/2205.14135
