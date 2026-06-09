---
type: concept
tags: [architecture, foundational]
---

# Self-Attention

> The core mechanism of the Transformer — each position in a sequence computes a weighted sum over all other positions, learning which elements are relevant to each other.

## Overview
Self-attention (also called "scaled dot-product attention") allows every token in a sequence to "look at" every other token and decide how much to attend to it. This replaces the sequential processing of RNNs with fully parallel computation.

## How It Works

### Scaled Dot-Product Attention
```
Attention(Q, K, V) = softmax(QK^T / √d_k) · V
```

Where:
- **Q (Query)**: "What am I looking for?"
- **K (Key)**: "What do I contain?"
- **V (Value)**: "What information do I provide?"
- **√d_k**: Scaling factor to prevent extreme softmax values

### Multi-Head Attention
Run attention `h` times in parallel with different learned projections:
```
MultiHead(Q, K, V) = Concat(head_1, ..., head_h) · W_O
where head_i = Attention(QW_i^Q, KW_i^K, VW_i^V)
```

Each head can learn different attention patterns (e.g., one head focuses on syntax, another on semantics).

### Variants
| Variant | Description | Papers |
|---|---|---|
| **Multi-Head Attention (MHA)** | Original — separate Q, K, V per head | [[sources/attention-is-all-you-need]] |
| **Multi-Query Attention (MQA)** | Shared K, V across heads; faster inference | Shazeer 2019 |
| **Grouped-Query Attention (GQA)** | K, V shared within groups of heads | [[concepts/gqa]] |
| **Sliding Window Attention** | Attention limited to a window | [[concepts/swa]] |
| **FlashAttention** | IO-optimized computation | [[concepts/flash-attention]] |
| **Multi-head Latent Attention (MLA)** | Compressed KV cache via latent space | DeepSeek-V2 |

## Key Papers
- [[sources/attention-is-all-you-need]] — Introduced self-attention for sequences
- [[sources/flash-attention]] — Made attention practical for long sequences

## See Also
- [[concepts/transformer-architecture]]
- [[concepts/gqa]]
- [[concepts/swa]]
- [[concepts/flash-attention]]
