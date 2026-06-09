---
type: comparison
tags: [quantization, efficiency, inference, training, 2024, 2025]
---

# Quantization Landscape: From FP16 to 1.58-bit

> Comparing post-training quantization, quantization-aware training, and low-precision training approaches for LLMs and image generation models.

## Overview
Quantization is the single most impactful technique for making LLMs deployable on consumer hardware. The field has evolved from basic 4-bit compression to sophisticated methods that maintain near-full quality at extreme compression ratios, and from inference-only to training-time low precision.

## Post-Training Quantization (Inference)

| Method | Year | Bits | Approach | Quality (PPL gap) | Speed |
|---|---|---|---|---|---|
| [[sources/gptq\|GPTQ]] | 2022 | 3–4 bit | Second-order weight quantization | ~0.5 PPL | 3–4× memory savings |
| [[sources/squeezellm\|SqueezeLLM]] | 2023 | 3 bit | Dense-and-sparse decomposition | ~0.3 PPL (better than GPTQ) | 2× inference speedup |
| [[sources/awq\|AWQ]] | 2023 | 4 bit | Activation-aware weight quantization | ~0.1 PPL | Fast, hardware-friendly |
| GGUF/llama.cpp | 2023 | 2–8 bit | K-quant mixed precision | Varies | CPU-optimized |
| [[sources/158-bit-flux\|1.58-bit FLUX]] | 2024 | 1.58 bit | Ternary self-supervised | Minimal (GenEval 0.71 vs 0.73) | 6× model size reduction |

## Training-Time Low Precision

| Method | Year | Precision | Stage | Quality vs BF16 |
|---|---|---|---|---|
| BF16 | Standard | 16-bit | Training | Baseline |
| FP8 ([[sources/deepseek-v3\|DeepSeek-V3]]) | 2024 | 8-bit | Pre-training | Negligible loss |
| [[sources/fp4-training\|FP4 Training]] | 2025 | 4-bit | Pre-training | 0.1–0.3 PPL gap |

## Key Insights

1. **AWQ is the current standard** for inference quantization — best quality/speed tradeoff at 4-bit
2. **SqueezeLLM's dense-and-sparse idea** is powerful — separating outliers enables more aggressive quantization
3. **3-bit is practical** for most models with SqueezeLLM or GPTQ
4. **FP8 training is production-ready** — validated at 671B scale by DeepSeek
5. **FP4 training is emerging** — could halve training memory requirements
6. **Extreme quantization (1.58-bit)** works surprisingly well for image generation models
7. **The bottleneck is memory bandwidth**, not compute — making quantization the most effective optimization

## The Quantization Stack

```
Training:    FP32 → BF16 → FP8 → FP4 (frontier)
Inference:   FP16 → INT8 → INT4 (GPTQ/AWQ) → INT3 (SqueezeLLM) → Ternary (1.58-bit)
On-device:   GGUF Q4_K_M (sweet spot for CPU inference)
```

## See Also
- [[concepts/quantization|Quantization]]
- [[concepts/post-training-quantization|Post-Training Quantization]]
- [[concepts/mixed-precision-training|Mixed Precision Training]]
- [[concepts/llm-serving|LLM Serving]]
