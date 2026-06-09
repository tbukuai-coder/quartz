---
type: source
arxiv_id: "2005.11401"
title: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
authors: ["Patrick Lewis", "Ethan Perez", "Aleksandra Piktus", "et al."]
date: 2020-05-22
org: "Facebook AI Research / UCL / NYU"
tags: [retrieval, rag, foundational]
upvotes: 14
---

# RAG: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

> Introduced the **RAG paradigm** — combining a pre-trained language model with a non-parametric retrieval system to access external knowledge at generation time, improving factual accuracy and enabling knowledge updates.

## Key Contributions
- Defined the **RAG architecture**: pre-trained seq2seq model + differentiable retrieval over a document index
- Showed that combining **parametric memory** (model weights) with **non-parametric memory** (retrieved documents) outperforms either alone
- Achieved SOTA on open-domain QA, fact verification, and Jeopardy question generation
- Demonstrated that the model generates more **specific, diverse, and factual** text
- Coined the term "RAG" that has become ubiquitous in the LLM ecosystem

## Method
### Architecture
```
Query → Dense Retriever (DPR) → Top-k Documents → Concat with Query → Seq2Seq Generator → Answer
```

1. **Dense Passage Retriever (DPR)**: Encodes query and documents into dense vectors; retrieves top-k via MIPS (Maximum Inner Product Search)
2. **Generator**: BART (seq2seq model) conditions on the query and retrieved documents
3. **End-to-end training**: Both retriever and generator are jointly fine-tuned

### Two Variants
- **RAG-Sequence**: Same documents used for the entire output sequence
- **RAG-Token**: Different documents can be retrieved for different output tokens

## Results
- SOTA on **Natural Questions** (open-domain QA) — 44.5 EM
- SOTA on **WebQuestions** and **CuratedTrec**
- More factual and specific generation than parametric-only baselines
- Can update knowledge by simply swapping the document index

## Connections
- **Influenced**: Entire RAG ecosystem — ChatGPT file uploads, enterprise Q&A systems, NotebookLM
- **Key concepts**: [[concepts/rag]], [[concepts/pre-training]]
- **Related**: [[sources/bert]] (retriever foundation), [[sources/llama-3]] (tool-use for retrieval)

## Citation
> Lewis et al., "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks," arXiv:2005.11401, 2020.
> https://huggingface.co/papers/2005.11401
