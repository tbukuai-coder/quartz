---
type: source
arxiv_id: "2407.10759"
title: "Qwen2-Audio Technical Report"
authors: ["Yunfei Chu", "Jin Xu", "Qian Yang"]
date: 2024-07-15
org: "Alibaba / Qwen"
tags: [multimodal, audio, speech, alignment, 2024]
upvotes: 64
---

# Qwen2-Audio

> A large-scale audio-language model that achieves SOTA on diverse audio understanding tasks using natural language prompts and DPO-optimized instruction following.

## Key Contributions
- Developed **Qwen2-Audio**, a large-scale audio-language model that processes diverse audio inputs (speech, music, environmental sounds) alongside text
- Introduced **voice chat** and **audio analysis** modes — users interact via spoken or text prompts
- Achieved **SOTA on multiple audio benchmarks** including speech recognition, audio captioning, sound event detection, and music understanding
- Applied **DPO optimization** to improve instruction-following capabilities for audio understanding
- Released as open-source, part of the broader [[entities/models/qwen|Qwen]] ecosystem

## Method
Qwen2-Audio uses an **audio encoder** (based on Whisper-large-v3 architecture) connected to a **Qwen2 language model** via a simple linear projection layer. Two training stages:

1. **Multi-task pre-training**: Trained on a diverse mix of audio tasks — ASR (30+ languages), audio captioning, sound event classification, music understanding, speaker verification. Uses hierarchical tags to prevent interference between different audio tasks.

2. **Instruction fine-tuning + DPO**: Fine-tuned on instruction-following data with natural language prompts. DPO applied to preference data to improve response quality and reduce hallucination.

## Results
- **Aishell-1 (ASR)**: 1.53% CER (competitive with specialized models)
- **LibriSpeech (ASR)**: 2.0% WER without LM
- **AudioCaps (captioning)**: SOTA CIDEr score
- **Multilingual ASR**: Competitive on 30+ languages
- **Environmental sound classification**: Beats prior audio-LMs on ESC-50, AudioSet evaluations
- **Music understanding**: Can identify instruments, genre, mood, and describe compositions

## Datasets Used
- LibriSpeech, Aishell, GigaSpeech (ASR)
- AudioCaps, Clotho (audio captioning)
- AudioSet, ESC-50 (sound classification)
- MusicCaps (music understanding)
- Custom multi-task audio-text dataset

## Models Released
- Qwen2-Audio (7B) — open weights
- Qwen2-Audio-Instruct — instruction-following variant

## Connections
- **Part of**: [[entities/models/qwen|Qwen]] family, [[entities/orgs/alibaba|Alibaba/Qwen]]
- **Builds on**: [[sources/whisper|Whisper]] (audio encoder architecture), [[sources/qwen25|Qwen2.5]] (language backbone)
- **Related**: [[sources/qwen2-vl|Qwen2-VL]] (visual counterpart), [[concepts/multimodal-models|Multimodal Models]]
- **Successor**: Qwen2.5-Omni (unified audio+vision+text)
- **Related concepts**: [[concepts/dpo|DPO]] (preference optimization), [[concepts/instruction-tuning|Instruction Tuning]]

## Citation
> Chu et al., "Qwen2-Audio Technical Report," arXiv:2407.10759, 2024.
