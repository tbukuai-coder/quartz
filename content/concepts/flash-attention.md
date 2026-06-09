---
type: concept
tags: [efficiency, attention]
---

# FlashAttention

> An **IO-aware** attention algorithm that computes exact attention 2–4× faster by minimizing GPU memory reads/writes through tiling and recomputation — now the default in virtually all LLM training.

## Overview
Standard attention materializes the full N×N attention matrix in GPU HBM, which is the bottleneck. FlashAttention ([[sources/flash-attention|Dao et al. 2022]]) restructures the computation to work in blocks that fit in fast SRAM, never materializing the full matrix.

## How It Works
1. **Tiling**: Split Q, K, V into blocks that fit in SRAM
2. **Online softmax**: Compute softmax incrementally across blocks
3. **No materialization**: The N×N attention matrix never exists in HBM
4. **Backward recomputation**: Recompute attention blocks during backprop instead of storing

## Versions
| Version | Year | Key Improvement |
|---|---|---|
| FlashAttention 1 | 2022 | Original IO-aware algorithm |
| FlashAttention 2 | 2023 | 2× faster; better parallelism |
| FlashAttention 3 | 2024 | Hopper GPU optimizations |

## Impact
- Enables **longer sequences** without memory explosion
- Standard in all major frameworks (PyTorch, HuggingFace, vLLM)
- Critical enabler for 32K–128K+ context models
- 15–50% end-to-end training speedup

## Key Papers
- [[sources/flash-attention]] — FlashAttention paper

## See Also
- [[concepts/self-attention]]
- [[concepts/transformer-architecture]]
