---
type: concept
tags: [efficiency, peft, fine-tuning, lora, dora]
---

# LoRA / PEFT (Parameter-Efficient Fine-Tuning)

> Methods for adapting large models by training only a **tiny fraction of parameters** — reducing memory, compute, and storage requirements by orders of magnitude while matching full fine-tuning performance.

## Overview
As models grew to billions of parameters, full fine-tuning became impractical. PEFT methods train a small number of additional or modified parameters while keeping the base model frozen. LoRA is by far the most popular approach, with DoRA as the latest evolution.

## LoRA (Low-Rank Adaptation)
Introduced in [[sources/lora|Hu et al. 2021]]:
- For weight matrix `W₀`, add: `ΔW = BA` where `B ∈ R^{d×r}`, `A ∈ R^{r×k}`, `r << min(d,k)`
- Typical rank: r=4 to r=64
- Applied to attention weights (Wq, Wk, Wv, Wo) and sometimes FFN weights
- **At inference: merge BA into W₀ — zero additional latency**
- 10,000× fewer trainable parameters; 3× less memory

## DoRA (Weight-Decomposed LoRA)
Introduced in [[sources/dora|Liu et al. 2024]]:
- Decomposes weight W into **magnitude** m (column norms) and **direction** V/‖V‖
- Applies LoRA only to direction, trains magnitude separately
- **Closes the gap** between LoRA and full fine-tuning
- Key insight: full FT changes direction a lot but magnitude little; LoRA conflates both
- Drop-in replacement: `peft_config = LoraConfig(..., use_dora=True)`

## QLoRA (Quantized LoRA)
Introduced in [[sources/qlora|Dettmers et al. 2023]]:
- Base model quantized to **4-bit NF4**
- LoRA adapters trained in BF16
- Backpropagation through frozen quantized weights
- Enables fine-tuning 65B model on **single 48GB GPU**

## Other PEFT Methods
| Method | Approach | Parameters |
|---|---|---|
| **LoRA** | Low-rank adapter matrices | ~0.01% |
| **DoRA** | LoRA + magnitude/direction decomposition | ~0.01% |
| **QLoRA** | LoRA + 4-bit quantization | ~0.01% |
| **Adapters** | Small bottleneck layers inserted between Transformer layers | ~1-5% |
| **Prefix Tuning** | Learnable prefix tokens prepended to KV cache | ~0.1% |
| **Prompt Tuning** | Learnable soft prompt tokens | ~0.01% |
| **IA3** | Learned vectors that rescale attention and FFN activations | ~0.01% |

## Practical Considerations
- **LoRA rank**: r=8 is a good default; r=4 works for many tasks; r=64+ for complex tasks
- **DoRA**: Use when you need to close the gap to full FT; slight training overhead vs. LoRA
- **Target modules**: At minimum Wq, Wv; for best results all attention + FFN weights
- **Alpha**: LoRA scaling factor, typically `alpha = 2 × rank`
- **Merging**: Multiple LoRA adapters can be merged for multi-task models; see [[concepts/model-merging]]

## Key Papers
- [[sources/lora]] — LoRA (foundational)
- [[sources/dora]] — DoRA (magnitude/direction decomposition)
- [[sources/qlora]] — QLoRA (4-bit quantized training)

## See Also
- [[concepts/fine-tuning]]
- [[concepts/quantization]]
- [[concepts/model-merging]]
