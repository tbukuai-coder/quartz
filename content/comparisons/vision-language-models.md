---
type: comparison
tags: [multimodal, vlm, vision, 2024, 2025]
---

# Comparison: Vision-Language Models (2024–2025)

> How the major open-source VLM families compare in architecture, scale, and performance — from 256M to 78B parameters.

## Overview

Vision-Language Models have rapidly evolved from early research prototypes (Flamingo, 2022) to production-quality systems rivaling GPT-4V. By 2025, three lineages dominate the open-source landscape: the **InternVL** series (Shanghai AI Lab), the **Qwen-VL** series (Alibaba), and the **HF-native** line (Hugging Face: IDEFICS → Idefics2 → SmolVLM). Each makes different trade-offs between scale, efficiency, and capability.

## Comparison Table

| Aspect | InternVL 1.5 | InternVL 2.5 | Qwen2.5-VL | Idefics2 | SmolVLM | Aya Vision |
|---|---|---|---|---|---|---|
| **Paper** | [[sources/internvl-1-5]] | [[sources/internvl-2-5]] | [[sources/qwen25-vl]] | [[sources/idefics2]] | [[sources/smolvlm]] | [[sources/aya-vision]] |
| **Date** | Apr 2024 | Dec 2024 | Feb 2025 | May 2024 | Apr 2025 | May 2025 |
| **Org** | Shanghai AI Lab | Shanghai AI Lab | Alibaba | Hugging Face | Hugging Face | Cohere For AI |
| **Sizes** | 26B | 1B–78B | 3B/7B/72B | 8B | 256M/500M/2.2B | 8B/32B |
| **Vision Encoder** | InternViT-6B | InternViT-300M/6B | Native dynamic ViT | SigLIP-SO400M | SigLIP-B/16 (93M) | Standard ViT |
| **LLM Backbone** | InternLM2-20B | Various (1.8B–78B) | Qwen2.5 | Mistral-7B | SmolLM2 | Aya text foundation |
| **Connector** | 2-layer MLP | 2-layer MLP | MLP | Learned pooling | Pixel shuffle | MLP projection |
| **Image Resolution** | Dynamic tiles (1–40×448²) | Dynamic tiles | Native dynamic | Sub-image split | Pixel shuffle 4× | Standard |
| **Video** | Limited | ✅ Strong | ✅ Hours-long | ❌ | ✅ Basic | Limited |
| **Multilingual** | Limited | Limited | ✅ Strong | Limited | Limited | **✅ Best-in-class** |
| **Agent/Tool Use** | ❌ | Limited | ✅ Computer/phone use | ❌ | ❌ | ❌ |
| **Min VRAM** | ~16GB | ~2GB (1B) | ~4GB (3B) | ~16GB | **<1GB** (256M) | ~8GB (8B) |
| **License** | Apache 2.0 | Apache 2.0 | Apache 2.0 | Apache 2.0 | Apache 2.0 | Apache 2.0 |

## Omni-Modal Streaming Comparison (2026)

| Aspect | MiniCPM-o 4.5 | Qwen3-Omni | VITA-1.5 | Nemotron 3 Nano Omni |
|---|---|---|---|---|
| **Paper** | [[sources/minicpm-o-4-5]] | Qwen3-Omni | [[sources/vita-1-5]] | [[sources/nemotron-3-nano-omni]] |
| **Date** | Apr 2026 | 2025 | Jan 2025 | Apr 2026 |
| **Org** | OpenBMB (THU) | Alibaba | Shanghai AI Lab | NVIDIA |
| **Size** | **9B** | 30B-A3B | 8B | 30B-A3B |
| **Modalities** | Text, Vision, Audio, Speech | Text, Vision, Audio, Speech | Text, Vision, Speech | Text, Vision, Audio, Speech |
| **Interaction** | **Full-duplex streaming** | Turn-based | Turn-based | Turn-based |
| **Proactive** | **✅ Yes** | ❌ No | ❌ No | ❌ No |
| **Min VRAM** | **<12GB** | ~24GB | ~16GB | ~24GB |
| **Speech Quality** | **SOTA open** | Good | Good | Good |
| **Vision Quality** | Approaches Gemini 2.5 Flash | Strong | GPT-4o-level | Strong |
| **Architecture** | End-to-end token-level | Compositional | Compositional | Compositional |
| **Voice Cloning** | **✅ Yes** | Limited | ❌ No | Limited |
| **GitHub Stars** | **24.5K** | — | 2.5K | — |

### Key Insight: Turn-Based vs Full-Duplex
The omni-modal models of 2024–2025 (VITA-1.5, Qwen3-Omni, Nemotron 3 Nano Omni) all share the same fundamental paradigm: **alternating perception and response phases**. The model listens, then thinks, then speaks, then listens again. MiniCPM-o 4.5 breaks this with **Omni-Flow** — a unified streaming framework where perception and response proceed continuously in parallel across all modalities.

This enables two capabilities impossible in turn-based systems:
1. **Real-time adaptation**: The model can update its response mid-sentence based on new visual/audio input
2. **Proactive behaviors**: The model can initiate actions (reminders, scene descriptions) without explicit user prompts

### Efficiency Breakthrough
Despite being 3× smaller than Qwen3-Omni-30B-A3B, MiniCPM-o 4.5 surpasses it in omni-modal understanding and speech generation quality. Key efficiency drivers:
- **16× visual token compression** (64 tokens vs typical 256+)
- **5× audio temporal compression** (10 tokens/second vs 50)
- **Speech token delegation** to lightweight decoder (~0.3B) rather than backbone generating ~25 tokens/second

## Benchmark Results

### Multi-Discipline Reasoning (MMMU val)
| Model | Score |
|---|---|
| InternVL 2.5-78B (CoT) | **70.1** |
| Qwen2.5-VL-72B | 67.2 |
| InternVL 1.5-26B | 46.8 |
| Idefics2-8B | 43.5 |
| SmolVLM-2.2B | ~35 |

### Document Understanding (DocVQA test)
| Model | Score |
|---|---|
| Qwen2.5-VL-72B | **96.4** |
| InternVL 2.5-78B | 96.0 |
| Qwen2.5-VL-7B | 94.5 |
| InternVL 1.5-26B | 90.9 |
| Idefics2-8B | 74.0 |

### Multilingual Multimodal (Aya Vision vs competitors)
| Model | Size | Key Advantage |
|---|---|---|
| Aya-Vision-8B | 8B | Beats Qwen2.5-VL-7B, Pixtral-12B, Llama-3.2-90B |
| Aya-Vision-32B | 32B | Outperforms Molmo-72B, Llama-3.2-90B-Vision |

### Omni-Modal Streaming (MiniCPM-o 4.5 vs Qwen3-Omni-30B-A3B)
| Capability | MiniCPM-o 4.5 (9B) | Qwen3-Omni-30B-A3B |
|---|---|---|
| Omni-modal understanding | **✅ Better** | Baseline |
| Speech generation quality | **✅ Better** | Baseline |
| Real-time full-duplex | **✅ Yes** | ❌ No |
| Proactive behaviors | **✅ Yes** | ❌ No |
| Edge deployment (<12GB) | **✅ Yes** | ❌ No |
| Voice cloning | **✅ Yes** | Limited |

## Key Design Insights

### 1. Vision Encoder Scale
InternVL showed that larger vision encoders (6B) benefit larger LLMs, but SmolVLM showed smaller encoders (93M) work best with compact LLMs. **Match encoder scale to LLM scale.**

### 2. Image Tokenization is Critical
- **Too many tokens** (LLaVA-style full tokens): Expensive, slow inference
- **Too few tokens** (aggressive compression): Lose spatial detail
- **Sweet spot**: SmolVLM's pixel shuffle (4× reduction, no quality loss) or InternVL's dynamic tiling or MiniCPM-o's 16× compression with resampler

### 3. Native vs. Adapted Resolution
- **Adapted** (InternVL, Idefics2): Tile images into fixed patches → flexible but introduces boundary artifacts
- **Native** (Qwen2.5-VL): Train ViT from scratch on variable resolution → cleaner but requires full retraining

### 4. Data Quality > Quantity
Idefics2's ablation: OCR/document data is critical for practical performance. InternVL 2.5's data filtering pipeline shows that removing even small amounts of noisy data improves results.

### 5. Multilingual Multimodality
Aya Vision demonstrates that multilingual multimodal data scarcity can be addressed through **synthetic annotation frameworks** combined with **cross-modal model merging** to prevent catastrophic forgetting of text-only capabilities.

### 6. Full-Duplex is the Next Frontier
MiniCPM-o 4.5 shows that the interaction paradigm matters as much as model scale. Real-time full-duplex streaming with proactive behaviors represents a qualitative leap beyond turn-based multimodal systems, even with smaller parameter counts.

### 7. Efficiency vs. Capability Trade-off
```
SmolVLM-256M (<1GB) — Edge/mobile, basic VQA
SmolVLM-2.2B (~2GB) — On-device, competitive quality
Idefics2-8B (~16GB) — Balanced, strong general VLM
InternVL 2.5-8B (~8GB) — Strong reasoning + document
Qwen2.5-VL-7B (~8GB) — Best mid-size, video + agent
Aya-Vision-8B (~8GB) — Best multilingual multimodal
MiniCPM-o 4.5-9B (~12GB) — Best omni-modal streaming, edge-ready
InternVL 2.5-78B (~40GB) — MMMU SOTA
Qwen2.5-VL-72B (~40GB) — Best document/agent
Aya-Vision-32B (~32GB) — Scaled multilingual performance
```

## Visual Reasoning with GRIT

[[sources/grit|GRIT (2025)]] pioneers a new paradigm where MLLMs generate **grounded reasoning chains** interleaving natural language with bounding box coordinates. Trained with only 20 image-question-answer triplets via GRPO-GR, it unifies grounding and reasoning capabilities that were previously disconnected in base MLLMs.

## Audio-Visual Intelligence (2026)

[[sources/audio-visual-intelligence|Audio-Visual Intelligence (2026)]] surveys the emerging field of **audio-visual foundation models** that jointly model auditory and visual modalities:
- Unified taxonomies covering understanding, generation, and interaction
- Modality tokenization, cross-modal fusion, and generation paradigms
- Tasks: speech recognition, sound localization, audio-driven video synthesis, video-to-audio, dialogue, embodied interfaces
- Safety, controllability, and synchronization considerations

This represents a next frontier beyond text+vision multimodality toward **tri-modal** (text+audio+vision) systems.

## Video Generation from Images: SwiftI2V

[[sources/swifti2v-highres|SwiftI2V (2026)]] demonstrates high-resolution (2K) image-to-video generation using diffusion transformer backbones:
- **Segment-wise generation** for parallel processing (avoids end-to-end expense at 2K)
- **Bidirectional contextual interaction** maintains global coherence across segments
- Input-faithful synthesis preserving fine-grained appearance details

## Video Background Replacement: Sparkle

[[sources/sparkle-video-bg-replacement|Sparkle (2026)]] applies vision-language understanding to **instruction-guided video background replacement**:
- **Decoupled guidance**: Separate foreground preservation and background synthesis controls
- Temporal consistency across frames while synthesizing entirely new scenes

## Evolution

```
Flamingo (2022): Cross-attention, frozen LLM, 80B
  → LLaVA (2023): MLP projection, full fine-tuning, simple
    → Idefics2 (2024): Rigorous ablation, learned pooling
      → SmolVLM (2025): Ultra-compact, <1GB deployment
    → InternVL 1.5 (2024): 6B vision encoder, dynamic tiles
      → InternVL 2.5 (2024): MMMU >70%, test-time scaling
    → Qwen2-VL (2024): M-RoPE, dynamic resolution
      → Qwen2.5-VL (2025): Native ViT, hours-long video, agent
      → Qwen3-Omni (2025): Turn-based omni-modal (text+vision+audio+speech)
  → Aya Vision (2025): Multilingual-first, synthetic data, model merging
  → VITA-1.5 (2025): Turn-based omni-modal, GPT-4o-level real-time
  → Nemotron 3 Nano Omni (2026): Turn-based omni-modal, 3× throughput
  → MiniCPM-o 4.5 (2026): Full-duplex streaming omni-modal, proactive, edge-ready
  → GRIT (2025): Grounded reasoning with images, 20 samples → SOTA visual reasoning
  → Audio-Visual Intelligence (2026): Tri-modal foundation models
  → SwiftI2V (2026): High-resolution image-to-video generation
  → Sparkle (2026): Instruction-guided video background replacement
```

## See Also
- [[concepts/vision-language-models|Vision-Language Models]] — design patterns and architecture
- [[concepts/multimodal-models|Multimodal Models]]
- [[concepts/multilingual-models|Multilingual Models]] — Aya Vision's multilingual approach
- [[concepts/video-generation|Video Generation]] — generation techniques for vision models
- [[comparisons/open-model-families|Open Model Families]] — text-only model comparison