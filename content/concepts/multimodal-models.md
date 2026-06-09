---
type: concept
tags: [multimodal, vision-language]
---

# Multimodal Models

> Models that process and generate across **multiple modalities** (text, images, audio, video) — the convergence point of language models, vision models, and speech models.

## Overview
Multimodal models extend LLMs to understand and generate content beyond text. The field has evolved from separate models per modality to unified architectures that process all modalities natively.

## Approaches

### Compositional (Adapter-based)
- Separate encoders for each modality, connected to LLM via adapters
- **Pros**: Reuse pre-trained components; modular
- **Cons**: Modalities aren't deeply integrated
- Examples: [[sources/llava|LLaVA]], [[sources/llama-3|Llama 3.2 Vision]], [[sources/whisper|Whisper]] + LLM

### Early Fusion (Native Multimodal)
- All modalities tokenized and processed jointly from pre-training
- **Pros**: Deep cross-modal understanding
- **Cons**: Expensive to train; complex data pipeline
- Examples: [[sources/llama-4|Llama 4]], Gemini, [[sources/gemma-3|Gemma 3]]

### Full-Duplex Omni-Modal (2026)
- **Pros**: Simultaneous perception and response across all modalities in real-time
- **Cons**: Complex temporal alignment; streaming infrastructure
- Example: [[sources/minicpm-o-4-5|MiniCPM-o 4.5]]

### The LLaVA Paradigm
The dominant pattern for open multimodal models:
```
Image → Vision Encoder (CLIP/SigLIP) → Projection → LLM → Text Response
```
This simple architecture, introduced by [[sources/llava|LLaVA]], is used by most open multimodal models.

## Evolution
| Year | Development | Examples |
|---|---|---|
| 2021 | CLIP — contrastive image-text learning | OpenAI CLIP |
| 2022 | Stable Diffusion — text-to-image generation | [[sources/latent-diffusion]] |
| 2022 | Whisper — speech recognition | [[sources/whisper]] |
| 2023 | LLaVA — visual instruction tuning | [[sources/llava]] |
| 2024 | Native multimodal LLMs | [[sources/llama-3]], [[sources/gemma-3]] |
| 2025 | Early-fusion multimodal | [[sources/llama-4]], Qwen2.5-Omni |
| 2026 | Full-duplex omni-modal streaming | [[sources/minicpm-o-4-5|MiniCPM-o 4.5]] |

## Full-Duplex Omni-Modal Interaction: MiniCPM-o 4.5

[[sources/minicpm-o-4-5|MiniCPM-o 4.5 (2026)]] represents a paradigm shift from turn-based multimodal interaction to **continuous full-duplex streaming**:

### The Problem with Turn-Based Interaction
Current models (VITA-1.5, Qwen2.5-Omni, Nemotron 3 Nano Omni) process one modality at a time in alternating phases:
```
Listen → Think → Speak → Listen → Think → Speak...
```
This prevents the model from incorporating new inputs during generation and limits proactive behaviors.

### Omni-Flow Framework
Formulates interaction as continuous full-duplex process:
- **Perception and response proceed in parallel** across all modalities
- **Millisecond-level temporal axis** aligns inputs and outputs
- **Proactive behaviors** emerge from ongoing context (reminders, scene descriptions, comments)
- Model can update its response in real-time based on incoming streams

### Architecture (9B parameters, <12GB RAM)
Three main components with **token-level differentiable connections**:

1. **Visual Encoding**: LLaVA-UHD partitioning → SigLIP ViT (0.4B) → Resampler (16× compression to 64 tokens)
2. **Audio Encoding**: Whisper Medium (0.3B) → 5× temporal compression → 10 audio tokens/second
3. **LLM + Speech Decoders**: Qwen3-8B backbone generates text + hidden states → lightweight Llama speech token decoder (~0.3B) → flow-matching waveform decoder

**Key design insight**: LLM generates text at 3-4 tokens/second (human speech speed); speech token generation delegated to lightweight decoder — avoids backbone bottleneck of generating ~25 speech tokens/second directly.

### Results
- Approaches **Gemini 2.5 Flash** in vision-language capabilities
- **SOTA open-source at 9B scale**
- Surpasses **Qwen3-Omni-30B-A3B** in omni-modal understanding and speech quality
- Supports voice cloning via multimodal system prompts with reference audio
- Runs on edge devices with <12GB RAM

## Key Papers
- [[sources/llava]] — LLaVA (visual instruction tuning)
- [[sources/latent-diffusion]] — Stable Diffusion (image generation)
- [[sources/whisper]] — Whisper (speech recognition)
- [[sources/gemma-3]] — Gemma 3 (multimodal open model)
- [[sources/llama-3]] — Llama 3 (multimodal adapters)
- [[sources/minicpm-o-4-5]] — MiniCPM-o 4.5 (full-duplex omni-modal streaming)

## See Also
- [[concepts/instruction-tuning]]
- [[concepts/transformer-architecture]]