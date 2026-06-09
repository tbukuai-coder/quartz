---
type: source
arxiv_id: "2306.00978"
title: "AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration"
authors: ["Ji Lin", "Jiaming Tang", "Haotian Tang", "Shang Yang", "Wei-Ming Chen", "Wei-Chen Wang", "Guangxuan Xiao", "Xingyu Dang", "Chuang Gan", "Song Han"]
date: 2023-06-01
org: "MIT HAN Lab"
tags: [quantization, efficiency, inference, edge-deployment]
upvotes: 12
---

# AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration

> A hardware-friendly weight quantization method that identifies and protects 1% of salient weight channels based on activation distributions, achieving superior quantization quality and enabling 70B model deployment on mobile GPUs.

## Key Contributions
- Discovered that only ~1% of weights are critical for LLM accuracy, and these can be identified from activation magnitudes (not weight magnitudes)
- Proposed per-channel scaling to protect salient weights — mathematically equivalent transformation that avoids mixed-precision hardware overhead
- Achieved superior generalization: works across instruction-tuned, code, math, and multimodal LLMs without task-specific calibration
- Built TinyChat inference framework achieving 3× speedup over HF FP16 on desktop and mobile GPUs
- First to deploy Llama-2-70B on mobile GPUs (NVIDIA Jetson Orin)

## Method
AWQ is based on three key insights:

1. **Observation**: Not all weights are equally important. Keeping just 1% of salient channels in FP16 (based on activation magnitude) dramatically reduces quantization error — but mixed-precision is hardware-inefficient.
2. **Equivalent Transformation**: Instead of mixed precision, AWQ scales up salient channels before quantization. Mathematically, this is equivalent to dividing activations and multiplying weights by the same factor, which reduces relative quantization error for important channels.
3. **Optimal Scale Search**: The per-channel scaling factors are determined by analyzing the activation distribution on a small calibration set (offline, no gradient computation needed). The optimal scale balances quantization error reduction on salient channels vs. error increase on non-salient channels.

AWQ requires no backpropagation, no reconstruction, and no regression — making it extremely fast and generalizable across domains.

**TinyChat** implements AWQ with:
- SIMD-aware weight packing for ARM NEON
- Kernel fusion for attention, normalization, and linear layers
- Platform-aware optimization for desktop GPUs (CUDA), mobile GPUs (Orin), and laptops

## Results
| Model | Method | Bits | Wiki2 PPL ↓ |
|---|---|---|---|
| Llama-2-7B | FP16 | 16 | 5.47 |
| Llama-2-7B | GPTQ | 4 | 5.62 |
| Llama-2-7B | AWQ | 4 | 5.60 |
| Llama-2-7B | GPTQ | 3 | 6.43 |
| Llama-2-7B | AWQ | 3 | 6.24 |
| Llama-2-70B | AWQ | 4 | 3.41 |

Key: AWQ consistently matches or outperforms [[sources/gptq|GPTQ]] at both 3-bit and 4-bit, while being faster to calibrate and better at generalizing to instruction-tuned and multimodal models.

**Throughput (tokens/sec on A100):**
- VILA-7B FP16: 81.6 → VILA-7B AWQ: 155.3 (1.9× speedup)
- VILA-13B FP16: 48.5 → VILA-13B AWQ: 102.1 (2.1× speedup)

## Datasets Used
- Pile (small calibration set, 128 samples)
- WikiText2, C4 (evaluation)
- Various instruction-following benchmarks (Vicuna, GPT-4 eval)

## Models Quantized
- LLaMA family (7B–65B)
- [[entities/models/llama|Llama 2]] (7B–70B)
- Vicuna, Code LLMs, math LLMs
- VILA (multimodal)

## Connections
- Builds on: [[sources/gptq|GPTQ]] (improves on its approach), SmoothQuant (activation-aware idea for W8A8)
- Related: [[sources/qlora|QLoRA]] (quantized training vs. quantized inference)
- Related concepts: [[concepts/quantization|Quantization]], [[concepts/post-training-quantization|Post-Training Quantization]]
- Ecosystem: AutoAWQ (7K+ GitHub stars), native support in [[sources/vllm|vLLM]], TGI, and HF Transformers; thousands of AWQ models on HF Hub
- Used in: TinyChat, On-device inference for mobile deployment

## Citation
> Lin et al., "AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration," MLSys 2024, arXiv:2306.00978, 2023.
