---
type: concept
tags: [multimodal, vlm, vision, architecture]
---

# Vision-Language Models (VLMs)

> Models that jointly process images/video and text, enabling visual question answering, document understanding, and visual reasoning.

## Overview
Vision-Language Models combine a vision encoder (typically a ViT) with a large language model to understand and reason about visual content. Starting with early models like Flamingo (2022), the field has rapidly evolved to produce models that rival GPT-4V in visual understanding while remaining fully open-source. The key design choices are: vision encoder selection, how to connect vision to language (architecture), image tokenization strategy, and training data composition.

## How It Works

### Architecture Patterns
Most modern VLMs follow the **ViT-Connector-LLM** paradigm:
1. **Vision encoder** processes the image → visual embeddings
2. **Connector** projects visual embeddings into the LLM's token space
3. **LLM** processes interleaved visual and text tokens autoregressively

**Connector types** (ablated in [[sources/idefics2|Idefics2]]):
- **MLP projection**: Simple, effective — used by LLaVA, InternVL
- **Perceiver resampler**: Compresses visual tokens — but [[sources/idefics2|Idefics2]] showed it can hurt performance
- **Pixel shuffle pooling**: 4× token reduction with no quality loss — used by [[sources/smolvlm|SmolVLM]]
- **Cross-attention**: Visual tokens attend into LLM layers — used by Flamingo/IDEFICS

### Image Resolution Handling
- **Fixed resolution**: Resize all images to 224×224 or 336×336 — simple but loses detail
- **Sub-image splitting**: Divide into tiles ([[sources/idefics2|Idefics2]], [[sources/llava|LLaVA-NeXT]])
- **Dynamic tiles**: Adapt tile count to image complexity ([[sources/internvl-1-5|InternVL 1.5]]: 1–40 tiles)
- **Native dynamic resolution**: Train ViT from scratch on variable sizes ([[sources/qwen25-vl|Qwen2.5-VL]])

### Key Design Findings
| Finding | Source |
|---|---|
| Perceiver resampler hurts vs. full tokens | [[sources/idefics2\|Idefics2]] |
| Pixel shuffle pooling recovers quality at 4× compression | [[sources/smolvlm\|SmolVLM]] |
| Larger LLMs benefit more from larger vision encoders | [[sources/internvl-1-5\|InternVL 1.5]] |
| OCR/document data critical for real-world performance | [[sources/idefics2\|Idefics2]] |
| Smaller vision encoders complement compact LMs | [[sources/smolvlm\|SmolVLM]] |

## Evolution

```
Flamingo (2022) — Cross-attention, frozen LLM
  → LLaVA (2023) — Simple projection, full fine-tuning
    → IDEFICS (2023) — Open Flamingo reproduction
      → Idefics2 (2024) — Rigorous ablation, MLP connector
        → InternVL 1.5 (2024) — 6B vision encoder, dynamic tiles
          → Qwen2.5-VL (2025) — Native dynamic resolution, M-RoPE
          → InternVL 2.5 (2024) — MMMU >70%, test-time scaling
          → SmolVLM (2025) — 256M–2.2B, on-device deployment
```

## Key Papers
- [[sources/llava|LLaVA]] (2023) — visual instruction tuning paradigm
- [[sources/idefics2|Idefics2]] (2024) — comprehensive VLM design ablation
- [[sources/internvl-1-5|InternVL 1.5]] (2024) — strong vision encoder + dynamic resolution
- [[sources/internvl-2-5|InternVL 2.5]] (2024) — first open MLLM >70% MMMU
- [[sources/qwen25-vl|Qwen2.5-VL]] (2025) — native dynamic resolution, video + agent
- [[sources/smolvlm|SmolVLM]] (2025) — efficient small VLMs for edge deployment

## See Also
- [[concepts/multimodal-models|Multimodal Models]]
- [[concepts/transformer-architecture|Transformer Architecture]]
- [[concepts/self-attention|Self-Attention]]
