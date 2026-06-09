---
type: concept
tags: [long-context, positional-encoding, rope, architecture]
---

# Long Context

> Extending LLMs beyond their training context window (4K→128K→1M→**2M+ tokens**) — enabled by RoPE scaling methods (YaRN, LongRoPE), efficient attention, and architectural innovations (Mamba).

## Overview
LLMs are trained on fixed context lengths but real-world applications demand longer contexts: full documents, long conversations, repository-level code, hour-long videos. Extending context is challenging because: (1) attention is quadratic in sequence length, (2) positional encodings don't generalize beyond training length, and (3) the KV cache grows linearly with context.

## Approaches

### Positional Encoding Extension
| Method | How | Cost | Extension | Used By |
|---|---|---|---|---|
| **Position Interpolation** | Linearly scale RoPE to fit longer context | High (full retraining) | ~4× | Early work |
| **NTK-Aware scaling** | Different scaling for high/low frequency dims | Moderate | ~8× | Foundation for YaRN |
| **[[sources/yarn|YaRN]]** | NTK-aware + dynamic + temperature scaling | **10× fewer tokens** | ~64× | Qwen, DeepSeek, Mistral |
| **[[sources/longrope|LongRoPE]]** | Non-uniform per-dimension rescaling via evolutionary search | **1K steps** | **512×** (to 2M) | Microsoft |
| **Dynamic NTK** | Scale factor adapts to sequence length at inference | **Zero training** | ~4× | Most inference engines |

### Efficient Attention
| Method | Complexity | How |
|---|---|---|
| Standard attention | O(n²) | Full pairwise computation |
| [[concepts/flash-attention|FlashAttention]] | O(n²) but fast | IO-aware SRAM tiling |
| Ring Attention | O(n²) distributed | Distribute across devices |
| Sparse attention | O(n·k) | Attend to subset of tokens |

### Alternative Architectures
| Method | Complexity | How |
|---|---|---|
| **[[sources/mamba|Mamba/SSM]]** | **O(n)** | Selective state spaces — linear scaling |
| RWKV | O(n) | Linear attention RNN |
| Hyena | O(n log n) | Gated long convolutions |
| Jamba | O(n) + O(n²) | Hybrid Mamba + Attention layers |

### Activation-Aware Memory: MiA-Signature

[[sources/mia-signature|MiA-Signature (2026)]] proposes a fundamentally different approach to long-context memory — rather than fitting more tokens into context, it **approximates global activation patterns**:

#### Cognitive Science Inspiration
Human cognition relies on "global ignition" — transient, large-scale activation over distributed memory systems. But we cannot directly access or enumerate all activated contents. Instead, we use a **compact internal representation** that approximates global influence on downstream processing.

#### The Mindscape Framework
1. **Mindscape**: Organized memory substrate $\mathcal{M}(D) = \{m_1, \ldots, m_N\}$ with redundancy and multiple abstraction levels
2. **Activation**: Query induces broad activation pattern $a_q: \mathcal{M}(D) \to \mathbb{R}_{\geq 0}$ over the mindscape
3. **MiA-Signature**: Compact subset of high-level memory units selected via submodular optimization:
   $$\sigma^*(q) = \arg\max_{\sigma \subseteq \mathcal{H}_q, |\sigma| \leq K} \mathcal{F}(\sigma; q, \mathcal{H}_q)$$
   where $\mathcal{F}$ scores relevance, coverage, and diversity.

#### Two Retrieval Interface
- **$\mathcal{E}_1$** (query-only): Initial broad retrieval for activation view (top-50)
- **$\mathcal{E}_2$** (mindscape-aware): Conditioned on $(q_t, \sigma_t)$ pair — query carries immediate intent, signature supplies global memory signal

#### Static vs Dynamic Settings
- **RAG**: Signature constructed once as fixed conditioning signal
- **Agent**: Signature evolves as $\sigma_t$ updated alongside local evidence at each step

#### Results
Consistent performance gains across long-context understanding tasks in both RAG and agentic settings. The key insight: approximating global activation provides more effective memory interface than relying solely on local retrieval, especially for multi-hop reasoning.

## Current State of the Art
- **LongRoPE** (2024): 2,048K tokens — first to break the 1M barrier with only 1K fine-tuning steps
- **Qwen2.5-1M**: 1M token context via YaRN-based extension
- **Gemini**: 1M+ token context (proprietary)
- **Kimi k1.5**: Long context for RL-based reasoning
- **MiA-Signature** (2026): Cognitive-science-inspired activation approximation for memory interfaces

## Key Papers
- [[sources/longrope|LongRoPE]] (2024) — extends to 2M tokens via non-uniform positional interpolation
- [[sources/yarn|YaRN]] (2023) — standard RoPE extension method
- [[sources/mamba|Mamba]] (2023) — linear-time alternative to attention
- [[sources/flash-attention|FlashAttention]] (2022) — efficient attention implementation
- [[sources/kimi-k15|Kimi k1.5]] (2025) — long context for reasoning RL
- [[sources/mia-signature|MiA-Signature]] (2026) — global activation approximation for memory systems

## See Also
- [[concepts/self-attention|Self-Attention]]
- [[concepts/positional-encodings|Positional Encodings]]
- [[concepts/kv-cache|KV Cache]]
- [[concepts/flash-attention|FlashAttention]]
- [[concepts/transformer-architecture|Transformer Architecture]]