---
type: entity
category: org
tags: [nvidia, infrastructure, reasoning, hybrid-architecture, fp4]
---

# NVIDIA

> The dominant **GPU hardware provider** for AI training and inference, and increasingly an **AI research lab** — creators of [[sources/llama-nemotron|Llama-Nemotron]] (efficient reasoning models), [[sources/nemotron-h|Nemotron-H]] (hybrid Mamba-Transformer), [[sources/nemotron-3-super|Nemotron 3 Super]] (first NVFP4-pretrained MoE), NeMo framework, and TensorRT-LLM.

## Overview
NVIDIA occupies a unique position in the AI ecosystem: not only providing the hardware (A100, H100, H200, B200 GPUs) that powers virtually all LLM training, but also conducting research that pushes the boundaries of model efficiency and deployment. Their Nemotron model family demonstrates that NAS, hybrid architectures, FP4 pre-training, and large-scale RL can produce open models competitive with DeepSeek-R1 while being significantly more efficient at inference.

## Key Contributions

### Models
- **[[sources/nemotron-3-super|Nemotron 3 Super]]** (2025): 120B (12B active) hybrid Mamba-Attention MoE — **first model pre-trained in NVFP4**, introduces LatentMoE + MTP layers for speculative decoding. 2.2× throughput over GPT-OSS-120B.
- **[[sources/llama-nemotron|Llama-Nemotron]]** (2025): Nano (8B), Super (49B), Ultra (253B) — efficient reasoning via NAS on Llama 3, GRPO RL, dynamic thinking toggle. First open models with reasoning toggle.
- **[[sources/nemotron-h|Nemotron-H]]** (2025): Hybrid Mamba-Transformer (8B, 56B/47B) — up to 3× faster than pure Transformers at equivalent quality
- **Nemotron-4**: Earlier NVIDIA language models for research

### Infrastructure & Frameworks
- **NeMo**: End-to-end framework for LLM training, fine-tuning, and alignment
- **NeMo-Aligner**: RLHF/GRPO training framework (used for Llama-Nemotron and Nemotron 3 Super RL)
- **TensorRT-LLM**: Optimized inference engine for NVIDIA GPUs
- **Megatron-LM**: Distributed training framework for large models

### Hardware
- **A100** (80GB): Standard for LLM training (used by Falcon, OLMo, etc.)
- **H100** (80GB): Current generation, Transformer Engine for FP8
- **H200** (141GB HBM3e): Extended memory variant
- **B200/GB200** (Blackwell): Next generation — native NVFP4 support, validated by Nemotron 3 Super and [[sources/quartet|Quartet]]

### Research
- **Puzzle/MiniPuzzle**: Neural Architecture Search for hardware-optimized LLM compression
- **NVFP4 pre-training**: First validated FP4 pre-training at 120B/25T-token scale (Nemotron 3 Super)
- **FP8 training**: Validated FP8 pretraining at 56B scale (Nemotron-H)
- **LatentMoE**: New MoE variant that projects to latent space before routing, optimizing accuracy per FLOP
- **Hybrid architectures**: Mamba-Transformer hybrids that maintain quality while improving efficiency

## Papers in This Wiki
- [[sources/nemotron-3-super]] — Nemotron 3 Super (hybrid Mamba-MoE, NVFP4)
- [[sources/llama-nemotron]] — Llama-Nemotron reasoning models
- [[sources/nemotron-h]] — Nemotron-H hybrid Mamba-Transformer

## See Also
- [[concepts/training-infrastructure]] — GPU hardware for LLM training
- [[concepts/llm-serving]] — Inference optimization
- [[concepts/state-space-models]] — SSMs (Mamba in Nemotron-H, Nemotron 3 Super)
- [[concepts/quantization]] — FP4/FP8 quantization
- [[entities/orgs/together-ai]] — Together AI (FlashAttention, inference)
