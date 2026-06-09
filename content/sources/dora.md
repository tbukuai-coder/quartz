---
type: source
arxiv_id: "2402.09353"
title: "DoRA: Weight-Decomposed Low-Rank Adaptation"
authors: ["Shih-Yang Liu", "Chien-Yi Wang", "Hongxu Yin", "Pavlo Molchanov", "Yu-Chiang Frank Wang", "Kwang-Ting Cheng", "Min-Hung Chen"]
date: 2024-02-14
org: "NVIDIA / NTHU"
tags: [peft, lora, adapter, fine-tuning, efficiency, 2024]
upvotes: 32
---

# DoRA — Weight-Decomposed Low-Rank Adaptation

> Decomposes pre-trained weights into magnitude and direction, applying LoRA only to the direction component — closing the gap between LoRA and full fine-tuning. Integrated into PEFT (`use_dora=True`).

## Key Contributions
- **Weight decomposition analysis**: Reveals that full fine-tuning updates both magnitude and direction of weight vectors, while LoRA disproportionately updates magnitude — explaining the accuracy gap
- **DoRA method**: Decomposes W = m · (V/‖V‖) where m is magnitude (scalar per column) and V/‖V‖ is direction (unit vector). Applies LoRA to V (direction) only, with m as a separate trainable parameter
- **Closes LoRA-to-full-FT gap**: Matches or exceeds full fine-tuning performance with LoRA-level parameter efficiency
- **Drop-in replacement**: Works with any LoRA variant (LoRA, VeRA, etc.) — just decompose and apply

## Method
1. **Decompose**: Split pre-trained weight W into magnitude m = ‖W‖_c (column norms) and direction V = W (will be normalized)
2. **Apply LoRA to direction**: V' = V + BA (standard LoRA delta)
3. **Normalize**: Direction component = V'/‖V'‖_c
4. **Combine**: W' = m · (V'/‖V'‖_c) where m is also trainable
5. **Key insight**: Full FT exhibits large direction changes but small magnitude changes. LoRA conflates both. DoRA separates them, allowing independent optimization

## Results
- **Commonsense reasoning** (LLaMA-7B): DoRA > LoRA by 1-3% across 8 benchmarks, matching full FT
- **Visual instruction tuning** (LLaVA-7B): DoRA closes gap to full FT on VQAv2, GQA, ScienceQA
- **Image/video understanding** (VL-BART): Consistent improvements over LoRA
- **Parameter efficiency**: Same number of trainable parameters as LoRA (m adds negligible overhead)
- **Training stability**: More stable learning curves than LoRA, especially at low ranks
- Integrated in HF PEFT library: `peft_config = LoraConfig(..., use_dora=True)`

## Connections
- Extends: [[sources/lora|LoRA]] (adds magnitude/direction decomposition)
- Related: [[sources/qlora|QLoRA]] (quantized LoRA), [[concepts/lora-peft|LoRA/PEFT concept]]
- Also see: IA3, AdaLoRA (other PEFT variants)
- Concepts: [[concepts/lora-peft|LoRA / PEFT]]

## Citation
> Liu et al., "DoRA: Weight-Decomposed Low-Rank Adaptation," ICML 2024, arXiv:2402.09353.
