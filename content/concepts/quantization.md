---
type: concept
tags: [efficiency, quantization]
---

# Quantization

> Reducing the numerical precision of model weights (e.g., FP16 → INT4) to **decrease memory usage and accelerate inference**, with minimal quality loss.

## Overview
LLMs store weights in floating-point format. Quantization converts these to lower-precision formats, reducing memory footprint and often increasing inference speed. The key innovation of [[sources/qlora|QLoRA]] was showing that 4-bit quantized models can serve as effective bases for fine-tuning.

## Precision Formats
| Format | Bits | Bytes/Param | Use Case |
|---|---|---|---|
| FP32 | 32 | 4 | Training (legacy) |
| BF16/FP16 | 16 | 2 | Standard training |
| INT8 | 8 | 1 | Inference; LLM.int8() |
| **NF4** | 4 | 0.5 | QLoRA fine-tuning |
| INT4 / GPTQ | 4 | 0.5 | Inference quantization |
| GGUF / GGML | 2-8 | varies | CPU inference (llama.cpp) |

## Key Methods
- **NormalFloat (NF4)**: Information-theoretically optimal 4-bit type for normally distributed weights — [[sources/qlora]]
- **Double Quantization**: Quantizing the quantization constants — saves ~0.37 bits/param
- **GPTQ**: Post-training quantization using approximate second-order information — [[sources/gptq]]
- **AWQ**: Activation-aware weight quantization — [[sources/awq]]
- **bitsandbytes**: Library implementing INT8/NF4 quantization on GPU

For a detailed comparison of post-training methods (GPTQ, AWQ, GGUF), see [[concepts/post-training-quantization|Post-Training Quantization]].

## Memory Impact (7B Model)
| Precision | Memory |
|---|---|
| FP32 | ~28 GB |
| BF16 | ~14 GB |
| INT8 | ~7 GB |
| NF4 | ~3.5 GB |

## Key Papers
- [[sources/qlora]] — NF4, double quantization, QLoRA training
- [[sources/gptq]] — GPTQ: Second-order post-training quantization
- [[sources/awq]] — AWQ: Activation-aware weight quantization

## See Also
- [[concepts/post-training-quantization]] — Detailed PTQ methods (GPTQ, AWQ, GGUF)
- [[concepts/lora-peft]]
- [[concepts/flash-attention]]