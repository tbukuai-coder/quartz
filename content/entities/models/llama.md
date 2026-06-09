---
type: entity
category: model
tags: [open-models, meta, foundational]
---

# LLaMA / Llama

> Meta's family of open-weight foundation language models — the catalyst for the open-source LLM revolution, spanning four generations from 1B to 405B+ parameters.

## Overview
LLaMA (Large Language Model Meta AI) is the most influential open-source model family. The release of LLaMA 1 weights in 2023 kicked off an explosion of community fine-tuning, alignment work, and derivative models (Alpaca, Vicuna, Guanaco, etc.). Llama 2 added official chat models. Llama 3/3.1 pushed to 405B parameters. Llama 4 shifted to MoE architecture with native multimodality.

## Model Generations

| Generation | Year | Sizes | Training Data | Key Innovation |
|---|---|---|---|---|
| LLaMA 1 | 2023 | 7B, 13B, 33B, 65B | 1–1.4T tokens (public) | Proved public data is enough |
| Llama 2 | 2023 | 7B, 13B, 70B | 2T tokens | First open RLHF chat models |
| Llama 3 / 3.1 / 3.2 | 2024 | 1B–405B | 15T+ tokens | Scaled to frontier; added multimodal |
| Llama 4 | 2025 | MoE variants | Undisclosed | MoE architecture, early-fusion multimodal, iRoPE |

## Specialized Variants
- **[[sources/code-llama|Code Llama]]**: Code-specialized models (7B–34B) with infilling and 100K context
- **Llama Guard**: Safety classifier models
- **Llama 3.2 Vision**: Multimodal (11B, 90B) with image understanding

## Architecture
- Transformer decoder-only (autoregressive)
- **RMSNorm** (pre-normalization)
- **SwiGLU** activation
- **Rotary Positional Embeddings (RoPE)**
- **Grouped-Query Attention (GQA)** (from Llama 2 onward)

This architecture template has become the de facto standard — adopted by [[entities/models/mistral]], [[entities/models/qwen]], [[entities/models/deepseek]], and others.

## Related Papers
- [[sources/llama]] — LLaMA 1 paper
- [[sources/llama-2]] — Llama 2 paper (with alignment details)
- [[sources/llama-3]] — Llama 3 paper (405B, multimodal)
- [[sources/llama-4]] — Llama 4 paper (MoE architecture shift)
- [[sources/code-llama]] — Code Llama (code specialization)

## Ecosystem Impact
- **Alpaca** (Stanford): Self-Instruct fine-tuning of LLaMA 7B
- **Vicuna**: ShareGPT conversation fine-tuning
- [[entities/models/guanaco]]: QLoRA fine-tuning
- Thousands of community fine-tunes on Hugging Face Hub

## See Also
- [[entities/orgs/meta]]
- [[concepts/pre-training]]
- [[concepts/rlhf]]
