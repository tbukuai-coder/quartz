---
type: source
arxiv_id: "2506.20920"
title: "FineWeb2: One Pipeline to Scale Them All — Adapting Pre-Training Data Processing to Every Language"
authors: ["Guilherme Penedo", "Hynek Kydlíček", "Vinko Sabolčec", "Various"]
date: 2025-06-26
org: "Hugging Face"
tags: [data-curation, multilingual, pre-training, 2025]
upvotes: 78
---

# FineWeb2

> HuggingFace's multilingual successor to FineWeb — a data curation pipeline that automatically adapts filtering and deduplication to any language, enabling high-quality multilingual pretraining datasets from Common Crawl.

## Key Contributions
- **Language-agnostic pipeline**: Automatically adapts filtering, deduplication, and quality scoring to any language — no per-language engineering needed
- **Multilingual FineWeb**: Extends the FineWeb methodology from English to all Common Crawl languages
- **Dataset rebalancing**: Strategies for balancing high/low-resource languages in training mixtures
- Produces datasets that **improve multilingual LLM performance** over prior multilingual corpora
- Open-source pipeline + datasets from [[entities/orgs/huggingface|Hugging Face]]

## Method
Extends FineWeb's pipeline with:
1. **Language-adaptive filtering**: Quality classifiers that transfer across languages via multilingual embeddings
2. **Cross-lingual deduplication**: Handles deduplication within and across languages
3. **Automatic evaluation**: Per-language evaluation tasks to measure dataset quality
4. **Rebalancing**: Optimized language proportions based on downstream performance signals

## Results
- Improved multilingual model performance over existing open multilingual datasets
- Effective for both high-resource (English, Chinese) and low-resource languages
- Pipeline scales to all languages present in Common Crawl

## Connections
- **Sequel to**: [[sources/fineweb|FineWeb/FineWeb-Edu]]
- **Org**: [[entities/orgs/huggingface|Hugging Face]]
- **Related**: [[entities/datasets/fineweb|FineWeb entity]], [[concepts/data-mixing|Data Mixing]], [[concepts/multilingual-models|Multilingual Models]]
- **Complements**: [[sources/nllb|NLLB]] (multilingual translation), [[sources/aya|Aya]] (multilingual instruct)

## Citation
> Penedo et al., "FineWeb2: One Pipeline to Scale Them All," arXiv:2506.20920, 2025.
