---
type: concept
tags: [inference, efficiency, speculative-decoding]
---

# Speculative Decoding

> Accelerating LLM inference by **predicting multiple future tokens in parallel** and verifying them in a single forward pass — achieving 2–3× speedup without changing the model's output distribution.

## Overview
Standard LLM inference is **autoregressive**: one token per forward pass, with each pass moving the full model parameters from memory to compute. This is memory-bandwidth bound, meaning the GPU spends most of its time waiting for data transfer rather than computing. Speculative decoding breaks this bottleneck by generating multiple candidate tokens cheaply and verifying them all at once.

## How It Works

### Standard Speculative Decoding
1. **Draft**: A small, fast "draft model" generates k candidate tokens quickly
2. **Verify**: The full target model processes all k candidates in a single forward pass
3. **Accept/Reject**: Using rejection sampling, accept the longest prefix that matches the target model's distribution
4. **Result**: Multiple tokens per forward pass of the large model → speedup

### Medusa ([[sources/medusa|Medusa]])
Instead of a separate draft model, **add extra prediction heads** to the target model:
1. **Medusa heads**: k lightweight MLPs added alongside the LM head, each predicting token+i
2. **Tree attention**: Construct a tree of candidate continuations from head predictions
3. **Parallel verification**: Process the entire candidate tree in one forward pass
4. **No draft model needed**: Simpler to deploy and maintain

**Advantages over standard speculative decoding:**
- No separate model to acquire, maintain, and synchronize
- Minimal parameter overhead (<1%)
- Works with any model via self-distillation

## Key Methods

| Method | Approach | Speedup | Extra Model? |
|---|---|---|---|
| Standard Speculative | Separate draft model | 2–3× | ✅ Yes |
| **Medusa-1** | Extra heads (frozen backbone) | 2.2× | ❌ No |
| **Medusa-2** | Extra heads (joint training) | 2.3–2.8× | ❌ No |
| EAGLE | Feature-level prediction | 2–3× | ❌ No |
| Lookahead | Jacobi iteration | 1.5–2× | ❌ No |

## Why It Works
- Autoregressive inference is **memory-bandwidth bound** (not compute bound)
- Processing 1 token vs 10 tokens takes nearly the same wall time (the bottleneck is loading model weights)
- Verification of k candidates in parallel costs only ~1.1× a single forward pass
- The more memory-bandwidth bound (larger models, lower batch sizes), the more benefit

## Trade-offs
- **Lossless** (with rejection sampling): Output distribution identical to target model
- **Lossy** (typical acceptance): Slightly different distribution but higher speedup
- Speedup depends on: draft model quality, model size, hardware, batch size
- Diminishing returns at large batch sizes (compute-bound regime)

## Key Papers
- [[sources/medusa]] — Medusa: Multiple decoding heads, tree attention (2.2–3.6×)
- [[sources/flash-attention]] — Efficient attention for tree verification

## See Also
- [[concepts/flash-attention]]
- [[concepts/quantization]] — Another inference efficiency approach
