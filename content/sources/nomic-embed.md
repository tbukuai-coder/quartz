---
type: source
arxiv_id: "2402.01613"
title: "Nomic Embed: Training a Reproducible Long Context Text Embedder"
authors: ["Zach Nussbaum", "John X. Morris", "Brandon Duderstadt", "Andriy Mulyar"]
date: 2024-02-02
org: "Nomic AI"
tags: [embeddings, retrieval, open-source, 2024]
upvotes: 17
---

# Nomic Embed: Training a Reproducible Long Context Text Embedder

> The first **fully open-source, open-weights, open-data** long-context (8192 tokens) text embedding model — outperforming OpenAI Ada-002 and text-embedding-3-small on both short and long context benchmarks. Released with complete training code and 235M curated training pairs.

## Key Contributions
- **nomic-embed-text-v1**: First fully reproducible, open embedding model to beat OpenAI closed models
- **8192 token context**: Supports long documents — most prior open models limited to 512 tokens
- **Fully open**: Model weights (Apache 2.0), training code, and 235M curated text pairs all released
- **3-stage training**: Masked language modeling → weakly-supervised contrastive pretraining → supervised contrastive fine-tuning
- **nomic-bert-2048**: Custom BERT variant with RoPE (Rotary Positional Embeddings), SwiGLU, and Flash Attention for efficient long-context encoding
- Training replicable in 1 week on a single 8×H100 node

## Method
### Stage 1: Masked Language Modeling
- Train **nomic-bert-2048**: BERT-base architecture modified with RoPE, SwiGLU activations, Flash Attention
- Trained on BooksCorpus + Wikipedia with 2048 token context
- RoPE enables later extension to 8192 tokens

### Stage 2: Weakly-Supervised Contrastive Pretraining
- **235M text pairs** from diverse sources: Reddit title-body, Wikipedia links, S2ORC citations, Stack Exchange Q&A, web search queries
- InfoNCE contrastive loss with in-batch negatives
- Extend context to 2048 tokens
- Matryoshka Representation Learning (MRL): train with multiple embedding dimensionalities simultaneously

### Stage 3: Supervised Contrastive Fine-tuning
- Fine-tune on high-quality human-labeled datasets: MS MARCO, NQ, HotpotQA, NLI
- Mine hard negatives from Stage 2 model
- Extend to 8192 context via RoPE position interpolation (NTK-aware scaling)
- 1 hour of training

### Architecture: nomic-bert-2048
- BERT-base size (137M parameters)
- **RoPE** instead of absolute positional embeddings → enables context extension
- **SwiGLU** activations → better performance than GELU
- **Flash Attention** → efficient long-sequence processing
- Matches or exceeds BERT-base/RoBERTa on GLUE benchmarks

## Results
### MTEB (Short Context)
| Model | Avg Score | Open Weights | Open Data | Open Code |
|---|---|---|---|---|
| nomic-embed-text-v1 | **62.39** | ✅ | ✅ | ✅ |
| OpenAI Ada-002 | 61.0 | ❌ | ❌ | ❌ |
| text-embedding-3-small | 62.26 | ❌ | ❌ | ❌ |
| jina-embeddings-v2 | 60.39 | ✅ | ❌ | ❌ |

### Long Context (LoCo Benchmark)
| Model | Avg Score |
|---|---|
| nomic-embed-text-v1 | **54.16** |
| jina-embeddings-v2 | 53.87 |
| OpenAI Ada-002 | 44.0 |

- First open model to beat Ada-002 on both short and long context
- Competitive with text-embedding-3-small while being fully reproducible

## Connections
- **Builds on**: [[sources/bert]] (BERT architecture), [[sources/flash-attention]] (efficient attention)
- **Related**: [[sources/rag]] (embedding models power retrieval in RAG)
- **Key concepts**: [[concepts/embeddings]], [[concepts/rag]], [[concepts/flash-attention]]
- **Organizations**: [[entities/orgs/nomic-ai]]
- **GitHub**: [nomic-ai/contrastors](https://github.com/nomic-ai/contrastors)

## Citation
> Nussbaum et al., "Nomic Embed: Training a Reproducible Long Context Text Embedder," arXiv:2402.01613, 2024.
> https://huggingface.co/papers/2402.01613
