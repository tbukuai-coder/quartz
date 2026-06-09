---
type: concept
tags: [architecture, efficiency]
---

# Sliding Window Attention (SWA)

> Each layer attends only to a **fixed window of recent tokens** instead of the full sequence — enabling efficient processing of arbitrarily long sequences through cross-layer information propagation.

## Overview
Standard attention has O(n²) cost. SWA limits each layer's attention to a fixed window W (e.g., 4096 tokens), making per-layer cost O(n·W). Information from distant tokens propagates across layers — with 32 layers and W=4096, a token can theoretically attend to 32×4096 = 131K previous tokens.

## How It Works
- Layer L attends to tokens in range `[position - W, position]`
- After L layers, receptive field is `L × W` tokens
- Combined with **Rolling Buffer Cache**: fixed-size KV cache that overwrites oldest entries

## Key Papers
- [[sources/mistral-7b]] — Introduced SWA to open-source LLMs (W=4096)
- [[sources/mixtral]] — Retained SWA from Mistral

## See Also
- [[concepts/self-attention]]
- [[concepts/gqa]]
- [[concepts/flash-attention]]
