---
type: concept
tags: [retrieval, rag, inference]
---

# RAG (Retrieval-Augmented Generation)

> Combining a language model with an **external knowledge retrieval system** — the model retrieves relevant documents at query time and conditions its generation on them, improving factual accuracy and enabling knowledge updates.

## Overview
RAG, introduced in [[sources/rag|Lewis et al. 2020]], addresses a fundamental limitation of LLMs: their knowledge is frozen at training time and stored implicitly in weights. RAG augments the model with explicit access to a document store, enabling it to look up facts, cite sources, and stay current.

## How It Works
```
User Query → Retriever → Top-k Documents → [Query + Documents] → LLM → Response
```

### Components
1. **Retriever**: Finds relevant documents (dense vector search, BM25, or hybrid)
2. **Document Store**: Indexed corpus (embeddings in a vector DB, or keyword index)
3. **Generator**: LLM that conditions on both the query and retrieved context
4. **Re-ranker** (optional): Scores retrieved documents for relevance

### Retrieval Methods
| Method | Type | Pros | Cons |
|---|---|---|---|
| **Dense retrieval** | Vector similarity (embeddings) | Semantic matching | Needs embedding model |
| **BM25** | Keyword matching | Fast, no training | No semantic understanding |
| **Hybrid** | Both | Best of both worlds | More complex |

## RAG vs. Fine-tuning
| Aspect | RAG | Fine-tuning |
|---|---|---|
| Knowledge update | Swap the index | Retrain the model |
| Factual grounding | Cites specific documents | Knowledge in weights |
| Cost | Cheap (no training) | Expensive (GPU hours) |
| Hallucination | Reduced (grounded) | Still possible |
| Private data | Just add to index | Must train on it |

## Ecosystem
- **LangChain, LlamaIndex**: Popular RAG frameworks
- **FAISS, Chroma, Weaviate**: Vector databases
- **Sentence Transformers**: Embedding models for retrieval
- **ChatGPT file uploads, NotebookLM**: Consumer RAG products

## Key Papers
- [[sources/rag]] — Original RAG paper

## See Also
- [[concepts/pre-training]]
- [[entities/models/bert-model]] (often used as retriever encoder)
