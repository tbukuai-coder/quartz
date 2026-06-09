---
type: source
arxiv_id: "1908.10084"
title: "Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks"
authors: ["Nils Reimers", "Iryna Gurevych"]
date: 2019-08-27
org: "UKP Lab, TU Darmstadt"
tags: [embeddings, retrieval, sentence-similarity, foundational]
upvotes: 12
---

# Sentence-BERT (SBERT)

> The foundational paper for sentence embeddings — enabling semantic similarity search in milliseconds instead of hours by producing fixed-size sentence vectors via Siamese BERT networks. Powers the most downloaded model family on HF Hub (37M+ downloads).

## Key Contributions
- **Siamese/triplet BERT networks**: Two identical BERTs process sentences independently → pooled → compared via cosine similarity
- **From 65 hours to 5 seconds**: Finding most similar pair in 10K sentences goes from O(n²) BERT cross-encoder to O(n) pre-computed embeddings
- **Mean pooling > CLS token**: Simple mean over token embeddings outperforms [CLS] token for sentence representation
- **Transfer learning for similarity**: Fine-tune on NLI data (SNLI + MultiNLI) → excellent zero-shot STS performance

## Method
1. **Architecture**: Siamese network — both sentences processed by same BERT independently
2. **Pooling**: Mean pooling of token embeddings → fixed-size sentence vector (768-dim for BERT-base)
3. **Training objectives**:
   - **Classification**: Softmax over `[u; v; |u-v|]` for NLI (entailment/contradiction/neutral)
   - **Regression**: Cosine similarity loss for STS datasets
   - **Triplet**: Triplet loss with anchor, positive, negative
4. **Inference**: Pre-compute all embeddings once → cosine similarity for any pair in O(1)

## Results
- STS benchmark: Competitive with BERT cross-encoder at 10,000× lower compute
- Outperforms InferSent, Universal Sentence Encoder on STS tasks
- Clustering accuracy significantly above bag-of-words and averaged GloVe
- Enabled practical semantic search, duplicate detection, paraphrase mining

## Impact on the Ecosystem
SBERT created the **sentence-transformers** library and model ecosystem:
- `sentence-transformers` library: >100M pip installs
- Most downloaded model family on HF Hub (37M+ downloads for multilingual MiniLM)
- Foundation for: [[sources/nomic-embed|Nomic Embed]], [[sources/e5|E5]], all modern embedding models
- Spawned MTEB benchmark for embedding evaluation

## Connections
- Builds on: [[sources/bert|BERT]] (base architecture)
- Extended by: [[sources/e5|E5]], [[sources/nomic-embed|Nomic Embed]], GTE, BGE
- Concepts: [[concepts/embeddings|Text Embeddings]], [[concepts/sentence-transformers|Sentence Transformers]]
- Library: `sentence-transformers` on HF

## Citation
> Reimers & Gurevych, "Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks," EMNLP 2019, arXiv:1908.10084.
