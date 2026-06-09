---
type: concept
tags: [efficiency, quantization, inference, deployment]
---

# Post-Training Quantization (PTQ)

> Compressing a pre-trained model's weights to lower precision (e.g., FP16 → INT4) **after training is complete**, without any fine-tuning — enabling deployment of large models on consumer hardware with minimal accuracy loss.

## Overview
Post-training quantization (PTQ) converts model weights from high-precision floating point to low-precision integer formats after training. Unlike [[concepts/quantization|quantization-aware training]] (QAT) or [[sources/qlora|QLoRA]] (which quantize during training), PTQ requires no gradient computation — just a small calibration dataset and minutes to hours of processing. This makes it the most practical path from trained model to deployed model.

PTQ is the dominant quantization approach in the open-source ecosystem: thousands of GPTQ, AWQ, and GGUF models on the Hugging Face Hub allow running 70B+ models on consumer GPUs.

## How It Works

### The Core Problem
Naively rounding weights to lower precision destroys accuracy because:
1. Not all weights are equally important — some channels carry critical information
2. Weight distributions are non-uniform — outliers cause disproportionate quantization error
3. Layer interactions compound errors

### Key Methods

| Method | Core Idea | Calibration | Speed | Quality |
|---|---|---|---|---|
| [[sources/gptq\|GPTQ]] | Second-order weight correction (inverse Hessian) | 128 samples, ~4 GPU-hours for 175B | Moderate | Strong |
| [[sources/awq\|AWQ]] | Protect 1% salient channels (activation-aware scaling) | 128 samples, no gradients | Fast | Best generalization |
| GGUF (llama.cpp) | Per-block quantization with multiple bit widths | None (round-to-nearest) | Instant | Varies |
| SmoothQuant | Smooth activation outliers into weights (W8A8) | Calibration set | Fast | Good for W8A8 |
| bitsandbytes (LLM.int8()) | Mixed-precision decomposition for outlier features | None (dynamic) | Instant | Good at 8-bit |

### GPTQ — Second-Order Quantization
[[sources/gptq|GPTQ]] uses approximate second-order information (inverse Hessian) to optimally quantize each weight, compensating for quantization error across columns:
- Processes each layer independently (layer-wise)
- Lazy batch updates for GPU efficiency
- Cholesky decomposition for numerical stability
- Result: <0.5 perplexity increase at 4-bit for most models

### AWQ — Activation-Aware Quantization
[[sources/awq|AWQ]] observes that ~1% of weight channels are critical (identified by activation magnitude), and protects them via per-channel scaling:
- No backpropagation or weight reconstruction needed
- Better generalization across domains (instruction-tuned, code, multimodal)
- Hardware-friendly: no mixed precision needed
- TinyChat framework for mobile/edge deployment

## Comparison: GPTQ vs. AWQ

| Aspect | GPTQ | AWQ |
|---|---|---|
| Year | 2022 | 2023 |
| Approach | Weight correction via Hessian | Salient channel protection |
| Calibration data | 128 samples (C4) | 128 samples (Pile) |
| Generalization | Good on similar domains | Better cross-domain |
| Speed (quantize 7B) | ~10 minutes | ~5 minutes |
| 4-bit PPL (Llama-2-7B) | 5.62 | 5.60 |
| 3-bit PPL (Llama-2-7B) | 6.43 | 6.24 |
| Ecosystem | AutoGPTQ, thousands of Hub models | AutoAWQ, thousands of Hub models |

## Bit Width Guide
| Bits | Memory Savings | Quality Impact | Use Case |
|---|---|---|---|
| 8-bit (INT8) | 2× | Negligible | Production serving |
| 4-bit (INT4) | 4× | Small (~0.2 PPL) | Consumer GPU deployment |
| 3-bit | 5.3× | Moderate (~1 PPL) | Extreme compression |
| 2-bit | 8× | Significant | Research / edge cases |

## Practical Impact
A 70B model at different precisions:
| Precision | VRAM Required | Accessible Hardware |
|---|---|---|
| FP16 | ~140 GB | 2× A100-80GB |
| INT8 | ~70 GB | 1× A100-80GB |
| **INT4 (GPTQ/AWQ)** | ~35 GB | **1× A6000 or 2× RTX 4090** |
| GGUF Q4_K_M | ~35 GB | **CPU with 64GB RAM** |

## Ecosystem
- **AutoGPTQ**: Widely-used Python library for GPTQ quantization
- **AutoAWQ**: AWQ implementation with 7K+ GitHub stars
- **llama.cpp / GGUF**: CPU-focused quantization, 2–8 bit, massive community
- **bitsandbytes**: Dynamic INT8/NF4 quantization on GPU
- **[[sources/vllm|vLLM]]** and TGI: Native support for GPTQ and AWQ models
- Thousands of pre-quantized models on Hugging Face Hub (TheBloke, etc.)

## Key Papers
- [[sources/gptq]] — GPTQ: Second-order post-training quantization (2022)
- [[sources/awq]] — AWQ: Activation-aware weight quantization (2023)
- [[sources/qlora]] — QLoRA: Quantization for training (related but different)

## See Also
- [[concepts/quantization]] — Broader overview of quantization methods
- [[concepts/lora-peft]] — QLoRA combines PTQ with LoRA training
- [[concepts/llm-serving]] — PTQ models deployed via vLLM, TGI, llama.cpp