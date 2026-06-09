---
type: source
arxiv_id: "2210.17323"
title: "GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers"
authors: ["Elias Frantar", "Saleh Ashkboos", "Torsten Hoefler", "Dan Alistarh"]
date: 2022-10-31
org: "IST Austria / ETH Zurich"
tags: [quantization, efficiency, inference, post-training]
upvotes: 10
---

# GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers

> A one-shot weight quantization method based on approximate second-order information that compresses LLMs to 3–4 bits with negligible accuracy loss, enabling 175B parameter models to run on a single GPU.

## Key Contributions
- Introduced GPTQ, a post-training quantization algorithm that extends Optimal Brain Quantization (OBQ) to scale to models with hundreds of billions of parameters
- Achieved 3–4 bit quantization of GPT-175B in ~4 GPU hours with negligible perplexity degradation
- Demonstrated first-ever execution of a 175B-parameter model on a single GPU for generative inference
- Showed 3.25× speedup on A100 and 4.5× speedup on A6000 vs. FP16 inference
- Proved that even extreme 2-bit and ternary quantization can yield reasonable accuracy

## Method
GPTQ builds on the Optimal Brain Quantization (OBQ) framework but introduces three key modifications for scalability:

1. **Arbitrary Order Processing**: Instead of greedy order (quantizing the weight with least error first), GPTQ quantizes weights in arbitrary (fixed) order. This enables batched computation with negligible accuracy loss.
2. **Lazy Batch Updates**: Groups of columns (e.g., 128) are processed together, with updates applied in blocks rather than one-at-a-time. This dramatically improves GPU utilization.
3. **Cholesky-based Computation**: Uses Cholesky decomposition to compute the inverse Hessian information numerically stably, avoiding the accumulation of numerical errors.

The algorithm processes each layer independently (layer-wise quantization), using a small calibration set (128 samples from C4) to compute activation statistics. No backpropagation or end-to-end fine-tuning is required.

## Results
| Model | Bits | Wiki2 PPL | Speedup |
|---|---|---|---|
| OPT-175B (FP16) | 16 | 8.34 | 1× |
| OPT-175B (GPTQ) | 4 | 8.68 | 3.25× (A100) |
| OPT-175B (GPTQ) | 3 | 9.56 | 4.5× (A6000) |
| BLOOM-176B (FP16) | 16 | 8.11 | 1× |
| BLOOM-176B (GPTQ) | 4 | 8.38 | — |

Key result: 4-bit GPTQ maintains <0.5 perplexity increase on WikiText2 for most model sizes, while reducing memory by ~4×.

## Datasets Used
- C4 (128 random samples for calibration)
- WikiText2, Penn Treebank, C4 (for evaluation)

## Models Quantized
- OPT family (125M to 175B)
- BLOOM family (560M to 176B)

## Connections
- Builds on: Optimal Brain Surgeon (OBS), Optimal Brain Quantization (OBQ)
- Extended by: [[sources/awq|AWQ]] (activation-aware approach), AutoGPTQ (widely-used implementation)
- Complementary to: [[sources/qlora|QLoRA]] (uses GPTQ-style quantization for training)
- Related concepts: [[concepts/quantization|Quantization]], [[concepts/post-training-quantization|Post-Training Quantization]]
- Ecosystem impact: Thousands of GPTQ-format models on Hugging Face Hub; supported by [[sources/vllm|vLLM]], TGI, llama.cpp, text-generation-webui

## Citation
> Frantar et al., "GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers," arXiv:2210.17323, 2022.
