---
type: source
arxiv_id: "2504.12285"
title: "BitNet b1.58 2B4T Technical Report"
authors: ["Shuming Ma", "Hongyu Wang", "Shaohan Huang", "Xingxing Zhang"]
date: 2025-04-16
org: "Microsoft"
tags: [quantization, efficiency, 1-bit, small-model, 2025]
upvotes: 85
---

# BitNet b1.58 2B4T

> The first open-source native 1-bit LLM (1.58-bit ternary weights) at 2B scale, trained from scratch on 4T tokens, matching full-precision models while offering massive efficiency gains.

## Key Contributions
- First **open-source native 1-bit LLM** at meaningful scale (2B parameters, 4T tokens)
- Achieves performance **on par with full-precision LLMs** of similar size (Llama 3.2 1B, Gemma 3 1B)
- **Ternary weights** ({-1, 0, 1}) enable inference with additions/subtractions only — no multiplication needed
- Significant improvements in **memory footprint, energy consumption, and decoding latency**
- Released with inference implementations for both **GPU and CPU**

## Method
BitNet b1.58 trains models natively in 1.58-bit precision from scratch (not post-training quantized). Key design:
- **Weight quantization**: All linear layer weights constrained to {-1, 0, 1} during training using straight-through estimators
- **Activation quantization**: 8-bit quantization for activations
- **Training**: Standard pre-training on 4T tokens with absmean weight quantization
- **Architecture**: Standard Transformer with RMSNorm, SwiGLU, RoPE — same template as modern LLMs

## Results
- **MMLU**: Competitive with Llama 3.2 1B and Gemma 3 1B
- **GSM8K**: Comparable math reasoning
- **HumanEval**: Competitive code generation
- **Memory**: ~10× reduction vs FP16 (weights stored as 2-bit)
- **Latency**: Significant decoding speedup on both CPU and GPU
- **Energy**: Major reduction in energy consumption per token

## Models Released
- BitNet b1.58 2B4T (open weights + inference code)

## Connections
- **Related**: [[sources/158-bit-flux|1.58-bit FLUX]] (ternary quantization for image gen), [[sources/squeezellm|SqueezeLLM]]
- **Org**: [[entities/orgs/microsoft|Microsoft]]
- **Related concepts**: [[concepts/quantization|Quantization]], [[concepts/post-training-quantization|PTQ]]
- **Comparison**: [[comparisons/quantization-landscape|Quantization Landscape]], [[comparisons/small-language-models|Small Language Models]]
- **Significance**: Proves 1-bit training is viable for production LLMs — could fundamentally change deployment economics

## Citation
> Ma et al., "BitNet b1.58 2B4T Technical Report," arXiv:2504.12285, 2025.
