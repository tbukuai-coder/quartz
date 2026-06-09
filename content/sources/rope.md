---
type: source
arxiv_id: "2104.09864"
title: "RoFormer: Enhanced Transformer with Rotary Position Embedding"
authors: ["Jianlin Su", "Yu Lu", "Shengfeng Pan", "Ahmed Murtadha", "Bo Wen", "Yunfeng Liu"]
date: 2021-04-20
org: "Zhuiyi Technology"
tags: [architecture, positional-encoding, foundational]
upvotes: 17
---

# RoFormer / Rotary Position Embedding (RoPE)

> Introduced **Rotary Position Embedding (RoPE)** — encoding absolute position via rotation matrices while naturally incorporating relative position dependency in self-attention. RoPE became the **de facto standard** positional encoding for virtually all modern LLMs (LLaMA, Mistral, Qwen, DeepSeek, Gemma, Falcon, OLMo).

## Key Contributions
- **Rotary Position Embedding (RoPE)**: Encodes absolute position by rotating query and key vectors, while the dot product between them naturally depends on relative position
- **Elegant mathematical formulation**: Position m is encoded as a block-diagonal rotation matrix R(m) applied to queries/keys; attention score between positions m and n depends only on (m-n)
- **Long-term decay**: Inner product between rotated vectors naturally decreases with increasing relative distance — a desirable inductive bias
- **Sequence length flexibility**: No fixed maximum length during training; extends naturally to longer sequences
- **Compatible with linear attention**: Can equip linear self-attention with relative position encoding

## Method
For a 2D case, RoPE applies a rotation of angle mθ to the query at position m:

```
f_q(x_m, m) = R(mθ) · W_q · x_m
f_k(x_n, n) = R(nθ) · W_k · x_n
```

The attention score q_m^T · k_n = (W_q·x_m)^T · R((n-m)θ) · (W_k·x_n), depending only on relative position (n-m).

For d-dimensional embeddings, RoPE uses d/2 rotation pairs with frequencies θ_i = 10000^(-2i/d), creating a multi-frequency encoding that captures both local and long-range dependencies.

### Key Properties
1. **Relative position dependency**: Attention scores depend on relative distance, not absolute position
2. **Decaying with distance**: Naturally decreasing attention with increasing relative distance
3. **Sequence length generalization**: No learned position embeddings means no fixed context length
4. **Computational efficiency**: Implemented as element-wise rotation, negligible overhead

## Impact on the Ecosystem
RoPE's adoption is nearly universal in modern LLMs:
- **[[sources/llama|LLaMA]]** (2023): Adopted RoPE, establishing the "LLaMA template" (RoPE + RMSNorm + SwiGLU + GQA)
- **[[sources/mistral-7b|Mistral]]**, **[[sources/qwen25|Qwen]]**, **[[sources/gemma|Gemma]]**, **[[sources/olmo|OLMo]]**: All use RoPE
- **[[sources/deepseek-v3|DeepSeek-V3]]**: Uses RoPE within MLA (Multi-head Latent Attention)
- **[[sources/yarn|YaRN]]**: Extends RoPE for longer contexts via temperature scaling
- **[[sources/longrope|LongRoPE]]**: Progressive extension to 2M+ tokens
- **[[sources/nomic-embed|Nomic Embed]]**: Uses RoPE for 8K-context embeddings (vs. 512-token BERT limit)

RoPE supplanted both sinusoidal (Transformer), learned absolute (GPT-2), and ALiBi ([[entities/models/bloom|BLOOM]]) position encodings.

## Connections
- Extended by: [[sources/yarn|YaRN]], [[sources/longrope|LongRoPE]]
- Adopted by: [[sources/llama]], [[sources/mistral-7b]], [[sources/qwen25]], [[sources/gemma]], [[sources/olmo]], [[sources/deepseek-v3]]
- Related concepts: [[concepts/positional-encodings]], [[concepts/transformer-architecture]], [[concepts/long-context]]

## Citation
> Su et al., "RoFormer: Enhanced Transformer with Rotary Position Embedding," arXiv:2104.09864, 2021.
