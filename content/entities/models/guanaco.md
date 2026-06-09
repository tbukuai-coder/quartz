---
type: entity
category: model
tags: [peft, qlora, chat]
---

# Guanaco

> QLoRA-trained chat models (7B–65B) — demonstrated that **4-bit quantized fine-tuning** on a single GPU can produce models reaching 99.3% of ChatGPT performance.

## Overview
Guanaco models were the headline result of the QLoRA paper. Fine-tuned from LLaMA using QLoRA on the OASST1 dataset, Guanaco-65B achieved 99.3% of ChatGPT's performance on the Vicuna benchmark while requiring only a single 48GB GPU for training.

## Key Details
- **Base models**: LLaMA 7B, 13B, 33B, 65B
- **Method**: QLoRA (4-bit NF4 + LoRA adapters)
- **Training data**: [[entities/datasets/oasst|OASST1]] (Open Assistant)
- **Hardware**: Single 48GB GPU (65B), single 24GB GPU (33B)
- **Vicuna benchmark**: 99.3% of ChatGPT (65B version)

## Related Papers
- [[sources/qlora]] — QLoRA paper

## See Also
- [[entities/models/llama]]
- [[concepts/lora-peft]]
- [[concepts/quantization]]
