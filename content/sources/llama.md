---
type: source
arxiv_id: "2302.13971"
title: "LLaMA: Open and Efficient Foundation Language Models"
authors: ["Hugo Touvron", "Thibaut Lavril", "Gautier Izacard", "et al."]
date: 2023-02-27
org: "Meta AI"
tags: [open-models, pre-training, foundational, 2023]
upvotes: 23
---

# LLaMA: Open and Efficient Foundation Language Models

> Demonstrated that **state-of-the-art models can be trained exclusively on publicly available data**, releasing the LLaMA series (7B–65B) that catalyzed the open-source LLM revolution.

## Key Contributions
- Trained competitive models **entirely on public data** (no proprietary datasets)
- LLaMA-13B outperforms GPT-3 (175B) on most benchmarks — a 13× parameter efficiency gain
- LLaMA-65B competitive with Chinchilla-70B and PaLM-540B
- Released model weights, enabling the open-source ecosystem to flourish
- Applied Chinchilla scaling laws: more tokens for smaller models

## Method
Architecture modifications over the original Transformer:
- **RMSNorm** (pre-normalization) instead of LayerNorm
- **SwiGLU** activation function instead of ReLU
- **Rotary Positional Embeddings (RoPE)** instead of absolute positional encodings
- Standard autoregressive language modeling objective

Training data (1.4T tokens for largest model):
- CommonCrawl (67%), C4 (15%), GitHub (4.5%), Wikipedia (4.5%), Books (4.5%), ArXiv (2.5%), StackExchange (2%)

## Models Released
| Model | Params | Training Tokens |
|---|---|---|
| LLaMA-7B | 7B | 1.0T |
| LLaMA-13B | 13B | 1.0T |
| LLaMA-33B | 33B | 1.4T |
| LLaMA-65B | 65B | 1.4T |

## Connections
- **Builds on**: [[sources/attention-is-all-you-need]], Chinchilla scaling laws
- **Continued by**: [[sources/llama-2]] (open release with chat models)
- **Spawned**: Alpaca, Vicuna, [[entities/models/guanaco]], entire open-source ecosystem
- **Architecture reused by**: [[sources/mistral-7b]], [[sources/deepseekmath]]
- **Key concepts**: [[concepts/pre-training]], [[concepts/scaling-laws]], [[concepts/transformer-architecture]]
- **Models**: [[entities/models/llama]]
- **Organizations**: [[entities/orgs/meta]]

## Citation
> Touvron et al., "LLaMA: Open and Efficient Foundation Language Models," arXiv:2302.13971, 2023.
> https://huggingface.co/papers/2302.13971
