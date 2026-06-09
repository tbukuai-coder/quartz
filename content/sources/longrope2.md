---
type: source
arxiv_id: "2502.20082"
title: "LongRoPE2: Near-Lossless LLM Context Window Scaling"
authors: ["Microsoft Research"]
date: 2025-02-27
org: "Microsoft"
tags: [long-context, positional-encodings, rope, 2025]
upvotes: 36
---

# LongRoPE2

> Near-lossless context window extension using rescaled RoPE and mixed-context training, fewer training tokens than LongRoPE.

## Key Contributions
- Near-lossless context extension preserving >99% short-context performance
- Simplified rescaling strategy vs LongRoPE
- Mixed-context training prevents short-context degradation
- Requires 30-50% fewer training tokens than LongRoPE

## Method
1. Simplified per-dimension RoPE rescale factor search
2. Mixed-context training: interleave short (4K) and long (64K-128K) sequences
3. Perplexity-guided optimization at both short and long contexts

## Results
- Less than 0.5% degradation on short-context benchmarks
- Competitive with LongRoPE and YaRN at 64K-128K
- More training efficient than LongRoPE

## Connections
- Extends: [[sources/longrope|LongRoPE]], [[sources/yarn|YaRN]]
- Related: [[concepts/long-context|Long Context]], [[concepts/positional-encodings|Positional Encodings]]

## Citation
> "LongRoPE2: Near-Lossless LLM Context Window Scaling," arXiv:2502.20082, 2025.
