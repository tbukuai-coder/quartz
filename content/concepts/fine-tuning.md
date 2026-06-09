---
type: concept
tags: [training, foundational]
---

# Fine-tuning

> Adapting a pre-trained model to a specific task or domain by continuing training on task-specific data — the second stage in the pre-train → fine-tune paradigm.

## Overview
Fine-tuning takes a pre-trained model and specializes it. The model's general knowledge is preserved while it learns task-specific behavior. This is far more efficient than training from scratch.

## Variants

### Full Fine-tuning
- Update **all model parameters** on task-specific data
- Best performance but highest compute/memory cost
- Impractical for very large models (175B+)

### Parameter-Efficient Fine-tuning (PEFT)
- Update only a **small subset** of parameters
- [[concepts/lora-peft|LoRA]]: Low-rank adapter matrices (~0.01% of parameters)
- [[concepts/quantization|QLoRA]]: LoRA + 4-bit quantization
- Adapters, prefix tuning, prompt tuning — various approaches

### Supervised Fine-tuning (SFT)
- Fine-tune on (instruction, response) pairs
- The first step of the alignment pipeline
- See [[concepts/instruction-tuning]]

## Key Papers
- [[sources/bert]] — Established fine-tuning paradigm
- [[sources/lora]] — Parameter-efficient fine-tuning
- [[sources/qlora]] — Quantized fine-tuning
- [[sources/instructgpt]] — SFT as alignment step

## See Also
- [[concepts/pre-training]]
- [[concepts/lora-peft]]
- [[concepts/instruction-tuning]]
- [[concepts/rlhf]]
