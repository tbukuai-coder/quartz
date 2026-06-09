---
type: source
arxiv_id: "2106.09685"
title: "LoRA: Low-Rank Adaptation of Large Language Models"
authors: ["Edward J. Hu", "Yelong Shen", "Phillip Wallis", "Zeyuan Allen-Zhu", "Yuanzhi Li", "Shean Wang", "Lu Wang", "Weizhu Chen"]
date: 2021-06-17
org: "Microsoft"
tags: [peft, efficiency, fine-tuning]
upvotes: 60
---

# LoRA: Low-Rank Adaptation of Large Language Models

> Introduced **Low-Rank Adaptation** — freezing pre-trained weights and injecting trainable low-rank decomposition matrices, reducing trainable parameters by 10,000× while matching full fine-tuning performance.

## Key Contributions
- Proposed injecting trainable **rank-decomposition matrices** (`A` and `B`) alongside frozen pre-trained weights
- Reduced trainable parameters by **10,000×** and GPU memory by **3×** compared to full fine-tuning
- No additional inference latency — LoRA weights can be **merged** into the base model
- Showed the method works across GPT-2, GPT-3 175B, RoBERTa, and DeBERTa
- Hypothesized and provided evidence that **pre-trained weight updates have low intrinsic rank**

## Method
For a pre-trained weight matrix `W₀ ∈ R^{d×k}`, LoRA constrains its update to:

```
W₀ + ΔW = W₀ + BA, where B ∈ R^{d×r}, A ∈ R^{r×k}, and r << min(d, k)
```

- `A` is initialized with random Gaussian; `B` is initialized to zero (so ΔW = 0 at start)
- Applied to attention weight matrices (Wq, Wv) — but can be applied anywhere
- Rank `r` can be as low as 1–4 and still achieve competitive performance
- At inference, merge `BA` into `W₀` — zero additional cost

## Results
- **GPT-3 175B**: With r=4, matches or exceeds full fine-tuning on multiple benchmarks
- **RoBERTa/DeBERTa**: Comparable to full fine-tuning on GLUE
- 10,000× fewer trainable parameters; 3× less memory; no inference overhead
- Enables serving multiple task-specific models by swapping small LoRA weights

## Connections
- **Extended by**: [[sources/qlora]] (adds 4-bit quantization)
- **Key concepts**: [[concepts/lora-peft]], [[concepts/fine-tuning]], [[concepts/quantization]]
- **Implemented in**: Hugging Face PEFT library — see [[entities/orgs/huggingface]]
- **Organizations**: Microsoft

## Citation
> Hu et al., "LoRA: Low-Rank Adaptation of Large Language Models," arXiv:2106.09685, 2021.
> https://huggingface.co/papers/2106.09685
