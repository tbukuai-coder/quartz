---
type: concept
tags: [architecture, foundational]
---

# Transformer Architecture

> The foundational neural network architecture for modern AI — based entirely on **attention mechanisms**, enabling parallel processing of sequences and scaling to hundreds of billions of parameters.

## Overview
The Transformer, introduced in [[sources/attention-is-all-you-need|"Attention Is All You Need" (2017)]], replaced recurrent and convolutional architectures with pure attention. It became the backbone of virtually every major language model, vision model, and multimodal model.

## How It Works

### Core Components
1. **[[concepts/tokenization|Tokenization]]**: Raw text is first converted to token IDs via subword tokenization (BPE, WordPiece, Unigram)
2. **Embedding Layer**: Token IDs mapped to dense vectors
3. **Multi-Head Self-Attention**: Each position attends to all other positions; multiple attention "heads" capture different relationship patterns — see [[concepts/self-attention]]
4. **Feed-Forward Networks (FFN)**: Two linear layers with a nonlinear activation, applied position-wise
5. **Residual Connections**: Skip connections around each sub-layer for gradient flow
6. **Layer Normalization**: Stabilizes training (originally post-norm; modern models use pre-norm / RMSNorm)
7. **Positional Encoding**: Injects sequence order information (sinusoidal → learned → RoPE)

### Architecture Variants
| Variant | Structure | Use Case | Examples |
|---|---|---|---|
| **Encoder-only** | Bidirectional attention | Classification, NER, embeddings | [[entities/models/bert-model|BERT]] |
| **Decoder-only** | Causal (left-to-right) attention | Text generation, LLMs | [[entities/models/llama|LLaMA]], GPT |
| **Encoder-Decoder** | Cross-attention between enc/dec | Translation, summarization | T5, BART |

Modern LLMs almost exclusively use **decoder-only** architectures.

### Modern Enhancements
- **RMSNorm**: Simpler, faster normalization (used by LLaMA, Mistral, Qwen)
- **SwiGLU / GeGLU**: Gated activation functions replacing ReLU
- **Rotary Positional Embeddings (RoPE)**: Better position encoding, supports length extrapolation
- **Grouped-Query Attention (GQA)**: Reduces KV cache — [[concepts/gqa]]
- **Sliding Window Attention (SWA)**: Bounded attention window — [[concepts/swa]]
- **FlashAttention**: IO-aware attention computation — [[concepts/flash-attention]]
- **Mixture of Experts**: Sparse expert routing — [[concepts/mixture-of-experts]]

## Implicit Reasoning in Depth-Bounded Transformers

[[sources/scaling-implicit-deductive-reasoning|Implicit Deductive Reasoning (2026)]] investigates whether deep Transformers with **bidirectional prefix masking** can perform implicit deductive reasoning comparable to explicit chain-of-thought:

- In sufficiently deep models, implicit reasoning approaches explicit CoT performance across diverse graph topologies and problem sizes
- **Algorithmic alignment** (matching model inductive biases to reasoning structure) is critical — without it, models exploit spurious features
- However, **explicit CoT remains necessary for depth extrapolation** (reasoning beyond training depth)
- This has implications for diffusion language models and other non-autoregressive architectures where CoT is not naturally available
- Horn clause reasoning serves as the controlled testbed, with systematic decorrelation of provability from spurious features

## TIDE: Token Identity at Every Layer

[[sources/tide-token-index|TIDE (2026)]] challenges the universal Transformer design assumption that token identity is looked up once at the input embedding layer and permanently discarded:

- The **Rare Token Problem**: Zipf-type vocabulary distribution causes rare-token embeddings to be chronically under-trained due to receiving a fraction of cumulative gradient signal
- **Contextual Collapse**: The model loses token identity information as depth increases, degrading performance on token-sensitive tasks

TIDE introduces **EmbeddingMemory** with:
- **Context-free semantic vectors**: Compute semantic similarity between hidden states and token embeddings without attending to context
- **Depth-conditioned softmax routing**: A learnable router adjusts token identity vs. context usage at each layer depth
- More token identity early (when position/identity matters), more context later (when semantics matter)

This is particularly important for diffusion language models where token identity reconstruction is critical.

## Key Papers
- [[sources/attention-is-all-you-need]] — Introduced the Transformer
- [[sources/bert]] — Encoder-only variant
- [[sources/llama]] — Modern decoder-only template
- [[sources/flash-attention]] — Efficient attention computation
- [[sources/scaling-implicit-deductive-reasoning]] — Scaling properties of implicit deductive reasoning
- [[sources/tide-token-index]] — TIDE: Every layer knows the token beneath the context

## See Also
- [[concepts/tokenization]] — Text → token IDs (first step before the Transformer)
- [[concepts/self-attention]]
- [[concepts/pre-training]]
- [[concepts/scaling-laws]]
