---
type: concept
tags: [embeddings, retrieval, rag, sentence-transformers]
---

# Text Embeddings

> Encoding text as **dense vector representations** that capture semantic meaning — powering search, retrieval-augmented generation (RAG), clustering, and classification. From [[sources/sentence-bert|Sentence-BERT]] (2019) to modern LLM-based embeddings, the open embedding ecosystem now matches or exceeds proprietary alternatives.

## Overview
Text embeddings transform text into fixed-dimensional vectors where semantic similarity is captured by vector distance. They are a critical component of modern AI systems — powering the retrieval step in [[concepts/rag|RAG]], semantic search, document clustering, and similarity-based classification.

## Evolution

### Era 1: Siamese Encoders (2019–2022)
[[sources/sentence-bert|Sentence-BERT]] established the paradigm:
- Siamese BERT networks → mean pooling → cosine similarity
- Reduced 65 hours of pairwise search to 5 seconds
- `sentence-transformers` library (100M+ pip installs)
- Models: SBERT, MiniLM, MPNet variants (up to 37M downloads)

### Era 2: Weakly-Supervised Pretraining (2022–2023)
[[sources/e5|E5]] introduced large-scale web pair pretraining:
- CCPairs: 1.3B text pairs from Common Crawl
- "query:"/"passage:" instruction prefix pattern
- First to beat BM25 across all BEIR datasets
- Established MTEB as the evaluation standard

### Era 3: Fully Open Embeddings (2024+)
[[sources/nomic-embed|Nomic Embed]] proved fully open models match proprietary:
- Open weights + code + training data
- 8K context via RoPE (vs. 512 token limit of earlier models)
- Beat OpenAI Ada-002 on MTEB

## How It Works

### Training Pipeline (3 stages)
1. **Masked Language Modeling**: Pre-train a bidirectional encoder (BERT-style)
2. **Weakly-Supervised Contrastive Pretraining**: Train on large-scale text pairs using InfoNCE loss
3. **Supervised Contrastive Fine-tuning**: Fine-tune on labeled datasets with hard negative mining

### Key Architecture Choices
- **Encoder**: Bidirectional transformer (BERT/RoBERTa variants) — not decoder-only
- **Pooling**: Mean pooling (preferred) or [CLS] token
- **Dimensionality**: 768–1536 dimensions
- **Context length**: 512 (legacy) → 8192+ (modern, via RoPE)
- **Instruction prefixes**: "query:" / "passage:" improve retrieval intent

### Matryoshka Representation Learning (MRL)
- Train embeddings that work at multiple dimensionalities simultaneously
- Can truncate 768-dim to 256 or 128 dims with minimal quality loss

## Key Models
| Model | Year | Context | Open | MTEB |
|---|---|---|---|---|
| [[sources/sentence-bert\|SBERT]] | 2019 | 512 | ✅ | Foundation |
| [[sources/e5\|E5-large-v2]] | 2022 | 512 | ✅ | SOTA at release |
| [[sources/nomic-embed\|Nomic Embed v1]] | 2024 | 8192 | ✅ (fully) | Beats Ada-002 |
| E5-mistral-7b | 2024 | 4096 | ✅ | LLM-based embeddings |
| GTE-Qwen2 | 2024 | 8192 | ✅ | Alibaba embeddings |

## Applications
1. **RAG** ([[concepts/rag]]): Retrieve relevant documents to augment LLM generation
2. **Semantic search**: Find documents by meaning, not keywords
3. **Clustering**: Group similar documents automatically
4. **Classification**: Use embeddings as features for downstream classifiers
5. **Deduplication**: Find near-duplicate documents (used in [[sources/fineweb|FineWeb]])

## Key Papers
- [[sources/sentence-bert]] — Siamese BERT networks (foundational)
- [[sources/e5]] — Weakly-supervised contrastive pretraining
- [[sources/nomic-embed]] — First fully open embedding model to beat OpenAI
- [[sources/bert]] — BERT encoder architecture (foundation for all embedding models)

## See Also
- [[comparisons/embedding-models]] — Detailed embedding model comparison
- [[concepts/rag]]
- [[concepts/self-attention]]
- [[concepts/transformer-architecture]]
