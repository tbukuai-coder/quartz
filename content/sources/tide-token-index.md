---
type: source
arxiv_id: "2605.06216"
title: "TIDE: Every Layer Knows the Token Beneath the Context"
authors: ["Ajay Jaiswal", "Lauren Hannah", "Han-Byul Kim", "Duc Hoang", "Mehrdad Farajtabar", "Minsik Cho"]
date: 2026-05
tags: [transformer-architecture, tokenization, rare-tokens, diffusion-models, embedding, llm-design]
upvotes: 0
---

# TIDE: Every Layer Knows the Token Beneath the Context

> Addresses two structural failures in LLM design — the Rare Token Problem and Contextual Collapse — by introducing EmbeddingMemory, which reintroduces token identity information at each layer through context-free semantic vectors and depth-conditioned routing.

## Key Contributions
- Revisits the universally accepted design choice: a token index is looked up once at the input embedding layer and permanently discarded
- Identifies two structural failures caused by this single-injection assumption:
  1. **Rare Token Problem**: Zipf-type vocabulary distribution causes rare-token embeddings to be chronically under-trained due to receiving a fraction of cumulative gradient signal
  2. **Contextual Collapse**: The model loses token identity information as depth increases, leading to degradation on token-sensitive tasks
- Introduces **EmbeddingMemory** — a mechanism that reintroduces token identity at each layer
- Uses context-free semantic vector computation and depth-conditioned softmax routing

## Method
TIDE (Token Identity Distribution Enhancement) works as follows:
1. **EmbeddingMemory**: Maintains a learnable bank of token embeddings accessible at every layer
2. **Context-free semantic vectors**: Computes semantic similarity between current hidden states and token embeddings without attending to context
3. **Depth-conditioned routing**: Uses a learnable router that adjusts how much token identity vs. context to use at each layer depth
4. The router learns to use more token identity early (when position/identity matters) and more context later (when semantics matter)

This is particularly relevant for diffusion language models where token identity reconstruction is critical.

## Results
- Improves performance on tasks requiring token-level precision (code generation, structured generation)
- Reduces the rare token problem by distributing gradient signal more evenly
- Maintains or improves performance on standard language modeling benchmarks

## Datasets Used
- Standard language modeling and downstream task benchmarks

## Models Released
- None explicitly mentioned

## Connections
- Related: [[sources/dllm-simple-diffusion]] — diffusion language modeling where token identity matters
- Related: [[sources/llada2-uni]] — unified discrete diffusion LLM
- Related concept: [[concepts/tokenization]], [[concepts/transformer-architecture]]

## Citation
> Jaiswal et al., "TIDE: Every Layer Knows the Token Beneath the Context," arXiv:2605.06216, 2026.
