---
type: source
arxiv_id: "2604.27393"
title: "MiniCPM-o 4.5: Towards Real-Time Full-Duplex Omni-Modal Interaction"
authors:
  - Junbo Cui
  - Bokai Xu
  - Chongyi Wang
  - Tianyu Yu
  - Weiyue Sun
  - Yingjing Xu
  - Tianran Wang
  - Zhihui He
  - Wenshuo Ma
  - Tianchi Cai
venue: arXiv
year: 2026
month: 4
date: "2026-04"
upvotes: 41
tags:
  - omni-modal
  - multimodal
  - streaming
  - full-duplex
  - speech-generation
  - edge-devices
github: https://github.com/OpenBMB/MiniCPM-o
stars: 24518
---

# MiniCPM-o 4.5: Towards Real-Time Full-Duplex Omni-Modal Interaction

## One-Line Summary

9B-parameter end-to-end omni-modal model enabling real-time full-duplex interaction (simultaneous seeing, listening, and speaking) via the Omni-Flow streaming framework, running on <12GB RAM edge devices.

## Key Contributions

1. **First full-duplex omni-modal LLM** — Perception and response proceed in parallel rather than alternating phases; model can update its response in real-time based on incoming multimodal streams.
2. **Omni-Flow framework** — Unified streaming architecture aligning multimodal inputs and outputs on a shared millisecond-level temporal axis. Formulates interaction as continuous full-duplex process rather than discrete turns.
3. **Time-aligned interleaving speech generation** — Output speech tightly couples with concurrent environment context through time-aligned text-to-speech token interleaving.
4. **Proactive behaviors** — Model can initiate actions (reminders, scene descriptions, comments) based on continuous understanding of live context, not just reactive responses.
5. **Edge-efficient** — 9B parameters, runs on <12GB RAM. Supports both full-duplex streaming and traditional turn-based modes.

## Architecture

Three main components with **token-level differentiable connections** (end-to-end trainable):

### Visual Encoding
- LLaVA-UHD image partitioning for any-aspect high-resolution images
- SigLIP ViT (0.4B) encodes slices into 1024 tokens
- Resampler compresses to **64 tokens** (16× compression ratio)
- Max resolution: 448×448 (streaming mode) or 2240×2240 (standard mode)

### Audio Encoding
- Whisper Medium encoder (0.3B) in chunk-based streaming
- 50 feature tokens/second → 5× temporal compression via 2-layer MLP projector → **10 audio tokens/second**

### LLM Backbone + Speech Decoders
- **Qwen3-8B backbone** generates text + hidden states for speech
- Lightweight Llama speech token decoder (~0.3B): receives LLM hidden states (via MLP) + text tokens for S3 token generation
- Streaming flow-matching decoder converts S3 tokens to audio waveforms
- **Key design**: LLM generates text at 3-4 tokens/second (human speech speed); speech tokens delegated to lightweight decoder — avoids backbone bottleneck of directly generating ~25 speech tokens/second

## Training

Four sequential stages:
1. **Speech pretraining** — Large-scale speech-text alignment
2. **Joint pretraining** — Multimodal pretraining across vision, speech, text
3. **Joint supervised fine-tuning** — Instruction following across all modalities
4. **Reinforcement learning** — RL fine-tuning for interaction quality

## Results

### Vision-Language (vs. Gemini 2.5 Flash, Qwen3-Omni)
- Approaches **Gemini 2.5 Flash** in vision-language capabilities
- **SOTA open-source performance at 9B scale**
- Strong OCR, low hallucination, multilingual support (inherits MiniCPM family strengths)

### Omni-Modal & Speech
- Surpasses **Qwen3-Omni-30B-A3B** in omni-modal understanding and speech generation quality
- Significantly higher computational efficiency than Qwen3-Omni

### Advanced Capabilities
- **Voice cloning**: Accepts multimodal system prompts with reference audio
- **Real-time streaming**: Continuous perception + response without turn boundaries
- **Proactive interaction**: Initiates behaviors from ongoing context

## Connections

- **Omni-Flow vs Turn-Based**: Breaks the alternating perception-response paradigm shared by [[sources/vita-1-5|VITA-1.5]], [[sources/qwen2-5-omni|Qwen2.5-Omni]], and [[sources/nemotron-3-nano-omni|Nemotron 3 Nano Omni]]. These models process one modality at a time; MiniCPM-o 4.5 processes all simultaneously.
- **Speech Architecture**: Delegates speech token generation to lightweight decoder (similar to [[concepts/speculative-decoding|speculative decoding]] principles), avoiding the capacity degradation seen when LLM backbones directly generate high-rate speech tokens.
- **Edge Efficiency**: 9B parameters on <12GB RAM extends the [[comparisons/small-language-models|small model]] frontier into omni-modal territory, comparable to [[sources/smolvlm|SmolVLM]]'s efficiency ethos but with full-duplex streaming.
- **Token Compression**: 16× visual + 5× audio compression ratios enable efficient streaming without quality loss, comparable to [[sources/mmtok|MMTok]]'s training-free VLM token pruning but achieved via architectural design.
- **Open Source**: 24.5K GitHub stars — one of the most popular open multimodal projects, following OpenBMB's [[sources/minicpm-v|MiniCPM-V]] lineage.

## Citation

```bibtex
@article{cui2026minicpmo45,
  title={MiniCPM-o 4.5: Towards Real-Time Full-Duplex Omni-Modal Interaction},
  author={Cui, Junbo and Xu, Bokai and Wang, Chongyi and Yu, Tianyu and Sun, Weiyue and Xu, Yingjing and Wang, Tianran and He, Zhihui and Ma, Wenshuo and Cai, Tianchi and others},
  journal={arXiv preprint arXiv:2604.27393},
  year={2026}
}
```

---
*Ingested in Batch 26 (2026-05-05)* | [[index]] | [[concepts/multimodal-models]] | [[concepts/agents]] | [[entities/models/minicpm]]