---
type: concept
tags: [training, infrastructure, distributed, deepspeed, fsdp]
---

# Training Infrastructure

> The systems and frameworks that enable training LLMs at scale — from distributed training ([[sources/zero-deepspeed|ZeRO/DeepSpeed]]) to efficient attention ([[sources/flash-attention|FlashAttention]]) to unified fine-tuning frameworks ([[sources/llamafactory|LlamaFactory]]).

## Overview
Training modern LLMs requires distributing computation across multiple GPUs and optimizing memory usage at every level. The HF ecosystem relies on a stack of training infrastructure: DeepSpeed ZeRO for memory-efficient distributed training, FlashAttention for compute-efficient attention, and HF's Accelerate/TRL libraries to tie it all together.

## Memory Hierarchy

### The Problem
A 7B model in fp32 requires ~28GB just for parameters. Adam optimizer adds 2× that (momentum + variance). Gradients add another 1×. Total: ~112GB — far exceeding any single GPU.

### Solutions by Layer
| Layer | Tool | Memory Reduction |
|---|---|---|
| **Optimizer states** | [[sources/zero-deepspeed\|ZeRO Stage 1]] | 4× |
| **+ Gradients** | ZeRO Stage 2 | 8× |
| **+ Parameters** | ZeRO Stage 3 | Linear with # GPUs |
| **Precision** | Mixed precision (bf16/fp16) | 2× |
| **Parameters** | [[concepts/lora-peft\|LoRA/QLoRA]] | 10,000× fewer trainable |
| **Attention** | [[sources/flash-attention\|FlashAttention]] | 5-20× memory for attention |
| **Offloading** | ZeRO-Offload | Move to CPU/NVMe |

## Key Frameworks in the HF Ecosystem
| Framework | Role | Integration |
|---|---|---|
| **[[sources/zero-deepspeed\|DeepSpeed]]** | Distributed training with ZeRO | `transformers.Trainer(deepspeed=config)` |
| **Accelerate** | Hardware-agnostic distributed training | HF native, wraps FSDP/DeepSpeed |
| **FSDP** | PyTorch native parameter sharding | Via Accelerate or direct PyTorch |
| **TRL** | SFT/DPO/GRPO trainers | Built on Transformers Trainer |
| **[[sources/llamafactory\|LlamaFactory]]** | Unified fine-tuning UI | Web interface for all methods |

## Practical Stack for Training
```
Small models (< 7B, single GPU):
  QLoRA + FlashAttention + bf16

Medium models (7-13B, multi-GPU):
  LoRA/Full FT + DeepSpeed ZeRO Stage 2 + FlashAttention

Large models (30B+, multi-node):
  Full FT + DeepSpeed ZeRO Stage 3 + FlashAttention + gradient checkpointing
```

## Key Papers
- [[sources/zero-deepspeed|ZeRO / DeepSpeed]] (2019) — memory-efficient distributed training
- [[sources/flash-attention|FlashAttention]] (2022) — IO-aware efficient attention
- [[sources/llamafactory|LlamaFactory]] (2024) — unified fine-tuning framework

## See Also
- [[concepts/lora-peft|LoRA / PEFT]]
- [[concepts/quantization|Quantization]]
- [[concepts/flash-attention|FlashAttention]]
