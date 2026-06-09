---
type: source
arxiv_id: "2306.07629"
title: "SqueezeLLM: Dense-and-Sparse Quantization"
authors: ["Sehoon Kim", "Coleman Hooper", "Amir Gholami", "Zhen Dong", "Xiuyu Li", "Sheng Shen", "Michael W. Mahoney", "Kurt Keutzer"]
date: 2023-06-13
org: "UC Berkeley"
tags: [quantization, efficiency, inference, compression, 2023]
upvotes: 4
---

# SqueezeLLM

> A post-training quantization framework that decomposes weights into dense-and-sparse components, enabling ultra-low-bit (3-bit) quantization with minimal perplexity loss.

## Key Contributions
- Introduced **Dense-and-Sparse decomposition**: separates weight outliers into a sparse matrix, enabling the remaining dense weights to be quantized more aggressively
- Proposed **sensitivity-based non-uniform quantization**: allocates higher precision to more sensitive weight groups based on second-order information (Hessian)
- Achieved **3-bit quantization** with only 0.1–0.3 perplexity increase over FP16 on LLaMA models
- Demonstrated **2× inference speedup** over FP16 baselines with custom CUDA kernels
- Showed that the bottleneck for LLM inference is **memory bandwidth**, not compute — making quantization critical

## Method
**Key insight**: LLM weights contain a small number of outlier values that are critical for model quality. Quantizing them uniformly causes large errors. SqueezeLLM addresses this with two innovations:

1. **Dense-and-Sparse Decomposition**: Extract the top ~0.5% of weight magnitudes into a sparse matrix (stored in compressed format). The remaining dense weights can be safely quantized to 3–4 bits with minimal loss.

2. **Sensitivity-based Non-uniform Quantization**: Use Fisher information / Hessian-based sensitivity to determine how finely each weight group should be quantized. More sensitive groups get more precise centroid placement in k-means quantization.

Custom CUDA kernels exploit the sparse structure for efficient inference.

## Results
- **LLaMA-7B at 3-bit**: 7.75 PPL (vs 5.67 FP16) — much better than GPTQ 3-bit (8.07 PPL)
- **LLaMA-13B at 3-bit**: 6.56 PPL (vs 5.09 FP16) — 0.5 PPL gap
- **Inference speed**: ~2× throughput gain over FP16 on single GPU
- **Memory**: 3-bit LLaMA-30B fits on a single 48GB GPU (vs requiring 60GB+ at FP16)
- Outperforms GPTQ at matched bit-widths across all model sizes

## Datasets Used
- C4 (calibration data for quantization)
- WikiText-2, C4, PTB (perplexity evaluation)

## Connections
- **Builds on**: [[sources/gptq|GPTQ]] (post-training quantization baseline), Hessian-based sensitivity analysis
- **Complements**: [[sources/awq|AWQ]] (activation-aware approach), [[sources/qlora|QLoRA]] (quantized training)
- **Related concepts**: [[concepts/quantization|Quantization]], [[concepts/post-training-quantization|Post-Training Quantization]], [[concepts/llm-serving|LLM Serving]]
- **Influenced**: Dense-and-sparse decomposition adopted by subsequent quantization work

## Citation
> Kim et al., "SqueezeLLM: Dense-and-Sparse Quantization," arXiv:2306.07629, 2023.
