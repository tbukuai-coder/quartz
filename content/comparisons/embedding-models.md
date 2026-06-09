---
type: comparison
tags: [embeddings, retrieval, rag, synthesis]
---

# Comparison: Embedding Models — From SBERT to Open SOTA

> A side-by-side analysis of the major open text embedding models, tracing the evolution from **Sentence-BERT** (2019) through **E5** and **Nomic Embed** to modern LLM-based embeddings — and how open models closed the gap with proprietary offerings like OpenAI's Ada-002.

## Overview

Text embeddings power the retrieval backbone of modern AI systems — from [[concepts/rag|RAG]] pipelines to semantic search, classification, and clustering. The embedding landscape has undergone four major shifts: (1) Siamese BERT encoders, (2) weakly-supervised contrastive pretraining on web data, (3) LLM-based embeddings with instruction awareness, and (4) tabular embeddings for structured data. The open ecosystem now matches or exceeds proprietary alternatives on the **MTEB (Massive Text Embedding Benchmark)**, the standard evaluation framework.

## Model Comparison

| Model | Year | Org | Base Arch | Params | Context | Training Data | MTEB Score | Open |
|---|---|---|---|---|---|---|---|---|
| [[sources/sentence-bert\|SBERT]] | 2019 | UKP Lab | BERT | 110M | 512 | NLI + STS | Foundation | ✅ Weights |
| MiniLM-L12 | 2020 | Microsoft | MiniLM | 33M | 512 | Distilled SBERT | Good | ✅ Weights |
| [[sources/e5\|E5-large-v2]] | 2022 | Microsoft | BERT-large | 335M | 512 | CCPairs (1.3B) + NLI | SOTA at release | ✅ Weights |
| OpenAI Ada-002 | 2022 | OpenAI | Unknown | Unknown | 8191 | Proprietary | Strong | ❌ API only |
| [[sources/nomic-embed\|Nomic Embed v1]] | 2024 | Nomic AI | BERT (mod.) | 137M | 8192 | Curated + CC | Beats Ada-002 | ✅ Fully open |
| E5-mistral-7B | 2024 | Microsoft | Mistral-7B | 7B | 4096 | Synthetic + real | Very strong | ✅ Weights |
| GTE-Qwen2-1.5B | 2024 | Alibaba | Qwen2-1.5B | 1.5B | 8192 | Large-scale | Very strong | ✅ Weights |
| Jina Embeddings v3 | 2024 | Jina AI | XLM-RoBERTa | 570M | 8192 | Multilingual | Strong | ✅ Weights |
| NV-Embed-v2 | 2024 | NVIDIA | Mistral-7B | 7B | 32768 | Curated | Top MTEB | ✅ Weights |
| [[sources/f2llm\|F2LLM-4B]] | 2025 | CodeFuse | Foundation LLM | 4B | — | **6M open-source** | 7th overall MTEB | ✅ Fully open |
| [[sources/f2llm\|F2LLM-1.7B]] | 2025 | CodeFuse | Foundation LLM | 1.7B | — | **6M open-source** | **1st in 1B–2B** | ✅ Fully open |
| [[sources/tabembed\|TabEmbed]] | 2026 | Various | Encoder | Various | — | TabBench suite | Tabular SOTA | ✅ Fully open |

## Architecture Evolution

### Era 1: Siamese Encoders (2019–2022)
[[sources/sentence-bert|Sentence-BERT]] established the paradigm:
- **Approach**: Siamese/triplet BERT networks → mean pooling → cosine similarity
- **Training**: NLI (Natural Language Inference) + STS (Semantic Textual Similarity) supervision
- **Impact**: Reduced 65 hours of pairwise search to 5 seconds
- **Limitation**: 512-token context, English-only, limited task diversity
- **Legacy**: `sentence-transformers` library → 100M+ pip installs, 37M+ model downloads

### Era 2: Contrastive Pretraining on Web Pairs (2022–2023)
[[sources/e5|E5]] showed that web-scale weak supervision dramatically improves embeddings:
- **Key innovation**: CCPairs — 1.3B text pairs mined from Common Crawl (title-body, QA, etc.)
- **Training**: Contrastive pretraining on CCPairs → fine-tuning on labeled datasets
- **Instruction prefixes**: "query:" / "passage:" pattern improves retrieval intent
- **Impact**: First to beat BM25 across all BEIR datasets; established MTEB as standard

### Era 3: Fully Open Embeddings (2024+)
[[sources/nomic-embed|Nomic Embed]] proved fully open models can beat proprietary:
- **Open everything**: Weights + training code + training data + evaluation code
- **8K context**: Extended to 8192 tokens via RoPE (vs. 512 for legacy models)
- **Matryoshka training**: Embeddings work at multiple dimensionalities (768, 512, 256, 128)
- **Beat OpenAI Ada-002**: First fully open model to exceed the proprietary standard on MTEB

### Era 4: LLM-Based Embeddings (2024+)
Using decoder-only LLMs (Mistral, Qwen) as embedding backbones:
- **E5-mistral-7B**: Shows 7B decoder-only LLM can produce SOTA embeddings with synthetic training data
- **GTE-Qwen2**: Alibaba's embeddings built on Qwen2 base
- **Trade-off**: Much higher quality but 10–50× more expensive than BERT-size models
- **Key insight**: Instruction-following capability of LLMs transfers to embedding tasks

### Era 5: Open-Data SOTA — No Contrastive Pretraining Needed (2025+)
[[sources/f2llm|F2LLM]] demonstrated that the dominant two-stage pipeline (contrastive pretraining → fine-tuning) is unnecessary:
- **Direct fine-tuning**: Skip contrastive pretraining entirely — fine-tune foundation LLMs directly on curated open data
- **6M open-source examples**: Achieves MTEB SOTA using only non-synthetic, open-source training data
- **F2LLM-4B**: 2nd among ~4B models, 7th overall on MTEB English
- **F2LLM-1.7B**: **1st** among 1B–2B models, outperforming GTE-Qwen2-1.5B
- **Reproducible baseline**: Fully open models, dataset, and code — enabling the community to build on a strong, budget-friendly foundation
- **Implication**: Massive contrastive pretraining and costly synthetic data generation are not required for SOTA performance

### Era 6: Tabular Embeddings (2026+)
[[sources/tabembed|TabEmbed]] extends the embedding paradigm to **structured tabular data**:
- **Problem**: LLM-based approaches lack retrieval-compatible vector outputs for tables; text embedding models fail to capture tabular structure and numerical semantics
- **TabBench**: Comprehensive benchmark suite for tabular classification and retrieval
- **TabEmbed model**: Unified embedding space for both tabular classification and retrieval
- **Training**: Large-scale contrastive learning with **positive-aware hard negative mining**
- **Key insight**: Mining hard negatives that are semantically similar but from different labels improves contrastive learning on tabular data

## Key Differentiators

| Feature | SBERT Family | E5 Family | Nomic Embed | LLM-Based | F2LLM | TabEmbed |
|---|---|---|---|---|---|---|
| **Speed** | ⚡ Fastest | ⚡ Fast | ⚡ Fast | 🐢 10–50× slower | 🐢 Moderate | Moderate |
| **Quality** | Good | Very good | Very good | Best | SOTA (open data) | Tabular SOTA |
| **Context** | 512 | 512 | 8192 | 4K–32K | — | — |
| **Multilingual** | Via distillation | E5-multilingual | Limited | Good (Qwen) | English | English |
| **Matryoshka** | Some variants | No | ✅ Yes | Some variants | — | — |
| **Cost** | Very low | Low | Low | High | **Medium** | Medium |
| **Openness** | Weights | Weights | Fully open | Weights | **Fully open** | Fully open |
| **Training Complexity** | Low | Medium | Medium | High (CPT needed) | **Low** (no CPT) | Medium |
| **Data Type** | Text | Text | Text | Text | Text | **Tabular** |

## Choosing an Embedding Model

### For Production RAG / Search
- **Budget-constrained**: MiniLM-L12 (33M params, very fast, good quality)
- **Balanced**: Nomic Embed v1.5 or E5-large-v2 (quality + speed + long context)
- **Maximum quality**: NV-Embed-v2 or E5-mistral-7B (LLM-based, highest MTEB)
- **Best open-data baseline**: [[sources/f2llm|F2LLM-1.7B]] or F2LLM-4B (SOTA with fully open training)

### For Multilingual
- **Small**: multilingual-e5-large (BERT-based, 100+ languages)
- **Large**: GTE-Qwen2 (Qwen base, strong CJK)
- **European**: Jina Embeddings v3 (multilingual, task-specific LoRA)

### For Code
- StarEncoder (from [[entities/models/starcoder|StarCoder]] project)
- CodeBERT / UniXcoder
- Voyage Code (proprietary)

### For Tabular Data
- [[sources/tabembed|TabEmbed]] — generalist tabular embeddings for classification and retrieval
- Requires tabular tokenization and positive-aware hard negative mining

## The MTEB Benchmark
**MTEB (Massive Text Embedding Benchmark)** is the standard for embedding evaluation:
- **8 task types**: Classification, Clustering, Pair Classification, Reranking, Retrieval, STS, Summarization, BitextMining
- **58+ datasets** across tasks
- **Public leaderboard**: Hosted on Hugging Face
- **Multilingual extensions**: MTEB-fr, MTEB-pl, etc.

Key observation: No single model dominates all tasks — retrieval-optimized models may underperform on classification, and vice versa.

## Tabular Embedding Benchmark (TabBench)

[[sources/tabembed|TabEmbed]] introduces **TabBench**, a comprehensive benchmark for tabular understanding:
- Evaluates both tabular classification and tabular retrieval
- Tests semantic matching problems on structured data
- Requires models to capture both categorical structure and numerical semantics
- Hard negative mining is critical: random negatives are too easy; semantically similar negatives from different labels are needed

## Key Papers
- [[sources/sentence-bert]] — Sentence-BERT (foundational)
- [[sources/e5]] — E5 and contrastive pretraining on web pairs
- [[sources/nomic-embed]] — Nomic Embed (first fully open model beating Ada-002)
- [[sources/f2llm]] — F2LLM (SOTA with open data, no contrastive pretraining)
- [[sources/tabembed]] — TabEmbed (generalist embeddings for tabular understanding)
- [[sources/bert]] — BERT (foundation architecture for most embedding models)
- [[sources/siglip]] — SigLIP (sigmoid loss, applicable to VL embeddings)

## See Also
- [[concepts/embeddings]] — Text Embeddings concept page
- [[concepts/contrastive-learning]] — Contrastive learning methodology
- [[concepts/rag]] — RAG (primary consumer of embeddings)
- [[comparisons/open-model-families]] — Open model comparison
