---
type: source
arxiv_id: "2501.17116"
title: "Optimizing Large Language Model Training Using FP4 Quantization"
authors: ["Ruizhe Wang", "Yeyun Gong", "Various"]
date: 2025-01-28
org: "Microsoft / Various"
tags: [training, quantization, efficiency, fp4, 2025]
upvotes: 36
---

# FP4 Training

> First framework demonstrating that LLMs can be pre-trained in 4-bit floating point (FP4) with accuracy comparable to BF16 and FP8, pushing the low-precision training frontier.

## Key Contributions
- Demonstrated **FP4 pre-training** of LLMs with accuracy comparable to BF16 and FP8 baselines
- Introduced **differentiable quantization** that allows gradients to flow through the quantization operator
- Proposed **outlier clamping** strategy to handle activation outliers during FP4 training
- Showed **2× memory reduction** over FP8 and **4× over BF16** for weight storage during training
- Validated on models up to 13B parameters

## Method
**FP4 format**: Uses E2M1 (2 exponent bits, 1 mantissa bit) format with microscaling (per-group scale factors).

Key innovations:
1. **Differentiable quantization**: Instead of straight-through estimator (STE), uses a smooth approximation that preserves gradient information
2. **Outlier clamping**: Clip activation outliers before quantization to prevent catastrophic representation errors
3. **Mixed precision**: FP4 for weights and activations in forward pass; accumulation and gradients at higher precision (FP8/BF16)
4. **Progressive training**: Optionally start at FP8 and transition to FP4 after initial warm-up

## Results
- **LLaMA-7B equivalent**: FP4 training achieves perplexity within 0.1–0.3 of BF16 baseline
- **LLaMA-13B equivalent**: Similar minimal degradation at larger scale
- **Memory**: 2× less memory than FP8 training for weights
- **Convergence**: Comparable training curves to FP8, slightly behind BF16 initially but catches up

## Connections
- **Extends**: [[sources/deepseek-v3|DeepSeek-V3]] (FP8 training at scale), [[concepts/mixed-precision-training|Mixed Precision Training]]
- **Related concepts**: [[concepts/quantization|Quantization]], [[concepts/training-infrastructure|Training Infrastructure]]
- **Implications**: Could enable frontier model training on fewer GPUs

## Citation
> Wang et al., "Optimizing Large Language Model Training Using FP4 Quantization," arXiv:2501.17116, 2025.
