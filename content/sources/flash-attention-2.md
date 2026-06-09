---
type: source
arxiv_id: "2307.08691"
title: "FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning"
authors: ["Tri Dao"]
date: 2023-07-17
org: "Together AI / Stanford"
tags: [efficiency, attention, infrastructure, 2023]
upvotes: 9
---

# FlashAttention-2

> A **2× speedup** over the original [[sources/flash-attention|FlashAttention]] through better GPU work partitioning — reaching **50–73% of theoretical maximum FLOPs/s** on A100 GPUs (vs. 25–40% for FA1). Enables **225 TFLOPs/s** per A100 for GPT-style training (72% model FLOPs utilization).

## Key Contributions
- **2× faster than FlashAttention**: Better parallelism and work partitioning across thread blocks and warps
- **Reduced non-matmul FLOPs**: Tweaked algorithm to minimize operations that don't use Tensor Cores
- **Better parallelism**: Parallelizes across sequence length (not just batch × heads), improving occupancy for long sequences
- **Optimized warp partitioning**: Reduces shared memory communication within thread blocks
- **50–73% of theoretical max**: Approaches the efficiency of optimized GEMM operations

## Method
Three key optimizations over FlashAttention:

1. **Reduce non-matmul FLOPs**: Rearranged computation to maximize Tensor Core utilization. On A100, matmul throughput is 312 TFLOPs/s vs. 19.5 TFLOPs/s for non-matmul — a 16× difference
2. **Parallelize across sequence length**: Instead of only parallelizing across batch × heads, also split the sequence dimension across thread blocks. Critical for long sequences with few heads (e.g., multi-query attention)
3. **Better warp partitioning**: Within each thread block, split work between warps to minimize shared memory reads/writes. Forward pass: split across K/V blocks; backward pass: split across Q blocks

## Results
| Method | A100 FLOPs/s | Speedup vs. FA1 |
|---|---|---|
| PyTorch baseline | ~40 TFLOPs/s | — |
| FlashAttention | ~120 TFLOPs/s | 1× |
| **FlashAttention-2** | **~230 TFLOPs/s** | **~2×** |
| Theoretical max | 312 TFLOPs/s | — |

End-to-end GPT training: **225 TFLOPs/s per A100** (72% MFU) for 2.7B model with 4K sequence length.

## Impact
- Standard in virtually all LLM training pipelines (PyTorch, Transformers, vLLM, etc.)
- Enabled practical training with 16K+ sequences at reasonable cost
- Integrated into Hugging Face Transformers as `attn_implementation="flash_attention_2"`
- Foundation for FlashAttention-3 (Hopper GPUs, FP8)

## Connections
- Builds on: [[sources/flash-attention|FlashAttention]]
- Extended by: FlashAttention-3 (Hopper, FP8), FlashAttention-4 (Blackwell)
- Creator: Tri Dao ([[entities/orgs/together-ai|Together AI]] co-founder)
- Concepts: [[concepts/flash-attention]], [[concepts/training-infrastructure]]

## Citation
> Dao, "FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning," ICLR 2024, arXiv:2307.08691.
