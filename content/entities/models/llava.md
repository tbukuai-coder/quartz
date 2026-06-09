---
type: entity
category: model
tags: [multimodal, vision-language, open-source]
---

# LLaVA (Large Language and Vision Assistant)

> The foundational **open-source multimodal model** paradigm — connecting a CLIP vision encoder to an LLM via a projection layer, establishing the template used by virtually all open multimodal models.

## Overview
LLaVA introduced the simple but effective pattern of "vision encoder + projection + LLM" for multimodal understanding. The LLaVA paradigm has been adopted and extended by numerous subsequent models, making it the most influential open-source multimodal architecture.

## Model Family
| Model | Year | Vision | LLM | Key Feature |
|---|---|---|---|---|
| LLaVA | 2023 | CLIP ViT-L/14 | Vicuna 13B | First visual instruction tuning |
| LLaVA-1.5 | 2023 | CLIP ViT-L/14-336 | Vicuna 7B/13B | MLP projection, better data |
| LLaVA-NeXT | 2024 | Various | Various | Dynamic resolution, stronger LLMs |
| LLaVA-o1 | 2024 | Various | Various | Step-by-step reasoning |

## The LLaVA Paradigm
```
Image → Vision Encoder (CLIP) → Projection (MLP) → LLM → Response
```
This pattern is now used by: [[sources/gemma-3|Gemma 3]], [[sources/llama-3|Llama 3.2 Vision]], Qwen-VL, InternVL, and many others.

## Related Papers
- [[sources/llava]] — Original LLaVA paper

## See Also
- [[concepts/multimodal-models]]
- [[concepts/instruction-tuning]]
