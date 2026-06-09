---
type: source
arxiv_id: "2310.06825"
title: "Retrieval-Augmented Generation for Large Language Models: A Survey"
authors: ["Yunfan Gao", "Yun Xiong", "et al."]
date: 2023-10-12
org: "Tongji University"
tags: [rag, retrieval, survey, 2023]
upvotes: 15
---

# RAG Survey: Retrieval-Augmented Generation for Large Language Models

> **Note**: The foundational RAG paper already exists at [[sources/rag]]. This entry covers the comprehensive RAG survey that catalogs the evolution from Naive RAG to Advanced RAG to Modular RAG, serving as the definitive reference for the RAG landscape.

## RAG Evolution (from the survey)

### Naive RAG (2020–2022)
```
Query → Retrieve documents → Concatenate with query → Generate answer
```
- Simple retrieve-then-read pipeline
- Problems: Retrieval quality bottleneck, "lost in the middle" for long contexts, hallucination from irrelevant retrieved docs

### Advanced RAG (2023)
- **Pre-retrieval**: Query rewriting, HyDE (hypothetical document embeddings)
- **Retrieval**: Dense retrievers ([[sources/e5|E5]], [[sources/nomic-embed|Nomic]]), hybrid search
- **Post-retrieval**: Reranking, compression, filtering irrelevant docs
- **Generation**: Citation-grounded generation, self-consistency checks

### Modular RAG (2024+)
- **Routing**: Decide whether to retrieve at all
- **Iterative**: Multiple retrieval rounds with intermediate reasoning
- **Adaptive**: Model decides retrieval strategy based on query complexity
- **Agentic RAG**: [[concepts/agents|Agent-based]] retrieval with tool use

## Key Components

| Component | Options | Best Open Practice |
|---|---|---|
| **Embeddings** | SBERT, E5, Nomic, LLM-based | See [[comparisons/embedding-models]] |
| **Vector Store** | FAISS, Qdrant, Weaviate, Chroma | Task-dependent |
| **Reranker** | Cross-encoders, Cohere Rerank, ColBERT | Cross-encoder + DeBERTa |
| **Chunking** | Fixed-size, semantic, recursive | Semantic chunking preferred |
| **Generator** | Any LLM | Qwen, Llama, Mistral |

## See Also
- [[sources/rag]] — Original RAG paper
- [[concepts/rag]] — RAG concept page
- [[concepts/embeddings]] — Embedding models
- [[comparisons/embedding-models]] — Embedding model comparison
