---
type: concept
tags: [training, efficiency, infrastructure, precision]
---

# Mixed Precision Training

> Training models using a combination of **lower-precision (FP16/BF16) and higher-precision (FP32) arithmetic** — halving memory usage and doubling throughput while maintaining stability.

## Overview
Mixed precision performs most computations in 16-bit while keeping master weights in FP32. This is the default for all modern LLM training.

## Precision Formats

| Format | Bits | Range | Used For |
|---|---|---|---|
| **FP32** | 32 | ±3.4×10³⁸ | Master weights, accumulation |
| **FP16** | 16 | ±65,504 | Forward/backward (needs loss scaling) |
| **BF16** | 16 | ±3.4×10³⁸ | Forward/backward (**preferred**) |
| **FP8** | 8 | Limited | [[sources/deepseek-v3\|DeepSeek-V3]] training |

### BF16 vs FP16
BF16 has FP32's dynamic range → no loss scaling needed → simpler and more stable. **BF16 is the default** for modern LLM training on A100/H100.

## How It Works
1. Master weights in FP32
2. Cast to BF16 for forward/backward pass
3. Gradients computed in BF16
4. Convert to FP32, apply optimizer step to FP32 master weights

## FP8 Training (Frontier)
[[sources/deepseek-v3|DeepSeek-V3]] pioneered FP8 at 671B parameters — GEMM in 8-bit with per-block scaling factors.

## Practical Guide

| Scenario | Precision |
|---|---|
| Standard LLM training | BF16 mixed precision |
| Older GPU (V100) | FP16 with loss scaling |
| Frontier (100B+) | BF16 or FP8 |
| QLoRA fine-tuning | BF16 + NF4 base |
| Inference | See [[concepts/post-training-quantization\|PTQ]] |

## Key Papers
- Micikevicius et al., "Mixed Precision Training" (2017)
- [[sources/deepseek-v3]] — FP8 training at 671B
- [[sources/flash-attention]] — Optimized for mixed precision

## See Also
- [[concepts/training-infrastructure]] — Part of the training stack
- [[concepts/quantization]] — Post-training precision reduction
- [[concepts/post-training-quantization]] — PTQ for inference