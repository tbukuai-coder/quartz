---
type: source
arxiv_id: "2501.01957"
title: "VITA-1.5: Towards GPT-4o Level Real-Time Vision and Speech Interaction"
authors: ["Chaoyou Fu", "Haojia Lin", "Xiong Wang", "Yi-Fan Zhang", "Various"]
date: 2025-01-03
org: "Nanjing University / Various"
tags: [multimodal, vision, speech, omni-model, real-time, 2025]
upvotes: 47
---

# VITA-1.5: Real-Time Vision + Speech Interaction

> A multimodal LLM that integrates **vision, language, and speech** into a single model via a three-stage training methodology — achieving **GPT-4o-level** real-time interaction without separate ASR/TTS modules, significantly accelerating end-to-end multimodal response speed. 2,507 GitHub ⭐.

## Key Contributions
- **Unified omni-model**: Integrates vision, language, and speech understanding + generation in a single model — no separate ASR/TTS pipeline needed
- **Three-stage training**: Progressive methodology that incrementally adds modalities while **relieving modality conflicts** that typically degrade performance
- **Real-time speech-to-speech**: End-to-end speech dialogue without transcription bottleneck — faster response times than pipeline approaches
- **Preserved vision-language quality**: Despite adding speech, maintains strong vision-language performance comparable to leading open-source MLLMs
- **Practical omni interaction**: Enables multimodal dialogue where users can show images/videos while speaking naturally

## Method
### Three-Stage Training
- **Stage 1 — Vision-Language Training**: Alignment (Stage 1.1, 20M image-text pairs) + visual instruction tuning (Stage 1.2) to establish strong vision-language foundation
- **Stage 2 — Speech Integration**: Add audio encoder + adapter; train on speech understanding tasks while freezing vision components to prevent modality conflict
- **Stage 3 — Omni Fusion**: Jointly fine-tune all modalities; end-to-end speech generation module replaces external TTS

### Architecture
- **Input**: Vision Transformer (image/video encoder) + Audio Transformer (speech encoder) + Multi-Layer Connector adapters
- **Core**: Large language model backbone
- **Output**: End-to-end speech generation module (not external TTS)

Key insight: Naively training all modalities together causes "modality conflict" — speech and vision compete for model capacity. The progressive three-stage approach isolates learning of each modality before fusion.

## Results
### Image Understanding (comparable to leading open-source MLLMs)
- Competitive with InternLM-XComposer2.5, Cambrian-1, MiniCPM-V-2.6 on MMBench, MMStar, HallusionBench, MathVista, OCRBench
- Strong performance across both Chinese and English benchmarks

### Video Understanding
- Competitive on video QA benchmarks, supporting multi-frame temporal reasoning

### Speech
- Mandarin ASR: Competitive with Wav2vec2 and specialized speech models
- Speech-to-speech dialogue: End-to-end without separate ASR/TTS pipeline
- Significantly faster response times than pipeline approaches (Mini-Omni2, Freeze-Omni)

## Connections
- **Builds on**: [[sources/llava|LLaVA]] (visual instruction tuning), [[sources/cambrian|Cambrian-1]] (vision encoders)
- **Related omni-models**: [[sources/qwen25-omni|Qwen2.5-Omni]] (also omni-model with speech)
- **Concepts**: [[concepts/multimodal-models|Multimodal Models]], [[concepts/vision-language-models|VLMs]]
- **Comparison**: [[comparisons/vision-language-models|VLM Comparison]]
- **GitHub**: https://github.com/VITA-MLLM/VITA

## Citation
> Fu et al., "VITA-1.5: Towards GPT-4o Level Real-Time Vision and Speech Interaction," arXiv:2501.01957, 2025.
