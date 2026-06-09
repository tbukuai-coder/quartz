---
type: source
arxiv_id: "2503.20215"
title: "Qwen2.5-Omni Technical Report"
authors: ["Qwen Team", "Jin Xu", "Yunfei Chu"]
date: 2025-03-26
org: "Alibaba / Qwen"
tags: [multimodal, audio, vision, speech-generation, 2025]
upvotes: 172
---

# Qwen2.5-Omni

> End-to-end multimodal model that perceives text, images, audio, and video while generating both text and natural speech responses in a streaming manner.

## Key Contributions
- First **end-to-end omni-modal model** in the Qwen family — handles text, images, audio, and video input; generates text and speech output
- Introduced **TMRoPE (Time-aligned Multimodal RoPE)** — a novel positional embedding that synchronizes audio and video timestamps in interleaved sequences
- Proposed **Thinker-Talker architecture**: Thinker (LLM) generates text, Talker (dual-track autoregressive model) generates speech from Thinker's hidden representations — avoiding modality interference
- Introduced **sliding-window DiT** for streaming speech token decoding with low initial latency
- Achieves SOTA on **Omni-Bench** (multimodal benchmark) and speech instruction following **comparable to text input** on MMLU/GSM8K

## Method
**Architecture**: Block-wise processing for audio and visual encoders enables streaming input. Audio and video are interleaved sequentially and encoded with TMRoPE for temporal alignment.

**Thinker-Talker**: The Thinker is a standard LLM that generates text. The Talker reads the Thinker's hidden states and produces audio tokens via a dual-track autoregressive model. Both are trained end-to-end. This avoids the common issue where text and speech generation interfere with each other.

**Streaming speech**: A sliding-window DiT (Diffusion Transformer) decodes audio tokens with a restricted receptive field, reducing the initial package delay for real-time streaming.

## Results
- **Omni-Bench**: SOTA among similarly-sized models
- **MMLU (speech input)**: Comparable to text-input performance — speech doesn't degrade reasoning
- **GSM8K (speech input)**: Similarly maintains performance vs text
- **Speech generation**: Outperforms most streaming and non-streaming alternatives in robustness and naturalness
- **Vision tasks**: Comparable to Qwen2.5-VL at matched model size
- **Audio understanding**: Outperforms Qwen2-Audio across benchmarks

## Models Released
- Qwen2.5-Omni-7B (open weights)

## Connections
- **Builds on**: [[sources/qwen25|Qwen2.5]], [[sources/qwen2-audio|Qwen2-Audio]], [[sources/qwen25-vl|Qwen2.5-VL]]
- **Part of**: [[entities/models/qwen|Qwen]] family, [[entities/orgs/alibaba|Alibaba/Qwen]]
- **Related concepts**: [[concepts/multimodal-models|Multimodal Models]], [[concepts/positional-encodings|Positional Encodings]] (TMRoPE), [[concepts/diffusion-models|Diffusion Models]] (sliding-window DiT)
- **Novel**: First open model to achieve text-parity on reasoning benchmarks when using speech input
- **Successor to**: [[sources/qwen2-audio|Qwen2-Audio]] + [[sources/qwen25-vl|Qwen2.5-VL]] (unified)

## Citation
> Qwen Team, "Qwen2.5-Omni Technical Report," arXiv:2503.20215, 2025.
