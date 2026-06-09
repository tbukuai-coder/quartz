---
type: source
arxiv_id: "2510.02294"
title: "F2LLM Technical Report: Matching SOTA Embedding Performance with 6 Million Open-Source Data"
authors: ["Ziyin Zhang", "Zihan Liao", "Hang Yu", "Peng Di", "Rui Wang"]
date: 2025-10-03
org: "CodeFuse / Ant Group"
tags: [embeddings, contrastive-learning, open-data, mteb, 2025]
upvotes: 48
---

# F2LLM: SOTA Embeddings with Open Data

> **Foundation to Feature LLMs** — a suite of embedding models (0.6B, 1.7B, 4B) that achieve SOTA performance on MTEB by fine-tuning foundation LLMs on just **6 million open-source, non-synthetic training examples**, eliminating the need for massive contrastive pretraining or costly synthetic data. 462 GitHub ⭐.

## Key Contributions
- **Open-data SOTA**: Matches top MTEB leaderboard performance using **only 6M open-source, non-synthetic data** — no proprietary or synthetic training data needed
- **Simple pipeline**: Directly fine-tunes foundation LLMs into embedding models without contrastive pretraining stage — dramatically simpler than prior approaches (GTE, BGE-M3, Gecko)
- **Three sizes**: F2LLM-0.6B, F2LLM-1.7B, F2LLM-4B — covering efficiency to quality spectrum
- **F2LLM-4B**: Ranks **2nd** among ~4B parameter models and **7th overall** on MTEB English leaderboard
- **F2LLM-1.7B**: Ranks **1st** among models in the 1B–2B parameter range on MTEB
- Fully reproducible: open models, training dataset, and code

## Method
1. **Data collection**: Compile 4.9M retrieval samples, 0.2M classification samples, 0.8M clustering samples from open-source datasets in a unified (query, positive, hard negatives ×24) format
2. **Training**: Contrastive learning with hard negative mining — directly fine-tune from foundation models (no contrastive pretraining needed)
3. **Loss**: Hard negative contrastive loss + in-batch negatives + cross-device negatives for maximum negative sample efficiency
4. **Model**: Uses last-token pooling (decoder-only LLM) with instruction-aware training

Key insight: Prior SOTA embedding models (NV-Embed, GTE-Qwen2) require billion-scale contrastive pretraining and/or expensive synthetic data generation. F2LLM shows this is unnecessary — careful curation of existing open datasets and direct fine-tuning is sufficient.

## Results
- **MTEB English** (41 tasks): F2LLM-4B ranks 7th overall, 2nd among ~4B models
- **F2LLM-1.7B**: Best in the 1B–2B range, outperforming GTE-Qwen2-1.5B
- **F2LLM-0.6B**: Competitive with models 2–3× its size
- Competitive on all MTEB task types: retrieval, classification, clustering, STS, reranking
- Training cost: fraction of prior SOTA approaches (no contrastive pretraining phase)

## Connections
- **Builds on**: [[sources/sentence-bert|SBERT]], [[sources/e5|E5]], [[sources/nomic-embed|Nomic Embed]]
- **Related**: GTE-Qwen2 (Alibaba), NV-Embed-v2 (NVIDIA), BGE-M3
- **Concepts**: [[concepts/embeddings|Embeddings]], [[concepts/contrastive-learning|Contrastive Learning]]
- **Comparison**: [[comparisons/embedding-models|Embedding Models Comparison]]
- **GitHub**: https://github.com/codefuse-ai/CodeFuse-Embeddings

## Citation
> Zhang et al., "F2LLM Technical Report: Matching SOTA Embedding Performance with 6 Million Open-Source Data," arXiv:2510.02294, 2025.
