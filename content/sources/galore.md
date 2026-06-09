---
type: source
arxiv_id: "2403.03507"
title: "GaLore: Memory-Efficient LLM Training by Gradient Low-Rank Projection"
authors: ["Jiawei Zhao", "Zhenyu Zhang", "Beidi Chen", "Zhangyang Wang", "Anima Anandkumar", "Yuandong Tian"]
date: 2024-03-06
org: "UT Austin / Meta / Caltech"
tags: [training, efficiency, peft, 2024]
upvotes: 190
---

# GaLore: Gradient Low-Rank Projection

> A memory-efficient training strategy that enables **full-parameter learning** while reducing optimizer state memory by up to 65.5% — for the first time enabling **pre-training a 7B model on a single 24GB consumer GPU** (NVIDIA RTX 4090) without model parallelism, checkpointing, or offloading. 1.7K GitHub stars.

## Key Contributions
- **Gradient low-rank projection**: Projects gradients into a low-rank subspace, maintaining optimizer states (Adam moments) only for the projected gradient — dramatically reducing memory
- **Full-rank weight updates**: Unlike LoRA, GaLore doesn't constrain the weight matrix to be low-rank — updates remain full-rank through periodic subspace rotation
- **7B pre-training on consumer GPU**: First demonstration of pre-training a 7B LLM on a single 24GB GPU
- **Compatible with existing techniques**: Works with 8-bit optimizers and per-layer weight updates for further savings
- **8-bit GaLore**: Reduces optimizer memory by 82.5% and total training memory by 63.3% vs. BF16 baseline

## Method
1. **Key insight**: Weight gradients during LLM training become low-rank during training, even when weight matrices are not
2. **Gradient projection**: At each step, project gradient G into a low-rank subspace via SVD: G̃ = P^T · G (or G · Q)
3. **Compact optimizer states**: Adam maintains first/second moments only for the rank-r projected gradient G̃ (r << min(m,n))
4. **Subspace switching**: Periodically recompute the projection matrix P via SVD of the gradient (every T steps)
5. **Full-rank recovery**: The update ΔW = P · G̃ has full rank because different subspaces are used over training, and their composition spans the full space

### Memory Comparison (7B model, BF16)
| Component | Full-Rank Adam | LoRA (r=128) | GaLore (r=512) | 8-bit GaLore |
|---|---|---|---|---|
| Params | 14GB | 14GB + 0.3GB | 14GB | 14GB |
| Optimizer | 28GB | 0.6GB | 4.4GB | 2.4GB |
| **Total** | **42GB** | **15GB** | **18.4GB** | **16.4GB** |

## Results
- **Pre-training**: GaLore matches full-rank training perplexity on LLaMA 1B and 7B architectures (C4 dataset, up to 19.7B tokens)
- **vs. LoRA**: GaLore outperforms LoRA at same memory budget for both pre-training and fine-tuning
- **Fine-tuning**: Matches full fine-tuning performance on GLUE tasks with RoBERTa
- **Scaling**: Successfully scaled to 7B on single RTX 4090 (24GB)

## Significance
GaLore occupies a unique niche between full fine-tuning and LoRA:
- **LoRA**: Constrains updates to low-rank subspace → limits expressivity
- **GaLore**: Projects *gradients* to low-rank → maintains full-rank *weight updates*
- This means GaLore can be used for both pre-training and fine-tuning, while LoRA typically requires full-rank warm start for pre-training

## Connections
- Builds on: [[sources/lora|LoRA]] (low-rank adaptation), Adam optimizer
- Related: [[concepts/lora-peft|LoRA/PEFT]], [[concepts/mixed-precision-training|Mixed Precision Training]]
- Concepts: [[concepts/training-infrastructure|Training Infrastructure]]

## Citation
> Zhao et al., "GaLore: Memory-Efficient LLM Training by Gradient Low-Rank Projection," ICML 2024, arXiv:2403.03507.
