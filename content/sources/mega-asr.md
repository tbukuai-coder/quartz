---
type: source
arxiv_id: "2605.19833"
title: "Mega-ASR: Towards In-the-wild² Speech Recognition via Scaling up Real-world Acoustic Simulation"
authors: ["Zhifei Xie", "Kaiyu Pang", "Haobin Zhang", "Deheng Ye", "Xiaobin Hu", "Shuicheng Yan", "Chunyan Miao"]
date: 2026-05-21
org: "Multi-institution"
tags: [speech, asr, robustness, rl, audio, 2026]
upvotes: 131
---

# Mega-ASR: Towards In-the-wild² Speech Recognition via Scaling up Real-world Acoustic Simulation

> Unified ASR-in-the-wild framework combining scalable compound-data construction with progressive acoustic-to-semantic optimization (A2S-PSFT + Dual-Granularity WER-Gated Policy Optimization), achieving dramatic WER reductions on severe real-world acoustic conditions.

## Key Contributions
- **Compound-data construction**: scalable pipeline synthesizing realistic acoustic distortions (noise, reverberation, channel effects) in compositional combinations
- **Acoustic-to-Semantic Progressive SFT (A2S-PSFT)**: staged training that first grounds acoustic features, then builds semantic understanding
- **Dual-Granularity WER-Gated Policy Optimization**: RL-based optimization with WER-based gating at both utterance and token granularity
- **841 GitHub stars** — strong practical adoption
- Addresses the "acoustic robustness bottleneck" where models hallucinate/omit under severe distortion

## Method
Mega-ASR identifies the acoustic robustness bottleneck: models lose acoustic grounding under severe compositional distortions, producing hallucinations and omissions. The solution combines: (1) Voices-in-the-Wild compound-data construction synthesizing diverse real-world acoustic scenarios; (2) A2S-PSFT that progressively builds from acoustic perception to semantic understanding; (3) Dual-granularity WER-gated policy optimization that uses reinforcement learning with word error rate as reward, gated at both utterance level (overall quality) and token level (specific corrections).

## Results
- Dramatic WER reductions on VOiCES R4-B-F and NOIZEUS benchmarks
- Maintains clean-speech performance while significantly improving noisy/distorted conditions
- Scales to severe compositional distortions that defeat standard ASR models

## Connections
- Builds on: [[sources/whisper]], [[sources/audio-visual-intelligence]], [[concepts/rlhf]]
- Related: [[concepts/multimodal-models]], [[sources/qwen2-audio]]
- Fills gap: robust speech recognition under real-world acoustic conditions

## Citation
> Xie et al., "Mega-ASR: Towards In-the-wild² Speech Recognition via Scaling up Real-world Acoustic Simulation," arXiv:2605.19833, 2026.
