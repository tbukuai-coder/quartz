---
type: source
arxiv_id: "2212.04356"
title: "Robust Speech Recognition via Large-Scale Weak Supervision"
authors: ["Alec Radford", "Jong Wook Kim", "Tao Xu", "Greg Brockman", "Christine McLeavey", "Ilya Sutskever"]
date: 2022-12-06
org: "OpenAI"
tags: [speech, multimodal, foundational]
upvotes: 53
---

# Whisper: Robust Speech Recognition via Large-Scale Weak Supervision

> A speech recognition model trained on **680,000 hours** of multilingual audio from the internet — achieving near-human accuracy and remarkable robustness in **zero-shot transfer** without fine-tuning.

## Key Contributions
- Trained on **680K hours** of weakly-supervised multilingual audio data (largest at the time)
- Achieves **near-human accuracy** and robustness on standard benchmarks in zero-shot setting
- Supports **multilingual transcription** (99 languages) and **translation** to English
- Released as a fully open model — catalyzed the open speech recognition ecosystem
- Multitask model: transcription, translation, language identification, voice activity detection

## Method
### Architecture
- **Encoder-decoder Transformer**
- Audio → Log-Mel spectrogram → Encoder → Cross-attention → Decoder → Text
- Trained end-to-end with standard sequence-to-sequence objectives

### Training
- **680,000 hours** of audio paired with transcripts scraped from the internet
- Weakly-supervised: transcripts are noisy/imperfect but massive in scale
- Multitask training: same model handles transcription, translation, and language ID
- Task and language specified via special tokens in the decoder

### Key Insight
Scale and diversity of training data beats careful curation. The model generalizes well to new domains, accents, and languages without any fine-tuning — purely through scale.

## Models Released
| Model | Params | Speed | Accuracy |
|---|---|---|---|
| Whisper Tiny | 39M | Fastest | Lowest |
| Whisper Base | 74M | Fast | Good |
| Whisper Small | 244M | Medium | Better |
| Whisper Medium | 769M | Slow | High |
| Whisper Large-v3 | 1.5B | Slowest | Near-human |

## Connections
- **Key concepts**: [[concepts/pre-training]], [[concepts/transformer-architecture]]
- **Related**: [[sources/llava]] (multimodal paradigm), [[sources/llama-3]] (speech adapter)
- **Organizations**: [[entities/orgs/openai]]
- **HF Hub**: One of the most downloaded models on the Hub

## Citation
> Radford et al., "Robust Speech Recognition via Large-Scale Weak Supervision," arXiv:2212.04356, 2022.
> https://huggingface.co/papers/2212.04356
