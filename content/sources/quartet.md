---
type: source
arxiv_id: "2505.14669"
title: "Quartet: Native FP4 Training Can Be Optimal for Large Language Models"
authors: ["Roberto L. Castro", "Andrei Panferov", "Soroush Tabesh", "Oliver Sieberling", "Jiale Chen", "Mahdi Nikdan", "Saleh Ashkboos", "Dan Alistarh"]
date: 2025-05-14
org: "IST Austria / Neural Magic"
tags: [quantization, fp4, training, efficiency, scaling-laws, 2025]
upvotes: 78
---

# Quartet

> Demonstrates that native FP4 training is a competitive alternative to FP16 and FP8 for LLMs, introducing low-precision scaling laws and optimized CUDA kernels for NVIDIA Blackwell.

## Key Contributions
- Introduces **low-precision scaling laws** that quantify performance trade-offs across bit-widths (FP4, FP8, FP16) and training setups, enabling principled precision selection
- Shows that **fully FP4 training** (all major linear layer computations in MXFP4) matches FP16/FP8 quality when properly designed
- Identifies four key "ingredients" for optimal quantized training: scaling-law comparison, mixed-precision trade-offs, minimal forward-pass error, and fast GPU support
- Provides **optimized CUDA kernels for NVIDIA Blackwell** (RTX 5090) demonstrating practical FP4 speedups
- Reveals a surprising finding: the optimal precision depends on the compute budget — FP4 is most beneficial for **larger models at moderate compute**

## Method
Quartet is built on four principles:

1. **Scaling-law comparison**: Fits standard scaling laws (loss as a function of model size and data) independently for each precision configuration. This reveals that different precisions trace different Pareto frontiers — and FP4 can be optimal in specific regimes.

2. **Mixed-precision trade-offs**: Independently varies forward and backward pass precisions (e.g., FP4 forward / FP8 backward). Shows that the optimal choice depends on the hardware's speedup profile — on RTX 5090, fully MXFP4 is competitive for models like Llama-7B.

3. **Minimal forward-pass error**: Uses **Hadamard rotations** before quantization to reduce outlier sensitivity. Applies **stochastic rounding** in the backward pass. Demonstrates an error-bias trade-off where techniques that minimize quantization error in the forward pass are most important.

4. **Fast GPU support**: Implements fused CUDA kernels for MXFP4 GEMMs on Blackwell architecture, with Hadamard transforms integrated into the quantization pipeline. Achieves practical speedups over FP8 baselines.

**Key architectural choice**: All three matrix multiplications of each linear layer (forward X×W, backward dL/dX, backward dL/dW) run in MXFP4, with only accumulation in higher precision.

## Results
- Pre-trained Llama-type models from 30M to 7B parameters across precision configurations
- **7B model**: FP4-trained model matches BF16 baseline quality (validated by scaling law predictions)
- **Scaling law**: Predicts that FP4 becomes increasingly attractive at larger model scales
- **Speedup**: 1.3–1.6× over FP8 on RTX 5090 prefill benchmarks
- **vs. prior FP4 methods**: Outperforms existing INT4/FP4 training approaches (e.g., Jetfire, NF4)

## Connections
- Related to: [[sources/fp4-training|FP4 Training]], [[sources/gptq|GPTQ]], [[sources/awq|AWQ]]
- Advances: [[concepts/quantization]], [[concepts/mixed-precision-training]]
- Relevant for: [[sources/nemotron-3-super|Nemotron 3 Super]] (uses NVFP4 pretraining)
- Related concepts: [[concepts/scaling-laws]], [[concepts/training-infrastructure]]

## Citation
> Castro et al., "Quartet: Native FP4 Training Can Be Optimal for Large Language Models," arXiv:2505.14669, 2025.
