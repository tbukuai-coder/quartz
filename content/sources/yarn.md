---
type: source
arxiv_id: "2309.00071"
title: "YaRN: Efficient Context Window Extension of Large Language Models"
authors: ["Bowen Peng", "Jeffrey Quesnelle", "Honglu Fan", "Enrico Shippole"]
date: 2023-09-01
org: "EleutherAI / NTX Research"
tags: [long-context, rope, positional-encoding, efficiency, 2023]
upvotes: 83
---

# YaRN — Yet another RoPE extensioN

> A compute-efficient method to extend LLM context windows, requiring 10× fewer tokens and 2.5× fewer training steps than prior methods — used by Qwen, Mistral, DeepSeek, and most long-context models on HF Hub.

## Key Contributions
- **NTK-aware interpolation**: Combines high-frequency extrapolation with low-frequency interpolation of RoPE embeddings — preserves local positional information while extending global reach
- **Dynamic NTK scaling**: Adjusts the scaling factor based on sequence length at inference time — no retraining needed for moderate extensions
- **Attention temperature scaling**: Fixes the entropy increase that occurs with longer sequences by scaling attention logits
- **10× fewer tokens, 2.5× fewer steps** than Position Interpolation (PI) to achieve the same context extension

## Method
1. **Background**: [[concepts/self-attention|RoPE (Rotary Position Embeddings)]] encode positions by rotating query/key vectors. Models trained on length L fail at length >L because high-frequency rotations "wrap around"
2. **NTK-aware scaling**: Different RoPE frequency dimensions are interpolated differently:
   - Low frequencies (long-range): Interpolated (scaled down to fit extended context)
   - High frequencies (short-range): Left mostly unchanged (preserve local token relationships)
   - Ramp function blends between interpolation and extrapolation based on frequency
3. **Dynamic NTK**: At inference time, scale factor s = (L'/L)^(d/(d-2)) where L' is current sequence length. No training needed — works at any length up to ~4× the training length
4. **Temperature scaling**: Multiply attention logits by t = 0.1·ln(s) + 1 to compensate for entropy increase with longer sequences
5. **Training**: Fine-tune for ~400 steps on long documents — 10× fewer tokens than Position Interpolation

## Results
- LLaMA 2 7B/13B extended from 4K to **128K context** with maintained perplexity
- **10× fewer tokens** needed vs. Position Interpolation at same performance
- **2.5× fewer training steps** to reach equivalent quality
- Dynamic NTK works without any training for up to 4× context extension
- Passkey retrieval accuracy maintained across extended context

## Impact on the Ecosystem
YaRN is the **standard method** for context extension in the HF ecosystem:
- Used by [[sources/qwen25|Qwen2.5]], [[sources/deepseek-v3|DeepSeek-V3]], and many Mistral fine-tunes
- Available in `transformers` via `rope_scaling` config parameter
- Enabled the 128K+ context era of open models

## Connections
- Extends: [[concepts/self-attention|Self-Attention / RoPE]]
- Used by: [[sources/qwen25|Qwen2.5]], [[sources/deepseek-v3|DeepSeek-V3]], [[sources/kimi-k15|Kimi k1.5]]
- Related: Position Interpolation (predecessor), NTK-Aware scaling (basis)
- Concepts: [[concepts/long-context|Long Context]], [[concepts/self-attention|Self-Attention]]

## Citation
> Peng et al., "YaRN: Efficient Context Window Extension of Large Language Models," arXiv:2309.00071, 2023.
